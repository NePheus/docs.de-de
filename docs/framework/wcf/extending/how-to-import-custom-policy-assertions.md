---
title: 'Vorgehensweise: Importieren von benutzerdefinierten Richtlinienassertionen'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1f41d787-accb-4a10-bfc6-a807671d1581
ms.openlocfilehash: b6155296e264bb3ae90aac2ee6b83797e632962e
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-import-custom-policy-assertions"></a>Vorgehensweise: Importieren von benutzerdefinierten Richtlinienassertionen
Richtlinienassertionen beschreiben die Funktionen und Anforderungen eines Dienstendpunkts.  Clientanwendungen können Richtlinienassertionen in Dienstmetadaten nutzen, um die Clientbindung zu konfigurieren oder den Dienstvertrag für einen Dienstendpunkt anzupassen.  
  
 Benutzerdefinierte Richtlinienassertionen werden importiert, indem die <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=nameWithType>-Schnittstelle implementiert und das Objekt in das Metadatensystem übergeben wird oder durch die Registrierung des Implementierungstyps in Ihrer Anwendungskonfigurationsdatei.  Implementierungen der <xref:System.ServiceModel.Description.IPolicyImportExtension>-Schnittstelle müssen den Standardkonstruktor bereitstellen.  
  
### <a name="to-import-custom-policy-assertions"></a>So importieren Sie benutzerdefinierte Richtlinienassertionen  
  
1.  Implementieren Sie die <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=nameWithType>-Schnittstelle auf einer Klasse. Anweisungen hierzu finden Sie in den folgenden Verfahren.  
  
2.  Fügen Sie das benutzerdefinierte Richtlinienimportprogramm durch eines der folgenden Verfahren ein:  
  
3.  Verwenden einer Konfigurationsdatei. Anweisungen hierzu finden Sie in den folgenden Verfahren.  
  
4.  Mithilfe einer Konfigurationsdatei mit [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md). Anweisungen hierzu finden Sie in den folgenden Verfahren.  
  
5.  Programmgesteuertes Einfügen des Richtlinienimportprogramms. Anweisungen hierzu finden Sie in den folgenden Verfahren.  
  
### <a name="to-implement-the-systemservicemodeldescriptionipolicyimportextension-interface-on-any-class"></a>So implementieren Sie die System.ServiceModel.Description.IPolicyImportExtension-Schnittstelle auf einer beliebigen Klasse  
  
1.  Suchen Sie für jedes Richtliniensubjekt, an dem Sie interessiert sind, in der <xref:System.ServiceModel.Description.IPolicyImportExtension.ImportPolicy%2A?displayProperty=nameWithType>-Methode die Richtlinienassertionen, die Sie importieren möchten, indem Sie die entsprechende Methode auf dem zur Methode übergebenen <xref:System.ServiceModel.Description.PolicyConversionContext?displayProperty=nameWithType>-Objekt aufrufen (abhängig vom Umfang der gewünschten Assertion). Im folgenden Codebeispiel wird veranschaulicht, wie die <xref:System.ServiceModel.Description.PolicyAssertionCollection.Remove%2A?displayProperty=nameWithType>-Methode verwendet wird, um die benutzerdefinierte Richtlinienassertion ausfindig zu machen und diese in einem Schritt aus der Sammlung zu entfernen. Wenn Sie die Entfernen-Methode verwenden, um die Assertion ausfindig zu machen und zu entfernen, müssen Sie Schritt 4 nicht durchführen.  
  
     [!code-csharp[CustomPolicySample#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/policyimporter.cs#9)]
     [!code-vb[CustomPolicySample#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/policyimporter.vb#9)]  
  
2.  Verarbeiten Sie die Richtlinienassertionen. Beachten Sie, dass das Richtliniensystem keine geschachtelten Richtlinien und `wsp:optional` normalisiert. Sie müssen diese Konstrukte in der Richtlinienimport-Erweiterungsimplementierung verarbeiten.  
  
3.  Nehmen Sie die Anpassung an der Bindung oder am Vertrag vor, die bzw. der die von der Richtlinienassertion festgelegte Funktion oder Anforderung erfüllt. In der Regel geben Assertionen an, dass eine Bindung eine besondere Konfiguration oder ein bestimmtes Bindungselement erfordert. Nehmen Sie diese Änderungen vor, indem Sie auf die <xref:System.ServiceModel.Description.PolicyConversionContext.BindingElements%2A?displayProperty=nameWithType>-Eigenschaft zugreifen. Andere Assertionen erfordern, dass Sie den Vertrag ändern.  Sie können über die <xref:System.ServiceModel.Description.PolicyConversionContext.Contract%2A?displayProperty=nameWithType>-Eigenschaft auf den Vertrag zugreifen und diesen ändern.  Beachten Sie, dass Ihr Richtlinienimportprogramm möglicherweise mehrere Male für dieselbe Bindung und für denselben Vertrag, aber für unterschiedliche Richtlinienalternativen aufgerufen wird, wenn der Import einer Richtlinienalternative fehlschlägt. Der Code sollte diesem Verhalten gegenüber flexibel sein.  
  
4.  Entfernen Sie die die benutzerdefinierte Richtlinienassertion aus der Assertionsauflistung. Wenn Sie die Assertion nicht entfernen, wird Windows Communication Foundation (WCF) davon ausgegangen, dass der Richtlinienimport nicht erfolgreich war und die zugeordnete Bindung nicht importiert. Wenn Sie die <xref:System.ServiceModel.Description.PolicyAssertionCollection.Remove%2A?displayProperty=nameWithType>-Methode verwendet haben, um die benutzerdefinierte Assertion ausfindig zu machen und diese in einem Schritt aus der Auflistung zu entfernen, müssen Sie diesen Schritt nicht durchführen.  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-using-a-configuration-file"></a>So fügen Sie das benutzerdefinierte Richtlinienimportprogramm mit einer Konfigurationsdatei ins Metadatensystem ein  
  
1.  Fügen Sie den Importer-Tool, das `<extensions>` Element innerhalb der [ \<PolicyImporters >](../../../../docs/framework/configure-apps/file-schema/wcf/policyimporters.md) Element in der Clientkonfigurationsdatei.  
  
     [!code-xml[CustomPolicySample#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/client.exe.config#7)]   
  
2.  Verwenden Sie in der Clientanwendung <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=nameWithType> oder <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> zur Auflösung der Metadaten. Das Importprogramm wird daraufhin automatisch ausgelöst.  
  
     [!code-csharp[CustomPolicySample#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/client.cs#10)]
     [!code-vb[CustomPolicySample#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/client.vb#10)]  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-using-svcutilexe"></a>So fügen Sie das benutzerdefinierte Richtlinienimportprogramm mithilfe der Datei Svcutil.exe ins Metadatensystem ein  
  
1.  Fügen Sie den Importer-Tool, das `<extensions>` Element innerhalb der [ \<PolicyImporters >](../../../../docs/framework/configure-apps/file-schema/wcf/policyimporters.md) Element in der Konfigurationsdatei "svcutil.exe.config". Über die Option `/svcutilConfig` können Sie Svcutil.exe darüber hinaus dazu bringen, Typen von Richtlinienprogrammen zu laden, die in einer anderen Konfigurationsdatei gespeichert sind.  
  
2.  Verwendung [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) zum Importieren von Metadaten und den Importer-Tool werden automatisch aufgerufen.  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-programmatically"></a>So fügen Sie das benutzerdefinierte Richtlinienimportprogramm programmgesteuert ins Metadatensystem ein  
  
1.  Fügen Sie vor dem Import der Metadaten das Importprogramm zur <xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A?displayProperty=nameWithType>-Eigenschaft hinzu (beispielsweise, wenn Sie <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> verwenden).  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=nameWithType>  
 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType>  
 <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=nameWithType>  
 [Erweitern des Metadatensystems](../../../../docs/framework/wcf/extending/extending-the-metadata-system.md)
