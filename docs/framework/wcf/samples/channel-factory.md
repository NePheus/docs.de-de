---
title: Kanalfactory
ms.date: 03/30/2017
ms.assetid: 09b53aa1-b13c-476c-a461-e82fcacd2a8b
ms.openlocfilehash: a528cc759ad550b21845dfd351d4e7808cfb6b56
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="channel-factory"></a>Kanalfactory
In diesem Beispiel wird veranschaulicht, wie eine Clientanwendung einen Kanal mit der <xref:System.ServiceModel.ChannelFactory>-Klasse und nicht mit einem generierten Client erstellen kann. Dieses Beispiel basiert auf der [Einstieg](../../../../docs/framework/wcf/samples/getting-started-sample.md) , implementiert einen rechnerdienst.  
  
> [!NOTE]
>  Die Setupprozedur und die Buildanweisungen für dieses Beispiel befinden sich am Ende dieses Themas.  
  
 In diesem Beispiel wird mithilfe der <xref:System.ServiceModel.ChannelFactory%601>-Klasse ein Kanal für einen Dienstendpunkt erstellt. Zum Erstellen eines Kanals zu einem Dienstendpunkt generieren Sie in der Regel eine Art von mit der [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) und erstellen Sie eine Instanz des generierten Typs. Sie können einen Kanal auch mithilfe der <xref:System.ServiceModel.ChannelFactory%601>-Klasse erstellen, wie in diesem Beispiel dargestellt. Der Dienst erstellt, indem der folgende Beispielcode ist identisch mit dem Dienst in der [Einstieg](../../../../docs/framework/wcf/samples/getting-started-sample.md).  
  
```csharp  
EndpointAddress address = new EndpointAddress("http://localhost/servicemodelsamples/service.svc");  
WSHttpBinding binding = new WSHttpBinding();  
ChannelFactory<ICalculator> factory = new   
                    ChannelFactory<ICalculator>(binding, address);  
ICalculator channel = factory.CreateChannel();  
```  
  
> [!IMPORTANT]
>  Wenn Sie dieses Beispiel in einem Szenario computerübergreifend ausführen, müssen Sie "localhost" im oben stehenden Code durch den vollqualifizierten Namen des Computers ersetzen, auf dem der Dienst ausgeführt wird. Im Beispiel wird die Endpunktadresse nicht in der Konfiguration festgelegt, daher muss dies im Code erfolgen.  
  
 Nach dem Erstellen des Kanals können Dienstvorgänge wie bei einem generierten Client aufgerufen werden.  
  
```csharp  
// Call the Add service operation.  
double value1 = 100.00D;  
double value2 = 15.99D;  
double result = channel.Add(value1, value2);  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
```  
  
 Zum Schließen des Kanals muss dieser zunächst in eine <xref:System.ServiceModel.IClientChannel>-Schnittstelle umgewandelt werden. Dies ist erforderlich, da der Kanal wie generiert in der Clientanwendung mit der `ICalculator`-Schnittstelle deklariert wird. Diese verfügt über Methoden wie `Add` und `Subtract`, nicht jedoch über `Close`. Die `Close`-Methode stammt aus der <xref:System.ServiceModel.ICommunicationObject>-Schnittstelle.  
  
```csharp  
// Close the channel.  
 ((IClientChannel)client).Close();  
```  
  
 Wenn Sie das Beispiel ausführen, werden die Anforderungen und Antworten für den Vorgang im Clientkonsolenfenster angezeigt. Drücken Sie im Clientfenster die EINGABETASTE, um die Clientanwendung zu schließen.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>So können Sie das Beispiel einrichten, erstellen und ausführen  
  
1.  Stellen Sie sicher, dass Sie ausgeführt haben die [Setupprozedur für die Windows Communication Foundation-Beispiele zum einmaligen](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Um die C#- oder Visual Basic .NET-Edition der Projektmappe zu erstellen, befolgen Sie die unter [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)aufgeführten Anweisungen. Beachten Sie, dass das Veröffentlichen von Metadaten in diesem Beispiel nicht aktiviert wird. Sie müssen zuerst das Veröffentlichen von Metadaten aktivieren, damit der Clienttyp in diesem Beispiel erneut generiert wird.  
  
3.  Um das Beispiel in einer einzelnen oder computerübergreifenden Konfiguration ausführen möchten, folgen Sie den Anweisungen [Ausführen der Windows Communication Foundation-Beispiele](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
### <a name="to-run-the-sample-cross-machine"></a>So führen Sie das Beispiel computerübergreifend aus  
  
1.  Ersetzen Sie "localhost" im folgenden Code durch den vollqualifizierten Namen des Computers, auf dem der Dienst ausgeführt wird.  
  
    ```csharp  
    EndpointAddress address = new EndpointAddress("http://localhost/servicemodelsamples/service.svc");  
    ```  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert. Suchen Sie nach dem folgenden Verzeichnis (Standardverzeichnis), bevor Sie fortfahren.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, fahren Sie mit [Windows Communication Foundation (WCF) und Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) aller Windows Communication Foundation (WCF) herunterladen und [!INCLUDE[wf1](../../../../includes/wf1-md.md)] Beispiele. Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Client\ChannelFactory`  
  
## <a name="see-also"></a>Siehe auch
