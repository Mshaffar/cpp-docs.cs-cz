---
title: ODDÍLY (C/C++)
ms.date: 11/04/2016
f1_keywords:
- SECTIONS
helpviewer_keywords:
- SECTIONS .def file statement
ms.assetid: 7b974366-9ef5-4e57-bbcc-73a1df6f8857
ms.openlocfilehash: 5125b09675969c784aafe375faf1fdbc36d8c5d9
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62318625"
---
# <a name="sections-cc"></a>ODDÍLY (C/C++)

Představuje část jednoho nebo více `definitions` , které jsou specifikátory přístupu na oddíly výstupního souboru projektu.

```
SECTIONS
definitions
```

## <a name="remarks"></a>Poznámky

Každá definice musí být na samostatném řádku. `SECTIONS` – Klíčové slovo může být na stejném řádku jako první definice nebo na předchozím řádku. Soubor .def může obsahovat jeden nebo více `SECTIONS` příkazy.

To `SECTIONS` příkaz nastaví atributy pro jeden nebo více oddílů v souboru bitové kopie a je možné přepsat výchozí atributy pro každý typ části.

Formát pro `definitions` je:

`.section_name specifier`

kde `.section_name` je název oddílu v bitové kopii programu a `specifier` je jeden nebo více následující modifikátory přístupu:

|Modifikátor|Popis|
|--------------|-----------------|
|`EXECUTE`|V části je spustitelný|
|`READ`|Umožňuje čtení operací s daty|
|`SHARED`|Sdílené složky v části mezi všechny procesy, které načtení obrázku|
|`WRITE`|Umožňuje operací zápisu na data|

Specifikátor názvy oddělte mezerou. Příklad:

```
SECTIONS
.rdata READ WRITE
```

`SECTIONS` Označuje začátek seznam části `definitions`. Každý `definition` musí být na samostatném řádku. `SECTIONS` – Klíčové slovo může být na stejném řádku jako první `definition` nebo na předchozím řádku. Soubor .def může obsahovat jeden nebo více `SECTIONS` příkazy. `SEGMENTS` – Klíčové slovo je podporovaný jako synonymum pro `SECTIONS`.

Starší verze jazyka Visual C++ nepodporuje:

```
section [CLASS 'classname'] specifier
```

`CLASS` – Klíčové slovo je podporována z důvodu kompatibility, ale je ignorována.

Je ekvivalentní umožňuje určit atributy oddílu [/SECTION](section-specify-section-attributes.md) možnost.

## <a name="see-also"></a>Viz také:

[Pravidla pro příkazy definice modulu](rules-for-module-definition-statements.md)
