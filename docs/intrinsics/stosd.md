---
title: __stosd
ms.date: 09/02/2019
f1_keywords:
- __stosd
helpviewer_keywords:
- stosd instruction
- rep stosd instruction
- __stosd intrinsic
ms.assetid: 03104247-1cea-49f6-b6f8-287917bf5680
ms.openlocfilehash: c46bb124390ff23d79361c66530493c48faf3f0a
ms.sourcegitcommit: 6e1c1822e7bcf3d2ef23eb8fac6465f88743facf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/03/2019
ms.locfileid: "70219977"
---
# <a name="__stosd"></a>__stosd

**Specifické pro společnost Microsoft**

Vygeneruje instrukci řetězce úložiště`rep stosd`().

## <a name="syntax"></a>Syntaxe

```C
void __stosd(
   unsigned long* Destination,
   unsigned long Data,
   size_t Count
);
```

### <a name="parameters"></a>Parametry

*Tabulka*\
mimo Cíl operace.

*Údajů*\
pro Data, která se mají uložit

*Výpočtu*\
pro Délka bloku doubleword, který se má zapsat

## <a name="requirements"></a>Požadavky

|Vnitřním|Architektura|
|---------------|------------------|
|`__stosd`|x86, x64|

**Hlavičkový soubor** \<intrin. h >

## <a name="remarks"></a>Poznámky

Výsledkem je, že doubleword *data* jsou zapsána do bloku *Count* doubleword v umístění v paměti, na které odkazuje *cíl*.

Tato rutina je k dispozici pouze jako vnitřní objekt.

## <a name="example"></a>Příklad

```C
// stosd.c
// processor: x86, x64

#include <stdio.h>
#include <memory.h>
#include <intrin.h>

#pragma intrinsic(__stosd)

int main()
{
    unsigned long val = 99999;
    unsigned long a[10];

    memset(a, 0, sizeof(a));
    __stosd(a+1, val, 2);

printf_s( "%u %u %u %u",
              a[0], a[1], a[2], a[3]);
}
```

```Output
0 99999 99999 0
```

**Specifické pro konec Microsoftu**

## <a name="see-also"></a>Viz také:

[Vnitřní objekty kompilátoru](../intrinsics/compiler-intrinsics.md)
