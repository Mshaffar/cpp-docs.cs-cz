---
title: Chyba kompilátoru C3012
ms.date: 11/04/2016
f1_keywords:
- C3012
helpviewer_keywords:
- C3012
ms.assetid: cc7040b1-b3fb-4da6-a474-877914d30332
ms.openlocfilehash: 69f0544815804e9827631be81bf9735a95bd1a22
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80176699"
---
# <a name="compiler-error-c3012"></a>Chyba kompilátoru C3012

> *vnitřní*: vnitřní funkce není povolená přímo v paralelní oblasti.

[Vnitřní funkce kompilátoru](../../intrinsics/compiler-intrinsics.md) není povolená v `omp parallel` oblasti. Chcete-li tento problém vyřešit, přesuňte vnitřní objekty mimo oblast nebo je nahraďte jinými nevnitřními ekvivalenty.

## <a name="example"></a>Příklad

Následující ukázka generuje C3012 a ukazuje jeden ze způsobů, jak ji opravit:

```cpp
// C3012.cpp
// compile with: /openmp
#ifdef __cplusplus
extern "C" {
#endif
void* _ReturnAddress();
#ifdef __cplusplus
}
#endif

int main()
{
   #pragma omp parallel
   {
      _ReturnAddress();   // C3012
   }
   _ReturnAddress();      // OK
}
```
