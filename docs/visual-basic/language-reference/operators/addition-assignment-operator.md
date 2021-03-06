---
title: +=-Operator (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.+=
helpviewer_keywords:
- += operator [Visual Basic]
- assignment statements [Visual Basic], compound
- statements [Visual Basic], compound assignment
- += operator [Visual Basic], appending strings
- compound assignment statements [Visual Basic]
ms.assetid: d3e959f4-85d4-4e47-87c4-77b62335a5b3
ms.openlocfilehash: f12a0560d984f871110c02f1df2c2ec42b68809b
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="-operator-visual-basic"></a>+=-Operator (Visual Basic)
Fügt den Wert eines numerischen Variablen oder einer Eigenschaft den Wert eines numerischen Ausdrucks und weist das Ergebnis der Variablen oder Eigenschaft. Kann auch zum Verketten verwendet eine `String` Ausdruck, der eine `String` Variablen oder einer Eigenschaft und das Ergebnis der Variablen oder Eigenschaft zuzuweisen.  
  
## <a name="syntax"></a>Syntax  
  
```  
variableorproperty += expression  
```  
  
## <a name="parts"></a>Teile  
 `variableorproperty`  
 Erforderlich. Ein beliebiges numerisches oder `String` Variablen oder Eigenschaft.  
  
 `expression`  
 Erforderlich. Ein beliebiges numerisches oder `String` Ausdruck.  
  
## <a name="remarks"></a>Hinweise  
 Das Element auf der linken Seite von der `+=` Operator kann eine einfache Skalarvariable, eine Eigenschaft oder ein Element eines Arrays sein. Die Variable oder Eigenschaft kann nicht [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md).  
  
 Die `+=` Operator fügt den Wert auf der rechten Seite der Variablen oder Eigenschaft auf der linken und weist das Ergebnis der Variablen oder Eigenschaft auf der linken Seite. Die `+=` -Operator kann auch zum Verketten verwendet werden die `String` Ausdruck auf der rechten Seite, um die `String` Variable oder die Eigenschaft auf der linken Seite und weisen das Ergebnis der Variablen oder Eigenschaft auf der linken Seite.  
  
> [!NOTE]
>  Bei Verwendung der `+=` -Operator, Sie möglicherweise nicht zu bestimmen, ob die Addition oder Zeichenfolge Verkettung erfolgt. Verwenden der `&=` Operator zum Verketten, um Mehrdeutigkeit zu vermeiden und sich selbst dokumentierenden Code bereitzustellen.  
  
 Dieser Zuweisungsoperator führt implizit erweiternde jedoch keine einschränkende Konvertierungen, wenn der kompilierungsumgebung strikte Semantik erzwingt. Weitere Informationen zu dieser Konvertierungen finden Sie unter [Widening und einschränkende Konvertierungen](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md). Weitere Informationen zu strikte und flexible Semantik, finden Sie unter [Option Strict-Anweisung](../../../visual-basic/language-reference/statements/option-strict-statement.md).  
  
 Wenn Semantik zulässig sind, die `+=` Operator führt implizit eine Vielzahl von Zeichenfolgen und numerische Konvertierungen identisch, mit denen die `+` Operator. Ausführliche Informationen zu dieser Konvertierungen, finden Sie unter [+-Operator](../../../visual-basic/language-reference/operators/addition-operator.md).  
  
## <a name="overloading"></a>Überladen  
 Die `+` Operator kann *überladen*, was bedeutet, dass eine Klasse oder Struktur sein Verhalten definieren kann, wenn ein Operand den Typ der betreffenden Klasse oder Struktur hat. Überladen der `+` Operator wirkt sich auf das Verhalten der `+=` Operator. Wenn im Code verwendet `+=` auf eine Klasse oder Struktur, die Überladungen `+`, achten Sie verstehen, dass ihr neu definierten Verhalten. Weitere Informationen finden Sie unter [Operatorprozeduren](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die `+=` Operator, um den Wert einer Variablen mit einem anderen zu kombinieren. Der erste Teil verwendet `+=` mit numerischen Variablen einen Wert in einen anderen hinzufügen. Der zweite Teil verwendet `+=` mit `String` Variablen einen Wert mit einem anderen zu verketten. In beiden Fällen ist das Ergebnis der ersten Variablen zugewiesen.  
  
 [!code-vb[VbVbalrOperators#7](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-assignment-operator_1.vb)]  
  
 [!code-vb[VbVbalrOperators#8](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-assignment-operator_2.vb)]  
  
 Der Wert der `num1` ist jetzt 13 und den Wert des `str1` ist jetzt "103".  
  
## <a name="see-also"></a>Siehe auch  
 [+-Operator](../../../visual-basic/language-reference/operators/addition-operator.md)  
 [Zuweisungsoperatoren](../../../visual-basic/language-reference/operators/assignment-operators.md)  
 [Arithmetische Operatoren](../../../visual-basic/language-reference/operators/arithmetic-operators.md)  
 [Verkettungsoperatoren](../../../visual-basic/language-reference/operators/concatenation-operators.md)  
 [Operator Precedence in Visual Basic (Operatorrangfolge in Visual Basic)](../../../visual-basic/language-reference/operators/operator-precedence.md)  
 [Nach Funktionalität sortierte Operatoren](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)  
 [Anweisungen](../../../visual-basic/programming-guide/language-features/statements.md)
