---
title: Kompilátor upozornění (úroveň 4) C4463
ms.date: 11/04/2016
f1_keywords:
- C4463
helpviewer_keywords:
- C4463
ms.assetid: a07ae70c-db4e-472b-8b58-9137d9997323
ms.openlocfilehash: e125a532f87533958ec43ed5580665ad4108856b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62400796"
---
# <a name="compiler-warning-level-4-c4463"></a>Kompilátor upozornění (úroveň 4) C4463

> přetečení; přiřazení *hodnotu* bitové pole, které můžou ukládat jenom hodnoty z *low_value* k *high_value*

Přiřazená *hodnotu* je mimo rozsah hodnot, které mohou obsahovat bitového pole. Typy signed bitového pole použít nejvyšším bit pro přihlašování, takže když *n* je velikost bitového pole, rozsah -2 je podepsaný bitová pole<sup>n-1</sup> na 2<sup>n-1</sup>-1, zatímco bez znaménka Bitová pole mají rozsah od 0 do 2<sup>n</sup>-1.

## <a name="example"></a>Příklad

Tento příklad vygeneruje C4463, protože se pokouší přiřadit hodnotu 3 pro bitové pole typu `int` s velikostí 2, který má rozsahu od -2 na 1.

Chcete-li vyřešit tento problém, můžete změnit hodnotu přiřazenou na něco v povoleném rozsahu. Pokud bitového pole je určený pro uchování hodnoty bez znaménka v rozsahu od 0 do 3, můžete změnit typ deklarace k `unsigned`. Pokud je pole pro uchování hodnoty v rozsahu -4 až 3, můžete změnit velikost bitového pole na 3.

```cpp
// C4463_overflow.cpp
// compile with: cl /W4 /EHsc C4463_overflow.cpp
struct S {
    int x : 2; // int type treats high-order bit as sign
};

int main() {
    S s;
    s.x = 3; // warning C4463: overflow; assigning 3
    // to bit-field that can only hold values from -2 to 1
    // To fix, change assigned value to fit in range,
    // increase size of bitfield, and/or change base type
    // to unsigned.
}
```
