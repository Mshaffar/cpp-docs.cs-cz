---
title: Chyba kompilátoru C2807
ms.date: 11/04/2016
f1_keywords:
- C2807
helpviewer_keywords:
- C2807
ms.assetid: bd7a207a-f379-4de6-8ee8-c7cab78b3480
ms.openlocfilehash: 8376f7aba0d090fa43ae675fe32cbfee182a6230
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74760605"
---
# <a name="compiler-error-c2807"></a>Chyba kompilátoru C2807

druhý formální parametr pro příponu operátoru operator operator musí být typu int.

Druhý parametr pro operátor přípony má nesprávný typ.

Následující ukázka generuje C2807:

```cpp
// C2807.cpp
// compile with: /c
class X {
public:
   X operator++ ( X );   // C2807 nonvoid parameter
   X operator++ ( int );   // OK, int parameter
};
```
