---
title: Initialisierung der Instanziierung
ms.date: 03/30/2017
ms.assetid: 154d049f-2140-4696-b494-c7e53f6775ef
ms.openlocfilehash: ae01254760219f2b408ef9d9663c4158e2802be8
ms.sourcegitcommit: 15109844229ade1c6449f48f3834db1b26907824
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2018
---
# <a name="instancing-initialization"></a>Initialisierung der Instanziierung
Dieses Beispiel erweitert die [Pooling](../../../../docs/framework/wcf/samples/pooling.md) durch Definieren einer Schnittstelle Sample `IObjectControl`, die passt die Initialisierung eines Objekts durch das Aktivieren und deaktivieren es an. Der Client ruft Methoden auf, die das Objekt an den Pool zurückgeben und das Objekt nicht an den Pool zurückgeben.  
  
> [!NOTE]
>  Die Setupprozedur und die Buildanweisungen für dieses Beispiel befinden sich am Ende dieses Themas.  
  
## <a name="extensibility-points"></a>Erweiterungspunkte  
 Der erste Schritt beim Erstellen einer Windows Communication Foundation (WCF)-Erweiterung ist die zu verwendenden Erweiterungspunkt entscheiden. In WCF der Begriff *EndpointDispatcher* bezieht sich auf eine Laufzeitkomponente verantwortlich, konvertieren eingehende Nachrichten in Methodenaufrufe für den Dienst des Benutzers konvertiert und Rückgabewerte von dieser Methode in eine ausgehende Nachricht . Ein WCF-Dienst erstellt einen EndpointDispatcher für jeden Endpunkt.  
  
 Der EndpointDispatcher stellt mithilfe der <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>-Klasse die Erweiterung des Endpunktbereichs bereit (für alle vom Dienst empfangenen oder gesendeten Nachrichten). Mit dieser Klasse können Sie verschiedene Eigenschaften anpassen, die das Verhalten von EndpointDispatcher steuern. In diesem Beispiel wird in erster Linie die <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A>-Eigenschaft behandelt, die auf das Objekt zeigt, das die Instanzen der Dienstklasse bereitstellt.  
  
## <a name="iinstanceprovider"></a>IInstanceProvider  
 In WCF erstellt EndpointDispatcher Instanzen einer Dienstklasse mithilfe eines Instanz-Anbieters, implementiert die <xref:System.ServiceModel.Dispatcher.IInstanceProvider> Schnittstelle. Diese Schnittstelle verfügt über nur zwei Methoden:  
  
-   <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A>: Wenn eine Nachricht eingeht, ruft der Verteiler die <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A>-Methode auf, um eine Instanz der Dienstklasse zum Verarbeiten der Nachricht zu erstellen. Die Häufigkeit der Aufrufe dieser Methode wird von der <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>-Eigenschaft bestimmt. Wenn die <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>-Eigenschaft beispielsweise auf <xref:System.ServiceModel.InstanceContextMode.PerCall?displayProperty=nameWithType> festgelegt ist, wird eine neue Instanz der Dienstklasse erstellt, um alle eingehenden Nachrichten zu verarbeiten. Daher wird <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A> immer dann aufgerufen, wenn eine Nachricht eingeht.  
  
-   <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%2A>: Wenn die Dienstinstanz das Verarbeiten der Nachricht abgeschlossen hat, ruft EndpointDispatcher die <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%2A>-Methode auf. Wie bei der <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A>-Methode wird die Häufigkeit der Aufrufe dieser Methode von der <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>-Eigenschaft bestimmt.  
  
## <a name="the-object-pool"></a>Der Objektpool  
 Die `ObjectPoolInstanceProvider`-Klasse enthält die Implementierung des Objektpools. Diese Klasse implementiert die <xref:System.ServiceModel.Dispatcher.IInstanceProvider>-Schnittstelle für die Interaktion mit der Dienstmodellebene. Wenn EndpointDispatcher die <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A>-Methode aufruft, erstellt die benutzerdefinierte Implementierung keine neue Instanz, sondern sucht ein vorhandenes Objekt in einem Pool im Speicher. Wenn eines verfügbar ist, wird es zurückgegeben. Andernfalls überprüft `ObjectPoolInstanceProvider`, ob die `ActiveObjectsCount`-Eigenschaft (Anzahl der aus dem Pool zurückgegebenen Objekte) die maximale Poolgröße erreicht hat. Wenn dies nicht der Fall ist, wird eine neue Instanz erstellt und an den Aufrufer zurückgegeben, und anschließend wird `ActiveObjectsCount` inkrementiert. Andernfalls wird eine Objekterstellungsanforderung für einen konfigurierten Zeitraum in die Warteschlange gestellt. Die Implementierung für `GetObjectFromThePool` wird im folgenden Beispielcode dargestellt.  
  
```  
private object GetObjectFromThePool()  
{  
    bool didNotTimeout =   
       availableCount.WaitOne(creationTimeout, true);  
    if(didNotTimeout)  
    {  
         object obj = null;  
         lock (poolLock)  
        {  
             if (pool.Count != 0)  
             {  
                   obj = pool.Pop();  
                   activeObjectsCount++;  
             }  
             else if (pool.Count == 0)  
             {  
                   if (activeObjectsCount < maxPoolSize)  
                   {  
                        obj = CreateNewPoolObject();  
                        activeObjectsCount++;  
  
                        #if (DEBUG)  
                        WritePoolMessage(  
                             ResourceHelper.GetString("MsgNewObject"));  
                       #endif  
                   }                          
            }  
           idleTimer.Stop();  
      }  
     // Call the Activate method if possible.  
    if (obj is IObjectControl)  
   {  
         ((IObjectControl)obj).Activate();  
   }  
   return obj;  
}  
throw new TimeoutException(  
ResourceHelper.GetString("ExObjectCreationTimeout"));  
}  
```  
  
 Die benutzerdefinierte `ReleaseInstance`-Implementierung fügt die freigegebene Instanz dem Pool erneut hinzu und dekrementiert den `ActiveObjectsCount`-Wert. EndpointDispatcher kann diese Methoden von unterschiedlichen Threads aus aufrufen. Daher ist ein synchronisierter Zugriff auf die Member der Klassenebene in der `ObjectPoolInstanceProvider`-Klasse erforderlich.  
  
```  
public void ReleaseInstance(InstanceContext instanceContext, object instance)  
{  
    lock (poolLock)  
    {  
        // Check whether the object can be pooled.   
        // Call the Deactivate method if possible.  
        if (instance is IObjectControl)  
        {  
            IObjectControl objectControl = (IObjectControl)instance;  
            objectControl.Deactivate();  
  
            if (objectControl.CanBePooled)  
            {  
                pool.Push(instance);  
  
                #if(DEBUG)  
                WritePoolMessage(  
                    ResourceHelper.GetString("MsgObjectPooled"));  
                #endif                          
            }  
            else  
            {  
                #if(DEBUG)  
                WritePoolMessage(  
                    ResourceHelper.GetString("MsgObjectWasNotPooled"));  
                #endif  
            }  
        }  
        else  
        {  
            pool.Push(instance);  
  
            #if(DEBUG)  
            WritePoolMessage(  
                ResourceHelper.GetString("MsgObjectPooled"));  
            #endif   
        }  
  
        activeObjectsCount--;  
  
        if (activeObjectsCount == 0)  
        {  
            idleTimer.Start();                       
        }  
    }  
  
    availableCount.Release(1);  
}  
```  
  
 Die `ReleaseInstance` Methode bietet eine *bereinigungsinitialisierung* Funktion. Normalerweise wird im Pool eine Mindestanzahl von Objekten für die Lebensdauer des Pools beibehalten. Es kann jedoch Zeiten mit übermäßiger Auslastung geben, für die im Pool zusätzliche Objekte erstellt werden müssen, um die in der Konfiguration festgelegte Höchstgrenze zu erreichen. Wenn der Pool weniger aktiv ist, stellen diese überzähligen Objekte einen zusätzlichen Aufwand dar. Wenn `activeObjectsCount` daher 0 (null) erreicht, wird ein Leerlaufzeitgeber gestartet, der einen Bereinigungszyklus auslöst und ausführt.  
  
```  
if (activeObjectsCount == 0)  
{  
    idleTimer.Start();   
}  
```  
  
 ServiceModel-Ebenenerweiterungen werden mithilfe der folgenden Verhalten verknüpft:  
  
-   Dienstverhalten: Diese ermöglichen die Anpassung der ganzen Dienstlaufzeit.  
  
-   Endpunktverhalten: Diese ermöglichen das Anpassen eines bestimmten Dienstendpunkts, einschließlich EndpointDispatcher.  
  
-   Vertragsverhalten: Diese ermöglichen das Anpassen von <xref:System.ServiceModel.Dispatcher.ClientRuntime>-Klassen oder <xref:System.ServiceModel.Dispatcher.DispatchRuntime>-Klassen auf dem Client bzw. Server.  
  
-   Vorgangsverhalten: Diese ermöglichen das Anpassen von <xref:System.ServiceModel.Dispatcher.ClientOperation>-Klassen oder <xref:System.ServiceModel.Dispatcher.DispatchOperation>-Klassen auf dem Client bzw. Server.  
  
 Für den Zweck einer Objektpoolingerweiterung kann ein Endpunktverhalten oder ein Dienstverhalten erstellt werden. In diesem Beispiel wird ein Dienstverhalten verwendet, das die Objektpoolingfähigkeit auf alle Endpunkte des Diensts anwendet. Dienstverhaltensweisen werden durch Implementieren der <xref:System.ServiceModel.Description.IServiceBehavior>-Schnittstelle erstellt. Es gibt mehrere Möglichkeiten, ServiceModel auf die benutzerdefinierten Verhaltensweisen hinzuweisen:  
  
-   Verwenden eines benutzerdefinierten Attributs.  
  
-   Imperatives Hinzufügen zur Verhaltensauflistung der Dienstbeschreibung.  
  
-   Erweitern der Konfigurationsdatei.  
  
 In diesem Beispiel wird ein benutzerdefiniertes Attribut verwendet. Beim Erstellen von <xref:System.ServiceModel.ServiceHost> werden die in der Typdefinition des Diensts verwendeten Attribute untersucht, und die verfügbaren Verhalten werden der Verhaltensauflistung der Dienstbeschreibung hinzugefügt.  
  
 Die <xref:System.ServiceModel.Description.IServiceBehavior> Schnittstelle verfügt über drei Methoden: <xref:System.ServiceModel.Description.IServiceBehavior.Validate%2A> `,` <xref:System.ServiceModel.Description.IServiceBehavior.AddBindingParameters%2A> `,` und <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A>. Diese Methoden werden aufgerufen, indem Sie WCF bei der <xref:System.ServiceModel.ServiceHost> initialisiert wird. <xref:System.ServiceModel.Description.IServiceBehavior.Validate%2A?displayProperty=nameWithType> wird zuerst aufgerufen. So kann der Dienst auf Inkonsistenzen untersucht werden. <xref:System.ServiceModel.Description.IServiceBehavior.AddBindingParameters%2A?displayProperty=nameWithType> wird danach aufgerufen. Diese Methode ist nur in sehr komplexen Szenarios erforderlich. <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A?displayProperty=nameWithType> wird zuletzt aufgerufen und ist für das Konfigurieren der Laufzeit zuständig. Die folgenden Parameter werden in <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A?displayProperty=nameWithType> übergeben:  
  
-   `Description`: Dieser Parameter stellt die Dienstbeschreibung für den gesamten Dienst bereit. Dies kann verwendet werden, um Beschreibungsdaten über die Endpunkte, Verträge, Bindungen und andere Daten zu dem Dienst zu überprüfen.  
  
-   `ServiceHostBase`: Dieser Parameter stellt die <xref:System.ServiceModel.ServiceHostBase> bereit, die gerade initialisiert wird.  
  
 In der benutzerdefinierten <xref:System.ServiceModel.Description.IServiceBehavior>-Implementierung wird eine neue Instanz von `ObjectPoolInstanceProvider` instanziiert und der <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A>-Eigenschaft in jedem <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> zugewiesen, der <xref:System.ServiceModel.ServiceHostBase> angefügt ist.  
  
```  
public void ApplyDispatchBehavior(ServiceDescription description, ServiceHostBase serviceHostBase)  
{  
    if (enabled)  
    {  
        // Create an instance of the ObjectPoolInstanceProvider.  
        instanceProvider = new ObjectPoolInstanceProvider(description.ServiceType,  
        maxPoolSize, minPoolSize, creationTimeout);  
  
        // Assign our instance provider to Dispatch behavior in each   
        // endpoint.  
        foreach (ChannelDispatcherBase cdb in serviceHostBase.ChannelDispatchers)  
        {  
             ChannelDispatcher cd = cdb as ChannelDispatcher;  
             if (cd != null)  
             {  
                 foreach (EndpointDispatcher ed in cd.Endpoints)  
                 {  
                        ed.DispatchRuntime.InstanceProvider = instanceProvider;  
                 }  
             }  
         }  
     }  
}   
```  
  
 Neben einer <xref:System.ServiceModel.Description.IServiceBehavior>-Implementierung verfügt die `ObjectPoolingAttribute`-Klasse über mehrere Member zum Anpassen des Objektpools mithilfe der Attributargumente. Diese Member umfassen `MaxSize`, `MinSize`, `Enabled` und `CreationTimeout` für die Übereinstimmung mit dem von .NET Enterprise Services bereitgestellten Objektpooling-Featuresatz.  
  
 Objektpooling Verhalten kann jetzt an einen WCF-Dienst hinzugefügt werden, durch das Hinzufügen der dienstimplementierung mit dem neu erstellten, benutzerdefinierten `ObjectPooling` Attribut.  
  
```  
[ObjectPooling(MaxSize=1024, MinSize=10, CreationTimeout=30000]      
public class PoolService : IPoolService  
{  
  // …  
}  
```  
  
## <a name="hooking-activation-and-deactivation"></a>Aktivieren und Deaktivieren von Verknüpfungen  
 Das primäre Ziel des Objektpoolings ist das Optimieren von Objekten mit kurzer Lebensdauer und relativ aufwändiger Erstellung und Initialisierung. Bei der richtigen Verwendung kann daher eine erhebliche Leistungssteigerung erreicht werden. Da das Objekt aus dem Pool zurückgegeben wird, wird der Konstruktor nur einmal aufgerufen. Bei einigen Anwendungen ist jedoch eine gewisse Kontrolle erforderlich, damit sie die in einem einzigen Kontext verwendeten Ressourcen initialisieren und bereinigen können. Ein Objekt, das beispielsweise für eine Gruppe von Berechnungen verwendet wird, kann die privaten Felder zurücksetzen, bevor die nächste Berechnung verarbeitet wird. In Enterprise Services wurde diese Art der kontextspezifischen Initialisierung ermöglicht, indem der Objektentwickler die `Activate`-Methode und die `Deactivate`-Methode in der <xref:System.EnterpriseServices.ServicedComponent>-Basisklasse überschreiben konnte.  
  
 Der Objektpool ruft die `Activate`-Methode unmittelbar vor dem Zurückgeben des Objekts aus dem Pool auf. `Deactivate` wird aufgerufen, wenn das Objekt an den Pool zurückgegeben wird. Die <xref:System.EnterpriseServices.ServicedComponent>-Basisklasse verfügt außerdem über die `boolean`-Eigenschaft mit der Bezeichnung `CanBePooled`, mit der der Pool darüber benachrichtigt werden kann, ob das Objekt weiter gepoolt werden kann.  
  
 Im Beispiel wird eine öffentliche Schnittstelle (`IObjectControl`) deklariert, die über die oben genannten Member verfügt, um diese Funktionalität zu imitieren. Diese Schnittstelle wird dann von Dienstklassen implementiert, die die kontextspezifische Initialisierung bereitstellen sollen. Die <xref:System.ServiceModel.Dispatcher.IInstanceProvider>-Implementierung muss geändert werden, um diese Anforderungen zu erfüllen. Jetzt, jedes Mal Sie Abrufen eines Objekts durch Aufrufen der `GetInstance` -Methode, müssen Sie überprüfen, ob das Objekt implementiert `IObjectControl.` Wenn dies der Fall ist, müssen Sie Aufrufen der `Activate` Methode entsprechend.  
  
```  
if (obj is IObjectControl)  
{  
    ((IObjectControl)obj).Activate();  
}  
```  
  
 Beim Zurückgeben eines Objekts an den Pool ist eine Überprüfung für die `CanBePooled`-Eigenschaft erforderlich, bevor das Objekt erneut dem Pool hinzugefügt wird.  
  
```  
if (instance is IObjectControl)  
{  
    IObjectControl objectControl = (IObjectControl)instance;  
    objectControl.Deactivate();  
    if (objectControl.CanBePooled)  
    {  
       pool.Push(instance);  
    }  
}  
```  
  
 Da der Dienstentwickler entscheiden kann, ob ein Objekt gepoolt werden kann, kann die Objektanzahl im Pool zu einem bestimmten Zeitpunkt unter dem Mindestwert liegen. Sie müssen daher überprüfen, ob die Objektanzahl unter dem Mindestwert liegt, und die erforderliche Initialisierung in der Bereinigungsprozedur ausführen.  
  
```  
// Remove the surplus objects.  
if (pool.Count > minPoolSize)  
{  
  // Clean the surplus objects.  
}                      
else if (pool.Count < minPoolSize)  
{  
  // Reinitialize the missing objects.  
  while(pool.Count != minPoolSize)  
  {  
    pool.Push(CreateNewPoolObject());  
  }  
}  
```  
  
 Wenn Sie das Beispiel ausführen, werden die Anforderungen und Antworten für den Vorgang im Dienst- und Clientkonsolenfenster angezeigt. Drücken Sie die EINGABETASTE in den einzelnen Konsolenfenstern, um den Dienst und den Client zu schließen.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>So können Sie das Beispiel einrichten, erstellen und ausführen  
  
1.  Stellen Sie sicher, dass Sie ausgeführt haben die [Setupprozedur für die Windows Communication Foundation-Beispiele zum einmaligen](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Führen Sie zum Erstellen der Projektmappe die Anweisungen im [Erstellen der Windows Communication Foundation-Beispiele](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Um das Beispiel in einer einzelnen oder computerübergreifenden Konfiguration ausführen möchten, folgen Sie den Anweisungen [Ausführen der Windows Communication Foundation-Beispiele](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert. Suchen Sie nach dem folgenden Verzeichnis (Standardverzeichnis), bevor Sie fortfahren.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, fahren Sie mit [Windows Communication Foundation (WCF) und Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) aller Windows Communication Foundation (WCF) herunterladen und [!INCLUDE[wf1](../../../../includes/wf1-md.md)] Beispiele. Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Initialization`  
  
## <a name="see-also"></a>Siehe auch
