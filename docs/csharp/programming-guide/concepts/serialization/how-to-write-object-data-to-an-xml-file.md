---
title: 'Vorgehensweise: Schreiben von Objektdaten in eine XML-Datei (C#)'
ms.date: 07/20/2015
ms.assetid: 7681eb98-703d-4005-a369-26a7bca0f894
ms.openlocfilehash: 1c8bfd00452cee63456bc3bf64ccf4a0c61aa06e
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-write-object-data-to-an-xml-file-c"></a>Vorgehensweise: Schreiben von Objektdaten in eine XML-Datei (C#)
Dieses Beispiel verwendet die <xref:System.Xml.Serialization.XmlSerializer>-Klasse, um das Objekt aus einer Klasse in eine XML-Datei zu schreiben.  
  
## <a name="example"></a>Beispiel  
  
```csharp  
public class XMLWrite  
{  
  
   static void Main(string[] args)  
    {  
        WriteXML();  
    }  
  
    public class Book  
    {  
        public String title;   
    }  
  
    public static void WriteXML()  
    {  
        Book overview = new Book();  
        overview.title = "Serialization Overview";  
        System.Xml.Serialization.XmlSerializer writer =   
            new System.Xml.Serialization.XmlSerializer(typeof(Book));  
  
        var path = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments) + "//SerializationOverview.xml";  
        System.IO.FileStream file = System.IO.File.Create(path);  
  
        writer.Serialize(file, overview);  
        file.Close();  
    }  
}  
```  
  
## <a name="compiling-the-code"></a>Kompilieren des Codes  
 Die Klasse muss über einen öffentlichen Konstruktor ohne Parameter verfügen.  
  
## <a name="robust-programming"></a>Stabile Programmierung  
 Die folgenden Bedingungen können einen Ausnahmefehler verursachen:  
  
-   Die zu serialisierende Klasse verfügt nicht über einen öffentlichen, parameterlosen Konstruktor.  
  
-   Die Datei ist bereits vorhanden und schreibgeschützt (<xref:System.IO.IOException>).  
  
-   Der Pfad ist zu lang (<xref:System.IO.PathTooLongException>).  
  
-   Der Datenträger ist voll (<xref:System.IO.IOException>).  
  
## <a name="net-framework-security"></a>.NET Framework-Sicherheit  
 Mit diesem Beispiel wird eine neue Datei erstellt, wenn diese noch nicht vorhanden ist. Wenn eine Anwendung eine Datei erstellen muss, benötigt sie eine `Create`-Berechtigung für den Ordner. Wenn die Datei bereits vorhanden ist, benötigt die Anwendung lediglich die Berechtigung für den `Write`-Zugriff, also eine geringere Berechtigung. Aus Sicherheitsgründen sollte die Datei nach Möglichkeit erst im Verlauf der Bereitstellung erstellt werden. Außerdem sollte nur die `Read`-Berechtigung für eine einzelne Datei erteilt werden (anstatt `Create`-Berechtigungen für den gesamten Ordner zu gewähren).  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.IO.StreamWriter>  
 [How to: Read Object Data from an XML File (C#)](../../../../csharp/programming-guide/concepts/serialization/how-to-read-object-data-from-an-xml-file.md) (Vorgehensweise: Lesen von Objektdaten aus einer XML-Datei (C#))  
 [Serialisierung (C#)](../../../../csharp/programming-guide/concepts/serialization/index.md)
