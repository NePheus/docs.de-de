---
title: Abrufen von unterstützten Steuerelementmustern für Benutzeroberflächenautomatisierung
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- control patterns, getting
- UI Automation, getting control patterns
- getting, control patterns
ms.assetid: 006c54c9-50bf-48d9-a855-9d62eb95603a
author: Xansky
ms.author: mhopkins
manager: markl
ms.openlocfilehash: fe492aa322f005e3bd118031e97e3837e3314093
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="get-supported-ui-automation-control-patterns"></a>Abrufen von unterstützten Steuerelementmustern für Benutzeroberflächenautomatisierung
> [!NOTE]
>  Diese Dokumentation ist für .NET Framework-Entwickler vorgesehen, die die verwalteten [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]-Klassen verwenden möchten, die im <xref:System.Windows.Automation>-Namespace definiert sind. Aktuelle Informationen zur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]finden Sie auf der Seite zur [Windows-Automatisierungs-API: UI-Automatisierung](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In diesem Thema wird gezeigt, wie Steuerelementmusterobjekte aus abzurufenden [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Elemente.  
  
### <a name="obtain-all-control-patterns"></a>Abrufen aller Steuerelementmuster  
  
1.  Abrufen der <xref:System.Windows.Automation.AutomationElement> , an dessen Steuerelementmustern Sie interessiert sind.  
  
2.  Rufen Sie <xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A> um alle Steuerelementmuster aus dem Element abzurufen.  
  
> [!CAUTION]
>  Es wird dringend empfohlen, dass ein Client nicht verwenden <xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>. Leistung kann schwerwiegend beeinträchtigt werden, wie diese Methode ruft <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> intern für jedes vorhandene Steuerelementmuster. Wenn möglich sollte ein Client Aufrufen <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> für die gewünschten Steuerelementmuster.  
  
### <a name="obtain-a-specific-control-pattern"></a>Abrufen eines bestimmten Steuerelementmusters  
  
1.  Abrufen der <xref:System.Windows.Automation.AutomationElement> , an dessen Steuerelementmustern Sie interessiert sind.  
  
2.  Rufen Sie <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> oder <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> auf ein bestimmtes Muster abzufragen. Diese Methoden ähneln sich, wenn das Muster nicht gefunden wird, aber <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> löst eine Ausnahme aus und <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> gibt `false`.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel ruft eine <xref:System.Windows.Automation.AutomationElement> für ein Listenelement und erhält eine <xref:System.Windows.Automation.SelectionItemPattern> aus diesem Element.  
  
 [!code-csharp[UIAClient_snip#103](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#103)]
 [!code-vb[UIAClient_snip#103](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#103)]  
  
## <a name="see-also"></a>Siehe auch  
 [Steuerelementmuster für Benutzeroberflächenautomatisierung für Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)
