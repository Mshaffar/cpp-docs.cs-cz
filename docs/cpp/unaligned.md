---
title: __unaligned
ms.date: 12/17/2018
f1_keywords:
- __unaligned_cpp
- __unaligned
- _unaligned
helpviewer_keywords:
- __unaligned keyword [C++]
ms.assetid: 0cd83aad-1840-47e3-ad33-59bfcbe6375b
ms.openlocfilehash: 5f93aaa79fd7c3664ecf80d5007d5954002bce4a
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80160642"
---
# <a name="__unaligned"></a>__unaligned

**Specifické pro společnost Microsoft**. Při deklaraci ukazatele pomocí modifikátoru **__unaligned** předpokládá kompilátor, že ukazatel odkazuje na data, která nejsou zarovnána. V důsledku toho je kód vhodný pro platformu vygenerován pro zpracování nezarovnaného čtení a zápisu přes ukazatel.

## <a name="remarks"></a>Poznámky

Tento modifikátor popisuje zarovnání dat, která jsou řešena ukazatelem; Předpokládá se, že ukazatel je zarovnaný.

Nutnost pro klíčové slovo **__unaligned** se liší podle platformy a prostředí. Nesprávné označení dat může mít za následek problémy v rozsahu od postihů výkonu až po hardwarové chyby. Modifikátor **__unaligned** není platný pro platformu x86.

Z důvodu kompatibility s předchozími verzemi je **_unaligned** synonymem pro **__unaligned** , pokud je zadána možnost kompilátoru [/za \(Disable Language Extensions)](../build/reference/za-ze-disable-language-extensions.md) .

Další informace o zarovnání naleznete v následujících tématech:

- [align](../cpp/align-cpp.md)

- [__alignof – operátor](../cpp/alignof-operator.md)

- [pack](../preprocessor/pack.md)

- [/Zp (zarovnání členů struktury)](../build/reference/zp-struct-member-alignment.md)

- [Příklady zarovnání struktur](../build/x64-software-conventions.md#examples-of-structure-alignment)

## <a name="see-also"></a>Viz také

[Klíčová slova](../cpp/keywords-cpp.md)
