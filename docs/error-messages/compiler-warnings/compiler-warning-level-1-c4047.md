---
title: Upozornění kompilátoru (úroveň 1) C4047
ms.date: 11/04/2016
f1_keywords:
- C4047
helpviewer_keywords:
- C4047
ms.assetid: b75ad6fb-5c93-4434-a85f-c4083051a5de
ms.openlocfilehash: 1bed592325f864e41f7dfdf2edaad86630e4b205
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80164193"
---
# <a name="compiler-warning-level-1-c4047"></a>Upozornění kompilátoru (úroveň 1) C4047

' operator ': ' identifier1 ' se odlišuje od ' identifier2 ' úrovně dereference.

Ukazatel může ukazovat na proměnnou (jednu úroveň dereference) na jiný ukazatel, který odkazuje na proměnnou (dvě úrovně indirekce) a tak dále.

## <a name="example"></a>Příklad

Následující ukázka generuje C4047:

```c
// C4047.c
// compile with: /W1

int main() {
   char **p = 0;   // two levels of indirection
   char *q = 0;   // one level of indirection

   char *p2 = 0;   // one level of indirection
   char *q2 = 0;   // one level of indirection

   p = q;   // C4047
   p2 = q2;
}
```

## <a name="example"></a>Příklad

Následující ukázka generuje C4047:

```c
// C4047b.c
// compile with: /W1
#include <stdio.h>

int main() {
   int i;
   FILE *myFile = NULL;
   errno_t  err = 0;
   char file_name[256];
   char *cs = 0;

   err = fopen_s(&myFile, "C4047.txt", "r");
   if ((err != 0) || (myFile)) {
      printf_s("fopen_s failed!\n");
      exit(-1);
    }
   i = fgets(file_name, 256, myFile);   // C4047
   cs = fgets(file_name, 256, myFile);   // OK
}
```
