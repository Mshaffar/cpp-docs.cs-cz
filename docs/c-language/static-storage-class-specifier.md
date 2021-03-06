---
title: Statický specifikátor třídy úložiště
ms.date: 11/04/2016
helpviewer_keywords:
- static variables, specifier
- storage classes, static
- static storage class specifiers
ms.assetid: 9bce361e-919b-46b9-8148-40d7ab0eb024
ms.openlocfilehash: ef85ee4d757cb9579431427fba7b46a0e5ac905f
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62157939"
---
# <a name="static-storage-class-specifier"></a>Statický specifikátor třídy úložiště

Proměnná deklarovaná na vnitřní úrovni se specifikátorem třídy úložiště **static** má globální životnost, ale je viditelná pouze v rámci bloku, ve kterém je deklarována. V případě konstantních řetězců je použití **static** užitečné, protože řeší režii časté inicializace v často volaných funkcích.

## <a name="remarks"></a>Poznámky

Pokud **statickou** proměnnou explicitně neinicializujete, je ve výchozím nastavení inicializována na hodnotu 0. Uvnitř funkce **statická** způsobí přidělení úložiště a slouží jako definice. Vnitřní statické proměnné poskytují trvalé soukromé úložiště, které je viditelné pouze jedinou funkcí.

## <a name="see-also"></a>Viz také

[Třídy úložiště jazyka C](c-storage-classes.md)<br/>
[Třídy úložiště (C++)](../cpp/storage-classes-cpp.md)
