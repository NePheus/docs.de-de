---
title: For-Aktivität
ms.date: 03/30/2017
ms.assetid: 2ea751b4-36f0-48aa-a115-70a2ab89f6d8
ms.openlocfilehash: c79f295e7880f845c606a55f9c56ad65350f9c52
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="for-activity"></a>For-Aktivität
Im For-Beispiel wird veranschaulicht, wie eine benutzerdefinierte Aktivität erstellt wird, die von <xref:System.Activities.NativeActivity> erbt, und wie diese in einem Workflow verwendet wird, um ein Beispiel mit realen Bedingungen auszuführen. Die benutzerdefinierte Aktivität in diesem Beispiel funktioniert wie die `for`-Anweisung in C#. T  
  
 Die benutzerdefinierte `For`-Aktivität weist die Eigenschaften `InitAction`, `IterationAction`, `Condition` und `Body` auf, die jeweils der Initialisierungsanweisung, der iterativen Anweisung, der Fortsetzungsbedingung und der Textanweisung in der standardmäßigen `For`-Anweisung in C# entsprechen.  
  
 In der folgenden Tabelle sind die im Beispiel verwendeten Schlüsseldateien beschrieben.  
  
|Datei|Beschreibung|  
|----------|-----------------|  
|For.cs|Klassendefinition für die benutzerdefinierte `For`-Aktivität, die durch Erweiterung der <xref:System.Activities.NativeActivity>-Klasse die Funktionalität der `For`-Anweisung in C# bereitstellt.|  
|Program.cs|Eine Clientanwendung, die unter Verwendung der benutzerdefinierten `For`-Aktivität grundlegende iterative Verarbeitungsschritte für eine Auflistung ausführt.|  
  
> [!NOTE]
>  Stellen Sie bei Verwendung der benutzerdefinierten `For`-Aktivität sicher, dass die `Condition`-Eigenschaft festgelegt ist. Andernfalls kann eine Endlosschleife auftreten.  
  
## <a name="demonstrates"></a>Veranschaulicht  
 Erstellen einer benutzerdefinierten Aktivität, die von <xref:System.Activities.NativeActivity> erbt.  
  
## <a name="discussion"></a>Diskussion  
 In der folgenden Tabelle werden die Eigenschaften der Aktivität in diesem Beispiel beschrieben.  
  
 InitAction  
 Initialisierungsanweisung  
  
 IterationAction  
 Iterative Anweisung  
  
 Bedingung  
 Fortsetzungsanweisung  
  
 Body  
 Textanweisung  
  
 Die Aktivität erbt von <xref:System.Activities.NativeActivity>, um mittels einer der `ScheduleActivity`-Methoden von <xref:System.Activities.NativeActivityContext> Zugriff auf Laufzeitfunktionen zu erhalten, z. B. zur Planung zusätzlicher auszuführender Aktivitäten.  
  
#### <a name="to-use-this-sample"></a>So verwenden Sie dieses Beispiel  
  
1.  Öffnen Sie in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] die Projektmappendatei "For.sln".  
  
2.  Erstellen Sie die Projektmappe, indem Sie STRG+UMSCHALT+B drücken.  
  
3.  Drücken Sie F5, um die Projektmappe auszuführen.  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert. Suchen Sie nach dem folgenden Verzeichnis (Standardverzeichnis), bevor Sie fortfahren.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, fahren Sie mit [Windows Communication Foundation (WCF) und Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) aller Windows Communication Foundation (WCF) herunterladen und [!INCLUDE[wf1](../../../../includes/wf1-md.md)] Beispiele. Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\For`