---
title: Anonymní typy třídy
ms.date: 11/04/2016
helpviewer_keywords:
- class types [C++], anonymous
- anonymous class types
ms.assetid: 9ba667b2-8c2a-4c29-82a6-fa120b9233c8
ms.openlocfilehash: e227f48588c3c4f59c0d0bd28ab16178de159b58
ms.sourcegitcommit: 89d9e1cb08fa872483d1cde98bc2a7c870e505e9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2020
ms.locfileid: "82032080"
---
# <a name="anonymous-class-types"></a>Anonymní typy třídy

Třídy mohou být anonymní – to znamená, že mohou být deklarovány bez *identifikátoru*. To je užitečné, když nahradíte název třídy názvem **typedef,** jako v následujícím:

```cpp
typedef struct
{
    unsigned x;
    unsigned y;
} POINT;
```

> [!NOTE]
> Použití anonymních tříd uvedené v předchozím příkladu je užitečné pro zachování kompatibility se stávajícím kódem jazyka C. V některých kódu C je převládající použití **typedef** ve spojení s anonymní struktury.

Anonymní třídy jsou také užitečné, pokud chcete odkazovat člena třídy, jako by nebyl obsažen v samostatné třídě (viz následující příklad):

```cpp
struct PTValue
{
    POINT ptLoc;
    union
    {
        int  iValue;
        long lValue;
    };
};

PTValue ptv;
```

V předchozím kódu `iValue` lze přistupovat pomocí operátoru výběru členů objektu (**.**) následujícím způsobem:

```cpp
int i = ptv.iValue;
```

Na anonymní třídy se vztahují jistá omezení. (Další informace o anonymních sjednoceních naleznete v tématu [Sjednocení](../cpp/unions.md).) Anonymní třídy:

- Nemohou mít konstruktor ani destruktor.

- Nelze předat jako argumenty funkcím (pokud není kontrola typu poražena pomocí tři tečky).

- Nelze je vrátit jako návratové hodnoty funkcí.

## <a name="anonymous-structs"></a>Anonymní struktury

**Specifické pro Microsoft**

Rozšíření jazyka Microsoft C umožňuje deklarovat proměnnou struktury v jiné struktuře bez zadání názvu. Tyto vnořené struktury se nazývají anonymní struktury. Jazyk C++ nepovoluje anonymní struktury.

Ke členům anonymní struktury lze přistupovat, jako kdyby byly členy obsahující struktury.

```cpp
// anonymous_structures.c
#include <stdio.h>

struct phone
{
    int  areacode;
    long number;
};

struct person
{
    char   name[30];
    char   gender;
    int    age;
    int    weight;
    struct phone;    // Anonymous structure; no name needed
} Jim;

int main()
{
    Jim.number = 1234567;
    printf_s("%d\n", Jim.number);
}
//Output: 1234567
```

**END Microsoft Specifické**
