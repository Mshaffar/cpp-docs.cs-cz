---
title: Chyba kompilátoru C3055
ms.date: 11/04/2016
f1_keywords:
- C3055
helpviewer_keywords:
- C3055
ms.assetid: 60446ee0-18dd-48fc-9059-f0a14229dce8
ms.openlocfilehash: 0bfd045079a7f0fbbd078d3d859d5687e96338dd
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74761169"
---
# <a name="compiler-error-c3055"></a>Chyba kompilátoru C3055

' symbol ': symbol nemůže být odkazován předtím, než se použije v direktivě ' threadprivate '.

Byl odkazován symbol a pak použit v klauzuli [threadprivate](../../parallel/openmp/reference/threadprivate.md) , což není povoleno.

Následující ukázka generuje C3055:

```cpp
// C3055.cpp
// compile with: /openmp
int x, y;
int z = x;
#pragma omp threadprivate(x, y)   // C3055

void test() {
   #pragma omp parallel copyin(x, y)
   {
      x = y;
   }
}
```

Možné řešení:

```cpp
// C3055b.cpp
// compile with: /openmp /LD
int x, y, z;
#pragma omp threadprivate(x, y)

void test() {
   #pragma omp parallel copyin(x, y)
   {
      x = y;
   }
}
```
