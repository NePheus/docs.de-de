---
title: Konfigurieren der Serialisierung in einem Workflowdienst
ms.date: 03/30/2017
ms.assetid: aa70b290-a2ee-4c3c-90ea-d0a7665096ae
ms.openlocfilehash: 74d9a812b9e0cd51a401fa3526c947d52413807a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="configuring-serialization-in-a-workflow-service"></a>Konfigurieren der Serialisierung in einem Workflowdienst
Workflowdienste sind Windows Communication Foundation (WCF)-Dienste und daher keine verwenden Sie entweder die <xref:System.Runtime.Serialization.DataContractSerializer> (Standard) oder die <xref:System.Xml.Serialization.XmlSerializer>. Beim Schreiben von Nicht-Workflowdiensten wird der Typ des zu verwendenden Serialisierungsprogramms im Dienstvertrag oder Vorgangsvertrag angegeben. Beim Erstellen von WCF-Workflowdienste keinen diese Verträge im Code angeben, aber sie werden vielmehr zur Laufzeit generiert, durch vertragsrückschluss. Weitere Informationen zu vertragsrückschluss, finden Sie unter [Verwenden von Verträgen im Workflow](../../../../docs/framework/wcf/feature-details/using-contracts-in-workflow.md).  Das Serialisierungsprogramm wird mithilfe der <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A>-Eigenschaft angegeben. Diese kann im Designer festgelegt werden, wie in der folgenden Abbildung dargestellt.  
  
 ![Festlegen des Serialisierungsprogramms](../../../../docs/framework/wcf/feature-details/media/settingserialzier.png "SettingSerialzier")  
  
 Das Serialisierungsprogramm kann auch im Code festgelegt werden, wie im folgenden Beispiel gezeigt.  
  
```  
Receive approveExpense = new Receive  
            {  
                OperationName = "ApproveExpense",  
                CanCreateInstance = true,  
                ServiceContractName = "FinanceService",  
                SerializerOption = SerializerOption.DataContractSerializer,  
                Content = ReceiveContent.Create(new OutArgument<Expense>(expense))  
            };  
```  
  
 Bekannte Typen können auch für Workflowdienste angegeben werden. Weitere Informationen über bekannte Typen finden Sie unter [Datenvertragstypen bezeichnet](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md). Bekannte Typen können im Designer oder im Code angegeben werden. Um bekannte Typen im Designer anzugeben, klicken Sie im Eigenschaftenfenster für eine <xref:System.ServiceModel.Activities.Receive>-Aktivität neben der KnownTypes-Eigenschaft auf die Schaltfläche mit den Auslassungspunkten, wie in der folgenden Abbildung gezeigt.  
  
 ![KnownTypes-Eigenschaft](../../../../docs/framework/wcf/feature-details/media/knowntypes.png "bekannte Typen")  
  
 Dadurch wird der Typauflistungs-Editor angezeigt, mit dem Sie bekannte Typen suchen und angeben können.  
  
 ![Hinzufügen von bekannten Typen](../../../../docs/framework/wcf/feature-details/media/typecollectionseditor.gif "TypeCollectionsEditor")  
  
 Klicken Sie auf die **hinzufügen, geben Sie neue** verknüpfen und mithilfe der Dropdownliste auswählen oder einen Typ zu suchen, das der Auflistung bekannter Typen hinzugefügt. Verwenden Sie die <xref:System.ServiceModel.Activities.Receive.KnownTypes%2A>-Eigenschaft, um bekannte Typen im Code anzugeben, wie im folgenden Beispiel gezeigt.  
  
```  
Receive approveExpense = new Receive  
            {  
                OperationName = "ApproveExpense",  
                CanCreateInstance = true,  
                ServiceContractName = "FinanceService",  
                SerializerOption = SerializerOption.DataContractSerializer,  
                Content = ReceiveContent.Create(new OutArgument<Expense>(expense))  
            };  
            approveExpense.KnownTypes.Add(typeof(Travel));  
            approveExpense.KnownTypes.Add(typeof(Meal));  
```  
  
 Um ein vollständiges Codebeispiel zeigt, wie Serialisierung, die für einen Workflowdienst konfigurieren finden Sie unter finden Sie unter [Formatieren von Meldungen in Workflowdiensten](../../../../docs/framework/windows-workflow-foundation/samples/formatting-messages-in-workflow-services.md).
