---
title: '&#39;&lt;Klassenname&gt; &#39; ist nicht CLS-kompatibel, da die Schnittstelle &#39; &lt;Schnittstellenname&gt; &#39; er implementiert ist nicht CLS-kompatibel.'
ms.date: 07/20/2015
f1_keywords:
- bc40029
- vbc40029
helpviewer_keywords:
- BC40029
ms.assetid: 178452f3-5575-4da0-9d6c-53bcddb6a338
ms.openlocfilehash: 4dda0e16a94f43cdb3deeff16fabdd1b10b62526
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="39ltclassnamegt39-is-not-cls-compliant-because-the-interface-39ltinterfacenamegt39-it-implements-is-not-cls-compliant"></a>&#39;&lt;Klassenname&gt; &#39; ist nicht CLS-kompatibel, da die Schnittstelle &#39; &lt;Schnittstellenname&gt; &#39; er implementiert ist nicht CLS-kompatibel.
Eine Klasse oder Schnittstelle wird als `<CLSCompliant(True)>` gekennzeichnet, wenn sie von einem Typ abgeleitet ist oder einen Typ implementiert, der als `<CLSCompliant(False)>` oder gar nicht gekennzeichnet ist.  
  
 Für eine Klasse oder Schnittstelle einhalten der [Sprachenunabhängigkeit und sprachunabhängige Komponenten](../../../standard/language-independence-and-language-independent-components.md) (CLS), ihre gesamte Vererbungshierarchie kompatibel sein muss. Das bedeutet, dass jeder Typ, von dem sie direkt oder indirekt erbt, kompatibel sein muss. Analog dazu muss eine Klasse, wenn sie eine oder mehrere Schnittstellen implementiert, deren Kompatibilität durch alle Vererbungshierarchien sicherstellen.  
  
 Wenn Sie das <xref:System.CLSCompliantAttribute> auf ein Programmierelement anwenden, legen Sie den `isCompliant` -Parameter des Attributs auf `True` oder `False` fest, um die Kompatibilität bzw. Nichtkompatibilität anzugeben. Es gibt keinen Standardwert für diesen Parameter, und Sie müssen einen Wert angeben.  
  
 Wenn Sie das <xref:System.CLSCompliantAttribute> nicht auf ein Element anwenden, wird dieses als nicht kompatibel betrachtet.  
  
 Standardmäßig ist diese Meldung eine Warnung. Informationen zum Ausblenden von Warnungen oder zum Behandeln von Warnungen als Fehler finden Sie unter [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **Fehler-ID:** BC40029  
  
## <a name="to-correct-this-error"></a>So beheben Sie diesen Fehler  
  
-   Wenn Sie CLS-Kompatibilität benötigen, definieren Sie diesen Typ innerhalb einer anderen Vererbungshierarchie oder eines anderen Implementierungsschemas.  
  
-   Wenn dieser Typ in der aktuellen Vererbungshierarchie oder dem aktuellen Implementierungsschema verbleiben muss, entfernen Sie das <xref:System.CLSCompliantAttribute> aus seiner Definition, oder kennzeichnen Sie ihn als `<CLSCompliant(False)>`.  
  
 
