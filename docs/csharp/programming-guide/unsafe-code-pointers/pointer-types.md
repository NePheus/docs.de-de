---
title: Zeigertypen (C#-Programmierhandbuch)
ms.date: 04/20/2018
helpviewer_keywords:
- unsafe code [C#], pointers
- pointers [C#]
ms.openlocfilehash: cbc75a2ec6fe826cb192b1e8bef61c7295f13916
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="pointer-types-c-programming-guide"></a>Zeigertypen (C#-Programmierhandbuch)

In einem unsicheren Kontext kann ein Typ sowohl ein Zeigertyp als auch ein Werttyp oder Verweistyp sein. Eine Zeigertypdeklaration erfolgt in einer der folgenden Formen:

``` csharp
type* identifier;
void* identifier; //allowed but not recommended
```

Der Typ, der vor `*` in einem Zeigertyp angegeben wird, wird als **Verweistyp** bezeichnet. Die folgenden Typen können Verweistypen sein:

- Ein beliebiger integraler Typ: [sbyte](../../language-reference/keywords/sbyte.md), [byte](../../language-reference/keywords/byte.md), [short](../../language-reference/keywords/short.md), [ushort](../../language-reference/keywords/ushort.md), [int](../../language-reference/keywords/int.md), [uint](../../language-reference/keywords/uint.md), [long](../../language-reference/keywords/long.md) oder [ulong](../../language-reference/keywords/ulong.md).
- Ein beliebiger Gleitkommatyp: [float](../../language-reference/keywords/float.md) oder [double](../../language-reference/keywords/double.md).
- [char](../../language-reference/keywords/char.md).
- [bool](../../language-reference/keywords/bool.md).
- [decimal](../../language-reference/keywords/decimal.md).
- Beliebiger [enum](../../language-reference/keywords/enum.md)-Typ.
- Beliebiger Zeigertyp. Dadurch können Sie Ausdrücke wie `void**` verwenden.
- Beliebiger benutzerdefinierter Strukturtyp, der nur Felder von nicht verwalteten Typen enthält.

Zeigertypen erben nicht von [object`object`, und es ist keine Konvertierung zwischen Zeigertypen und ](../../language-reference/keywords/object.md) möglich. Weiterhin unterstützen Boxing und Unboxing keine Zeiger. Es ist jedoch möglich, Konvertierungen zwischen verschiedenen Zeigertypen sowie zwischen Zeigertypen und ganzzahligen Typen durchzuführen.

Wenn Sie mehrere Zeiger innerhalb ein- und derselben Deklaration deklarieren, wird das Sternchen (*) nur einmal mit dem zugrunde liegenden Typ notiert und nicht als Präfix für jeden Zeigernamen verwendet. Zum Beispiel:

```csharp
int* p1, p2, p3;   // Ok
int *p1, *p2, *p3;   // Invalid in C#
```

Ein Zeiger kann nicht auf einen Verweis oder eine [Struktur](../../language-reference/keywords/struct.md) verweisen, die Verweise enthält, da ein Objektverweis auch dann in die Garbage Collection aufgenommen werden kann, wenn ein Zeiger darauf verweist. In der Garbage Collection wird nicht nachgehalten, ob von einem der Zeigertypen auf ein Objekt verwiesen wird.

Der Wert der Zeigervariablen vom Typ `myType*` ist die Adresse einer Variablen vom Typ `myType`. Im Folgenden finden Sie Beispiele für Zeigertypdeklarationen:

|Beispiel|description|
|-------------|-----------------|
|`int* p`|`p` ist ein Zeiger auf einen ganzzahligen Wert.|
|`int** p`|`p` ist ein Zeiger auf einen Zeiger auf einen ganzzahligen Wert.|
|`int*[] p`|`p` ist ein eindimensionales Array von Zeigern auf ganzzahlige Werte.|
|`char* p`|`p` ist ein Zeiger auf eine char-Variable.|
|`void* p`|`p` ist ein Zeiger auf einen unbekannten Typ.|

Sie können den Zeigerdereferenzierungsoperator * verwenden, um auf den Inhalt an der Speicherstelle zuzugreifen, auf die die Zeigervariable zeigt. Betrachten Sie beispielsweise die folgende Deklaration:

```csharp
int* myVariable;
```

Der Ausdruck `*myVariable` kennzeichnet die `int`-Variable, die sich an der in `myVariable` enthaltenen Adresse befindet.

Es gibt mehrere Beispiele von Zeigern in den Themen [fixed-Anweisung](../../language-reference/keywords/fixed-statement.md) und [Zeigerkonvertierungen](../../programming-guide/unsafe-code-pointers/pointer-conversions.md). Im folgenden Beispiel wird die Verwendung des `unsafe`-Schlüsselworts und der `fixed`-Anweisung sowie die Vorgehensweise zum Erhöhen eines inneren Zeigers veranschaulicht.  Sie können diesen Code in die Hauptmethode einer Konsolenanwendung einfügen, um ihn auszuführen. Diese Beispiele müssen mithilfe der Compileroption [-unsafe](../../language-reference/compiler-options/unsafe-compiler-option.md) kompiliert werden.

[!code-csharp[Using pointer types](../../../../samples/snippets/csharp/keywords/FixedKeywordExamples.cs#5)]

Der Dereferenzierungsoperator kann nicht auf Zeiger vom Typ `void*` angewendet werden. Sie können jedoch eine Umwandlung verwenden, um einen void-Zeiger in einen anderen Zeigertyp und umgekehrt zu konvertieren.

Ein Zeiger kann den Wert `null` annehmen. Die Anwendung des Dereferenzierungsoperators auf einen NULL-Zeiger führt zu einem in der Implementierung definierten Verhalten.

Die Übergabe von Zeigern zwischen Methoden kann zu nicht definiertem Verhalten führen. Ziehen Sie eine Methode in Betracht, die einen Zeiger auf eine lokale Variable als einen `in`-, `out`- oder `ref`-Parameter oder als Funktionsergebnis zurückgibt. Wenn der Zeiger in einem fixed-Block festgelegt wurde, ist die Variable, auf die der Zeiger verweist, möglicherweise nicht fixiert.

In der folgenden Tabelle werden die Operatoren und Anweisungen aufgelistet, die in einem unsicheren Kontext auf Zeiger angewendet werden können.

|Operator/Anweisung|Mit|
|-------------------------|---------|
|*|Führt eine Zeigerdereferenzierung aus.|
|->|Greift über einen Zeiger auf einen Member einer Struktur zu.|
|[]|Indiziert einen Zeiger.|
|`&`|Ruft die Adresse einer Variablen ab.|
|++ und --|Inkrementiert und dekrementiert Zeiger.|
|+ und -|Führt Zeigerarithmetik aus.|
|==, !=, \<, >, \<=, und >=|Vergleicht Zeiger.|
|`stackalloc`|Belegt Speicher für den Stapel.|
|`fixed`-Anweisung|Fixiert eine Variable vorübergehend, damit ihre Adresse gefunden werden kann.|

## <a name="c-language-specification"></a>C#-Programmiersprachenspezifikation

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Siehe auch
 [C#-Programmierhandbuch](../index.md)  
 [Unsicherer Code und Zeiger](index.md)  
 [Zeigerkonvertierungen](pointer-conversions.md)  
 [Zeigerausdrücke](pointer-expressions.md)  
 [Typen](../../language-reference/keywords/types.md)  
 [unsafe](../../language-reference/keywords/unsafe.md)  
 [fixed-Anweisung](../../language-reference/keywords/fixed-statement.md)  
 [stackalloc](../../language-reference/keywords/stackalloc.md)  
 [Boxing und Unboxing](../types/boxing-and-unboxing.md)
