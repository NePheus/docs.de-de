---
title: 'Exemplarische Vorgehensweise: Kopieren und Einfügen eines ElementHost-Steuerelements in separate Windows Forms'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, content copying and pasting
- interoperability [WPF]
- ElementHost control [Windows Forms], copying and pasting at design time
- WPF user control [Windows Forms], hosting in Windows Forms
ms.assetid: 6e81bb13-577c-46c3-a1cf-8d15969fb83e
ms.openlocfilehash: 1cce981e4cb04ab6ed6ed41e0afac0121b242761
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="walkthrough-copying-and-pasting-an-elementhost-control-into-separate-windows-forms"></a>Exemplarische Vorgehensweise: Kopieren und Einfügen eines ElementHost-Steuerelements in separate Windows Forms
In dieser exemplarischen Vorgehensweise wird veranschaulicht, wie ein WPF-Steuerelement (Windows Presentation Foundation) von einem Windows Form-Objekt in ein anderes kopiert wird.  
  
 Im Verlauf dieser exemplarischen Vorgehensweise führen Sie die folgenden Aufgaben aus:  
  
-   Erstellen des Projekts  
  
-   Kopieren eines WPF-Steuerelements  
  
> [!NOTE]
>  Je nach den aktiven Einstellungen oder der Version unterscheiden sich die Dialogfelder und Menübefehle auf Ihrem Bildschirm möglicherweise von den in der Hilfe beschriebenen. Klicken Sie im Menü **Extras** auf **Einstellungen importieren und exportieren** , um die Einstellungen zu ändern. Weitere Informationen finden Sie unter [Anpassen der Entwicklungseinstellungen in Visual Studio](http://msdn.microsoft.com/library/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 Zum Durchführen dieser exemplarischen Vorgehensweise benötigen Sie die folgenden Komponenten:  
  
-   [!INCLUDE[vs_dev11_long](../../../../includes/vs-dev11-long-md.md)].  
  
## <a name="creating-the-project"></a>Erstellen des Projekts  
 Zunächst muss das Windows Forms-Projekt erstellt werden.  
  
> [!NOTE]
>  Beim Hosten von WPF-Inhalt werden nur C#- und Visual Basic-Projekte unterstützt.  
  
#### <a name="to-create-the-project"></a>So erstellen Sie das Projekt  
  
-   Erstellen Sie ein neues Windows Forms-Anwendungsprojekt in Visual Basic oder Visual c# mit dem Namen `CopyElementHost`.  
  
## <a name="copying-a-wpf-control"></a>Kopieren eines WPF-Steuerelements  
 Nachdem Sie dem Projekt ein WPF-Steuerelement hinzugefügt haben, können Sie es auf andere Formulare im Projekt kopieren.  
  
#### <a name="to-copy-a-wpf-control"></a>So kopieren Sie ein WPF-Steuerelement  
  
1.  Fügen Sie der Projektmappe ein neues WPF-<xref:System.Windows.Controls.UserControl>-Projekt hinzu. Verwenden Sie den Standardnamen (`UserControl1.xaml`) für den Steuerelementtyp. Weitere Informationen finden Sie unter [Exemplarische Vorgehensweise: Erstellen neuen WPF-Inhalts in Windows Forms zur Entwurfszeit](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md).  
  
2.  Erstellen Sie das Projekt.  
  
3.  Öffnen Sie `Form1` im Windows Forms-Designer.  
  
4.  Aus der **Toolbox**, ziehen Sie eine Instanz des `UserControl1` auf das Formular.  
  
     Eine Instanz von `UserControl1` wird in einem neuen <xref:System.Windows.Forms.Integration.ElementHost>-Steuerelement namens `elementHost1` gehostet.  
  
5.  Während `elementHost1` ausgewählt ist, drücken Sie STRG + C, um das Steuerelement in die Zwischenablage zu kopieren.  
  
6.  Fügen Sie dem Projekt ein neues Windows Form-Objekt hinzu. Verwenden Sie den Standardnamen für den Formulartyp, `Form2`.  
  
7.  Während `Form2` im Windows Forms-Designer geöffnet ist, drücken Sie STRG+V, um eine Kopie von `elementHost1` auf dem Formular einzufügen.  
  
     Das kopierte Steuerelement erhält ebenfalls den Namen `elementHost1`, da es ein privates Feld der `Form2`-Klasse ist. Es gibt keinen Namenskonflikt mit `elementHost1` in der `Form1`-Klasse.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.Forms.Integration.ElementHost>  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>  
 [Migration und Interoperabilität](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)  
 [Verwenden von WPF-Steuerelementen](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)  
 [WPF-Designer](http://msdn.microsoft.com/library/c6c65214-8411-4e16-b254-163ed4099c26)
