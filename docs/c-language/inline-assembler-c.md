---
title: Vložený assembler (C)
ms.date: 11/04/2016
helpviewer_keywords:
- __asm keyword [C]
- inline assembler [C]
ms.assetid: 821acc77-60b1-434c-ba54-2ba930a25ab4
ms.openlocfilehash: 8fb2a1dd3e87ef452083935e23048d80b4cdc8c3
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62233174"
---
# <a name="inline-assembler-c"></a>Vložený assembler (C)

**Specifické pro Microsoft**

Vložený assembler umožňuje vložení instrukcí sestavení jazyka přímo do zdrojových programů v jazyce C bez nutnosti dodatečných kroků sestavení a propojení. Vložený assembler je integrován v kompilátoru, takže nepotřebujete používat samostatný kompilátor, jako například Microsoft Macro Assembler (MASM).

Protože vložený assembler nevyžaduje samostatné kroky sestavení a propojení, je pohodlnější než samostatný assembler. Kód vloženého sestavení může použít název proměnné nebo funkce jazyka C, který je v rozsahu, takže jej lze snadno integrovat do kódu jazyka C programu. A protože lze kód sestavení kombinovat s příkazy jazyka C, lze provádět úkoly, které jsou v samostatném jazyce C náročné nebo nemožné.

Klíčové slovo `__asm` vyvolá vložený assembler a může se objevit všude, kde lze použít příkaz jazyka C. Nemůže být použit sám sebou. Musí následovat instrukce sestavení, skupina instrukcí uzavřených ve složených závorkách nebo, minimálně prázdný pár složených závorek. Termín "`__asm` Block" zde odkazuje na jakoukoli instrukci nebo skupinu instrukcí, bez ohledu na to, zda jsou v závorkách.

Kód níže je jednoduchý blok `__asm` uzavřený ve složených závorkách. (Kód je posloupnost vlastní funkce sekvence prologu.)

```
__asm
{
   push ebp
   mov  ebp, esp
   sub  esp, __LOCAL_SIZE
}
```

Alternativně můžete umístit `__asm` před každou instrukci sestavení:

```
__asm push ebp
__asm mov  ebp, esp
__asm sub  esp, __LOCAL_SIZE
```

Protože klíčové slovo `__asm` představuje oddělovač výrazů, lze také umístit pokyny sestavení na stejný řádek:

```
__asm push ebp   __asm mov  ebp, esp   __asm sub  esp, __LOCAL_SIZE
```

**Specifické pro konec Microsoftu**

## <a name="see-also"></a>Viz také

[Atributy funkce](../c-language/function-attributes.md)
