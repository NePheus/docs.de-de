---
title: 'Gewusst wie: Anzeigen eines Steuerelements im Dialogfeld "Toolboxelemente auswählen"'
ms.date: 03/30/2017
helpviewer_keywords:
- global assembly cache [Windows Forms], Choose Toolbox Items dialog box
- AssemblyFoldersEx [Windows Forms], Choose Toolbox Items dialog box
- controls [Windows Forms], display in Choose Toolbox Items dialog box
- assembly folder registration [Windows Forms], Choose Toolbox Items dialog box
- Choose Toolbox Items dialog box [Windows Forms], display control
ms.assetid: 01ef6eba-d044-40f0-951d-78eff7ebd9a9
ms.openlocfilehash: 7e452c3d3be131b891ee26555e3085fc31b04517
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-display-a-control-in-the-choose-toolbox-items-dialog-box"></a>Gewusst wie: Anzeigen eines Steuerelements im Dialogfeld "Toolboxelemente auswählen"
Beim Entwickeln und Verteilen von Steuerelementen, sollten Sie diese Kontrollen, die in angezeigt werden die **Toolboxelemente** im Dialogfeld angezeigt wird, wenn Sie mit der rechten Maustaste die **Toolbox** , und wählen Sie  **Wählen Sie Elemente aus**. Sie können das Steuerelement in diesem Dialogfeld angezeigt werden, mit der Registrierung-Prozedur "AssemblyFoldersEx" aktivieren.  
  
### <a name="to-display-your-control-in-the-choose-toolbox-items-dialog-box"></a>Zum Anzeigen des Steuerelements im Dialogfeld "Toolboxelemente auswählen"  
  
-   Die Steuerelementassembly im globalen Assemblycache zu installieren. Weitere Informationen finden Sie unter [Vorgehensweise: Installieren einer Assembly im globalen Assemblycache](../../../../docs/framework/app-domains/how-to-install-an-assembly-into-the-gac.md)  
  
     - oder -   
  
-   Registrieren Sie das Steuerelement und seine zugehörigen zur Entwurfszeit Assemblys mit der Registrierung-Prozedur "AssemblyFoldersEx" ein. "AssemblyFoldersEx" ist ein Registrierungsspeicherort, an dem Drittanbieter Pfade für jede Version des Frameworks speichern, die sie unterstützen. An diesem Registrierungsspeicherort Verweisassemblys suchen kann während der Entwurfszeit-Lösung suchen. Das Registrierungsskript kann die Steuerelemente angeben, in der Toolbox angezeigt werden sollen. Weitere Informationen finden Sie unter [Bereitstellen eines benutzerdefinierten Steuerelements und zur Entwurfszeit Assemblys (Visual Studio 2013)](http://msdn.microsoft.com/library/96158eb0-b691-4ae1-9e7b-3c65a1b798cb).  
  
## <a name="see-also"></a>Siehe auch  
 [Dialogfeld „Toolboxelemente auswählen“ (Visual Studio)](http://msdn.microsoft.com/library/bd07835f-18a8-433e-bccc-7141f65263bb)  
 [Bereitstellen eines benutzerdefinierten Steuerelements und zur Entwurfszeit Assemblys (Visual Studio 2013)](http://msdn.microsoft.com/library/96158eb0-b691-4ae1-9e7b-3c65a1b798cb)  
 [Entwickeln von Windows Forms-Steuerelementen zur Entwurfszeit](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)  
 [Gewusst wie: Installieren einer Assembly in den globalen Assemblycache](../../../../docs/framework/app-domains/how-to-install-an-assembly-into-the-gac.md)  
 [Exemplarische Vorgehensweise: Automatisches Füllen der Toolbox mit benutzerdefinierten Komponenten](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)
