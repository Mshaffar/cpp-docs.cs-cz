---
title: logical_or – struktura
ms.date: 11/04/2016
f1_keywords:
- functional/std::logical_or
helpviewer_keywords:
- logical_or class
- logical_or struct
ms.assetid: ec8143f8-5755-4e7b-8025-507fb6bf6911
ms.openlocfilehash: ec3637c1d5a2d0d916aec012783cecd37a179468
ms.sourcegitcommit: 3590dc146525807500c0477d6c9c17a4a8a2d658
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/16/2019
ms.locfileid: "68246452"
---
# <a name="logicalor-struct"></a>logical_or – struktura

Předdefinovaný objekt funkce, který provádí operace logická disjunkce ( `operator||`) na svých argumentů.

## <a name="syntax"></a>Syntaxe

```
template <class Type = void>
struct logical_or : public binary_function<Type, Type, bool>
{
    bool operator()(const Type& Left, const Type& Right) const;
};

// specialized transparent functor for operator||
template <>
struct logical_or<void>
{
  template <class T, class U>
  auto operator()(T&& Left, U&& Right) const`
    -> decltype(std::forward<T>(Left) || std::forward<U>(Right));
};
```

### <a name="parameters"></a>Parametry

*Typ*, *T*, *U*\
Libovolný typ, který podporuje `operator||` , která přebírá operandů zadaný nebo odvozené typy.

*doleva*\
Levý operand logická disjunkce operace. Nespecializovaná šablony přebírá argument typu odkazu l-hodnoty *typ*. Specializovaná šablona perfektní přesměrování l-hodnoty a argumenty odkazu rvalue odvodit typ *T*.

*doprava*\
Pravý operand logická disjunkce operace. Nespecializovaná šablony přebírá argument typu odkazu l-hodnoty *typ*. Specializovaná šablona perfektní přesměrování l-hodnoty a argumenty odkazu rvalue odvodit typ *U*.

## <a name="return-value"></a>Návratová hodnota

Výsledek `Left || Right`. Specializovaná šablona perfektní přesměrování výsledku, který má typ, který je vrácen `operator||`.

## <a name="remarks"></a>Poznámky

Pro typy definované uživatelem neexistuje žádné krátký cyklus vyhodnocení operand. Oba argumenty jsou vyhodnocovány pomocí `operator||`.

## <a name="example"></a>Příklad

```cpp
// functional_logical_or.cpp
// compile with: /EHsc
#include <deque>
#include <algorithm>
#include <functional>
#include <iostream>

int main( )
{
   using namespace std;
   deque <bool> d1, d2, d3( 7 );
   deque <bool>::iterator iter1, iter2, iter3;

   int i;
   for ( i = 0 ; i < 7 ; i++ )
   {
      d1.push_back((bool)((rand() % 2) != 0));
   }

   int j;
   for ( j = 0 ; j < 7 ; j++ )
   {
      d2.push_back((bool)((rand() % 2) != 0));
   }

   cout << boolalpha;    // boolalpha I/O flag on

   cout << "Original deque:\n d1 = ( " ;
   for ( iter1 = d1.begin( ) ; iter1 != d1.end( ) ; iter1++ )
      cout << *iter1 << " ";
   cout << ")" << endl;

   cout << "Original deque:\n d2 = ( " ;
   for ( iter2 = d2.begin( ) ; iter2 != d2.end( ) ; iter2++ )
      cout << *iter2 << " ";
   cout << ")" << endl;

   // To find element-wise disjunction of the truth values
   // of d1 & d2, use the logical_or function object
   transform( d1.begin( ), d1.end( ), d2.begin( ),
      d3.begin( ), logical_or<bool>( ) );
   cout << "The deque which is the disjuction of d1 & d2 is:\n d3 = ( " ;
   for ( iter3 = d3.begin( ) ; iter3 != d3.end( ) ; iter3++ )
      cout << *iter3 << " ";
   cout << ")" << endl;
}
```

```Output
Original deque:
d1 = ( true true false false true false false )
Original deque:
d2 = ( false false false true true true true )
The deque which is the disjuction of d1 & d2 is:
d3 = ( true true false true true true true )
```
