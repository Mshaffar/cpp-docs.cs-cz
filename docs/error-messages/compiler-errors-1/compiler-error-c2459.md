---
title: Chyba kompilátoru C2459
ms.date: 11/04/2016
f1_keywords:
- C2459
helpviewer_keywords:
- C2459
ms.assetid: 81e29f4c-5b60-40fb-9557-1cdc630d77e8
ms.openlocfilehash: c49c348968f750c7e5c64ab9ef4f298d3fc74f67
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74743988"
---
# <a name="compiler-error-c2459"></a>Chyba kompilátoru C2459

identifikátor: je definován; nejde přidat jako anonymní člen.

Třída, struktura nebo sjednocení jsou předefinovány ve vlastním oboru členem anonymního sjednocení.

Následující ukázka generuje C2459:

```cpp
// C2459.cpp
// compile with: /c
class C {
   union { int C; };   // C2459
   union { int D; };
};
```
