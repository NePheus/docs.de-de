---
title: ContextMenu-Stile und -Vorlagen
ms.date: 03/30/2017
helpviewer_keywords:
- templates [WPF], ContextMenu
- parts [WPF], ContextMenu
- ContextMenu [WPF], styles and templates
- styles [WPF], ContextMenu
- ControlTemplate [WPF], ContextMenu
- states [WPF], ContextMenu
ms.assetid: 342d1f17-c406-4f94-8f55-867c5f3ea511
ms.openlocfilehash: 4208f8cf197849876a100ab8c799ef04331a3e0a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="contextmenu-styles-and-templates"></a>ContextMenu-Stile und -Vorlagen
In diesem Thema wird beschrieben, die Stile und Vorlagen für die <xref:System.Windows.Controls.ContextMenu> Steuerelement. Sie können den Standardwert ändern <xref:System.Windows.Controls.ControlTemplate> auf dem Steuerelement ein einzigartiges aussehen zu verleihen. Weitere Informationen finden Sie unter [Anpassen der Darstellung eines vorhandenen Steuerelements durch Erstellen einer ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
## <a name="contextmenu-parts"></a>ContextMenu-Teile  
 Die <xref:System.Windows.Controls.ContextMenu> Steuerelement enthält keine benannten Teile.  
  
 Beim Erstellen einer <xref:System.Windows.Controls.ControlTemplate> für eine <xref:System.Windows.Controls.ContextMenu>, Ihrer Vorlage enthalten möglicherweise eine <xref:System.Windows.Controls.ItemsPresenter> innerhalb einer <xref:System.Windows.Controls.ScrollViewer>. (Die <xref:System.Windows.Controls.ItemsPresenter> wird jedes Element in der <xref:System.Windows.Controls.ContextMenu>; das <xref:System.Windows.Controls.ScrollViewer> Bildlauf im Steuerelement aktiviert).  Wenn die <xref:System.Windows.Controls.ItemsPresenter> ist kein direkte untergeordnetes Element von der <xref:System.Windows.Controls.ScrollViewer>, geben Sie die <xref:System.Windows.Controls.ItemsPresenter> den Namen `ItemsPresenter`.  
  
## <a name="contextmenu-states"></a>ContextMenu-Zustände  
 Die folgende Tabelle enthält die visueller Zustände für die <xref:System.Windows.Controls.ContextMenu> Steuerelement.  
  
|VisualState-Name|VisualStateGroup-Name|Beschreibung|  
|-|-|-|  
|Gültig|ValidationStates|Das Steuerelement verwendet die <xref:System.Windows.Controls.Validation> Klasse und die <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> angefügte Eigenschaft `false`.|  
|InvalidFocused|ValidationStates|Die <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> angefügte Eigenschaft `true` weist das Steuerelement den Fokus hat.|  
|InvalidUnfocused|ValidationStates|Die <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> angefügte Eigenschaft `true` hat das Steuerelement verfügt nicht über den Fokus.|  
  
## <a name="contextmenu-controltemplate-example"></a>ContextMenu-ControlTemplate-Beispiel  
 Das folgende Beispiel zeigt, wie Sie definieren eine <xref:System.Windows.Controls.ControlTemplate> für die <xref:System.Windows.Controls.ContextMenu> Steuerelement.  
  
 [!code-xaml[ControlTemplateExamples#ContextMenu](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/menu.xaml#contextmenu)]  
  
 Die <xref:System.Windows.Controls.ControlTemplate> verwendet die folgenden Ressourcen.  
  
 [!code-xaml[ControlTemplateExamples#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 Das vollständige Beispiel finden Sie unter [Beispiel zum Formatieren mit ControlTemplates](http://go.microsoft.com/fwlink/?LinkID=160041).  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.FrameworkElement.Style%2A>  
 <xref:System.Windows.Controls.ControlTemplate>  
 [Steuerelementformate und -vorlagen](../../../../docs/framework/wpf/controls/control-styles-and-templates.md)  
 [Anpassung von Steuerelementen](../../../../docs/framework/wpf/controls/control-customization.md)  
 [Erstellen von Formaten und Vorlagen](../../../../docs/framework/wpf/controls/styling-and-templating.md)  
 [Anpassen der Darstellung eines vorhandenen Steuerelements durch Erstellen einer ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)
