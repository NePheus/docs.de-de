---
title: Lesen und Schreiben von XML-Schemata
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
ms.assetid: b5757c4a-ea59-467e-ac62-be2bfe24eb77
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b652adb27c3bb075fe86c09d7c9ab33511371279
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="reading-and-writing-xml-schemas"></a>Lesen und Schreiben von XML-Schemata
Mit der SOM-API (Schema Object Model) können XSD-Schemata (XML Schema Definition Language) aus Dateien und anderen Quellen gelesen und geschrieben werden. Außerdem können mithilfe der Klassen im <xref:System.Xml.Schema?displayProperty=nameWithType>-Namespace speicherintern XML-Schemata erstellt werden, die den Strukturen entsprechen, die in der XML-Schemaempfehlung des W3C (World Wide Web Consortium) festgelegt sind.  
  
## <a name="reading-and-writing-xml-schemas"></a>Lesen und Schreiben von XML-Schemata  
 Die <xref:System.Xml.Schema.XmlSchema>-Klasse stellt die <xref:System.Xml.Schema.XmlSchema.Read%2A>-Methode und die <xref:System.Xml.Schema.XmlSchema.Write%2A>-Methode bereit, mit denen XML-Schemata gelesen bzw. geschrieben werden. Mit der <xref:System.Xml.Schema.XmlSchema.Read%2A>-Methode wird ein <xref:System.Xml.Schema.XmlSchema>-Objekt zurückgegeben, das das XML-Schema darstellt, und einen optionalen <xref:System.Xml.Schema.ValidationEventHandler> als Parameter annimmt, um Schemavalidierungswarnungen und Fehler zu behandeln, die beim Lesen eines XML-Schemas auftreten.  
  
 Mit der <xref:System.Xml.Schema.XmlSchema.Write%2A>-Methode werden XML-Schemata in die Objekte <xref:System.IO.Stream>, <xref:System.IO.TextWriter> und <xref:System.Xml.XmlWriter> geschrieben, und ein optionales <xref:System.Xml.XmlNamespaceManager>-Objekt kann als Parameter angenommen werden. Mit einem <xref:System.Xml.XmlNamespaceManager> werden in einem XML-Schema gefundene Namespaces behandelt. Weitere Informationen zur <xref:System.Xml.XmlNamespaceManager>-Klasse finden Sie unter [Verwalten von Namespaces in einem XML-Dokument](../../../../docs/standard/data/xml/managing-namespaces-in-an-xml-document.md).  
  
 Im folgenden Codebeispiel werden das Lesen und Schreiben von XML-Schemata in eine bzw. aus einer Datei veranschaulicht. Im Codebeispiel wird die Datei `example.xsd` verwendet und mithilfe der <xref:System.Xml.Schema.XmlSchema>`static`-Methode in ein <xref:System.Xml.Schema.XmlSchema.Read%2A>-Objekt eingelesen. Anschließend wird die Datei in die Konsole und eine neue Datei `new.xsd` geschrieben. Im Codebeispiel wird außerdem ein <xref:System.Xml.Schema.ValidationEventHandler> als Parameter für die `static`<xref:System.Xml.Schema.XmlSchema.Read%2A>-Methode bereitgestellt, mit dem alle Schemavalidierungswarnungen und Fehler behandelt werden, die beim Lesen des XML-Schemas auftreten. Wenn der <xref:System.Xml.Schema.ValidationEventHandler> nicht angegeben ist (bzw. `null` ist), werden keine Warnungen oder Fehler ausgegeben.  
  
 [!code-cpp[XmlSchemaReadWriteExample#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaReadWriteExample/CPP/XmlSchemaReadWriteExample.cpp#1)]
 [!code-csharp[XmlSchemaReadWriteExample#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaReadWriteExample/CS/XmlSchemaReadWriteExample.cs#1)]
 [!code-vb[XmlSchemaReadWriteExample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaReadWriteExample/VB/XmlSchemaReadWriteExample.vb#1)]  
  
 In diesem Beispiel wird `example.xsd` als Eingabe verwendet.  
  
```xml  
<?xml version="1.0"?>  
<xs:schema id="play" targetNamespace="http://tempuri.org/play.xsd" elementFormDefault="qualified" xmlns="http://tempuri.org/play.xsd" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    <xs:element name='myShoeSize'>  
        <xs:complexType>  
            <xs:simpleContent>  
                <xs:extension base='xs:decimal'>  
                    <xs:attribute name='sizing' type='xs:string' />  
                </xs:extension>  
            </xs:simpleContent>  
        </xs:complexType>  
    </xs:element>  
</xs:schema>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über das XML-Schemaobjektmodell (SOM)](../../../../docs/standard/data/xml/xml-schema-object-model-overview.md)  
 [Erstellen von XML-Schemas](../../../../docs/standard/data/xml/building-xml-schemas.md)  
 [Durchlaufen von XML-Schemas](../../../../docs/standard/data/xml/traversing-xml-schemas.md)  
 [Bearbeiten von XML-Schemas](../../../../docs/standard/data/xml/editing-xml-schemas.md)  
 [Einfügen oder Importieren von XML-Schemas](../../../../docs/standard/data/xml/including-or-importing-xml-schemas.md)  
 [„XmlSchemaSet“ zur Kompilierung von Schemas](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)  
 [Post-Schema-Compilation-Infoset](../../../../docs/standard/data/xml/post-schema-compilation-infoset.md)  
 [Managing Namespaces in an XML Document (Verwalten von Namespaces in einem XML-Dokument)](../../../../docs/standard/data/xml/managing-namespaces-in-an-xml-document.md)
