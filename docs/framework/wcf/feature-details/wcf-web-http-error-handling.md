---
title: WCF-Web-HTTP-Fehlerbehandlung
ms.date: 03/30/2017
ms.assetid: 02891563-0fce-4c32-84dc-d794b1a5c040
ms.openlocfilehash: 228f8cdbe5ddde63f2b6afd82a27055f2241e058
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="wcf-web-http-error-handling"></a>WCF-Web-HTTP-Fehlerbehandlung
Windows Communication Foundation (WCF)-Web-HTTP-Fehlerbehandlung können Sie zur Rückgabe von Fehlern von WCF-Web-HTTP-Diensten, die einen HTTP-Statuscode und Zurückgeben von Fehlerdetails, die mit dem gleichen Format wie des Vorgangs (z. B. XML oder JSON).  
  
## <a name="wcf-web-http-error-handling"></a>WCF-Web-HTTP-Fehlerbehandlung  
 Die <xref:System.ServiceModel.Web.WebFaultException>-Klasse definiert einen Konstruktor, der Ihnen das Angeben eines HTTP-Statuscodes ermöglicht. Dieser Statuscode wird dann an den Client zurückgegeben. Dies ist eine generische Version der <xref:System.ServiceModel.Web.WebFaultException>-Klasse. Mit <xref:System.ServiceModel.Web.WebFaultException%601> können Sie einen benutzerdefinierten Typ zurückgeben, der Informationen zum aufgetretenen Fehler enthält. Dieses benutzerdefinierte Objekt wird in dem Format serialisiert, das vom Vorgang angegeben und an den Client zurückgegeben wird. Im folgenden Beispiel wird gezeigt, wie Sie einen HTTP-Statuscode zurückgeben.  
  
```  
Public string Operation1()  
{   // Operation logic  
   // ...  
   Throw new WebFaultException(HttpStatusCode.Forbidden);  
}  
```  
  
 Im folgenden Beispiel wird gezeigt, wie Sie einen HTTP-Statuscode und zusätzliche Informationen in einem benutzerdefinierten Typ zurückgeben. `MyErrorDetail` ist ein benutzerdefinierter Typ, der zusätzliche Informationen zum aufgetretenen Fehler enthält.  
  
```  
Public string Operation2()  
   // Operation logic  
   // ...   MyErrorDetail detail = new MyErrorDetail  
   {  
      Message = "Error Message",  
      ErrorCode = 123,  
   }  
   throw new WebFaultException<MyErrorDetail>(detail, HttpStatusCode.Forbidden);  
}  
```  
  
 Der oben angegebene Code gibt eine HTTP-Antwort mit dem unzulässigen Statuscode und einem Text zurück, in der eine Instanz des `MyErrorDetails`-Objekts enthalten ist. Zum Bestimmen des Formats des `MyErrorDetails`-Objekts werden folgende Komponenten herangezogen:  
  
-   Der Wert des `ResponseFormat`-Parameters des <xref:System.ServiceModel.Web.WebGetAttribute>- oder <xref:System.ServiceModel.Web.WebInvokeAttribute>-Attributs, das für den Dienstvorgang angegeben wurde.  
  
-   Der Wert von <xref:System.ServiceModel.Description.WebHttpBehavior.AutomaticFormatSelectionEnabled%2A>.  
  
-   Der Wert der <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A>-Eigenschaft, indem auf <xref:System.ServiceModel.Web.OutgoingWebResponseContext> zugegriffen wird.  
  
 Weitere Informationen darüber, wie diese Werte beeinflussen die Formatierung des Vorgangs finden Sie unter [WCF Web-HTTP-Formatierung](../../../../docs/framework/wcf/feature-details/wcf-web-http-formatting.md).  
  
 <xref:System.ServiceModel.Web.WebFaultException> ist ein <xref:System.ServiceModel.FaultException>-Objekt und kann daher als Fehlerausnahme-Programmiermodell für Dienste verwendet werden, die SOAP-Endpunkte sowie Web-HTTP-Endpunkte verfügbar machen.  
  
## <a name="see-also"></a>Siehe auch  
 [WCF-Web-HTTP-Programmiermodell](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)  
 [WCF-Web-HTTP-Formatierung](../../../../docs/framework/wcf/feature-details/wcf-web-http-formatting.md)  
 [Definieren und Angeben von Fehlern](../../../../docs/framework/wcf/defining-and-specifying-faults.md)  
 [Behandeln von Ausnahmen und Fehlern](../../../../docs/framework/wcf/extending/handling-exceptions-and-faults.md)  
 [Senden und Empfangen von Fehlern](../../../../docs/framework/wcf/sending-and-receiving-faults.md)
