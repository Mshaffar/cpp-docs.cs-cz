---
title: Chyba kompilátoru C3052
ms.date: 11/04/2016
f1_keywords:
- C3052
helpviewer_keywords:
- C3052
ms.assetid: 87480c42-1ceb-4775-8d20-88c54a7bb6a6
ms.openlocfilehash: 618fac69078987b0322739733c403e5b2cd36486
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74761215"
---
# <a name="compiler-error-c3052"></a>Chyba kompilátoru C3052

var: proměnná se neobjevuje v klauzuli data-Sharing pod klauzulí default (None).

Pokud se použije [výchozí (žádné)](../../parallel/openmp/reference/default-openmp.md) , musí být jakákoli proměnná použitá ve strukturovaném bloku explicitně zadaná buď jako [sdílená](../../parallel/openmp/reference/shared-openmp.md) , nebo [soukromá](../../parallel/openmp/reference/private-openmp.md).

Následující ukázka generuje C3052:

```cpp
// C3052.cpp
// compile with: /openmp /c
int main() {
   int n1 = 1;

   #pragma omp parallel default(none) // shared(n1) private(n1)
   {
      n1 = 0;   // C3052 use either a shared or private clause
   }
}
```
