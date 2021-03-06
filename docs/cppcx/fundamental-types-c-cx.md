---
title: Základní typy (C++/CX)
ms.date: 01/22/2017
ms.assetid: c9f82907-25f2-440b-91d6-afb8dbd46ea6
ms.openlocfilehash: 2bd5be01b868fd3086c2064edfd4ca343db425be
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62301447"
---
# <a name="fundamental-types-ccx"></a>Základní typy (C++/CX)

Kromě standardní C++ vestavěné typy, C++/CX podporuje systém typů, který je definován architekturu Windows Runtime tím, že poskytuje – definice TypeDef pro Windows Runtime základních typů, která je namapována na úroveň standard C++ typy... C++/CX implementuje logická hodnota, znak a číselných základních typů. Tyto funkce TypeDef jsou definovány v `default` obor názvů, který nikdy musí být explicitně zadán. Kromě toho C++/CX poskytuje obálky a konkrétní implementace rozhraní a některé typy Windows Runtime.

## <a name="boolean-and-character-types"></a>Typy logické a znak

Následující tabulka uvádí integrované datový typ Boolean a typy znaků a jejich ekvivalenty standard C++.

|Obor názvů|C++/CX název|Definice|Standardní název jazyka C++|Rozsah hodnot|
|---------------|-----------------------------------------------------------------------|----------------|-------------------------|---------------------|
|Platforma|Boolean|Hodnotu typu Boolean. 8 bitů.|bool|**Hodnota TRUE** (nenulový) a **false** (nula)|
|default|char16|Hodnota nečíselné 16-bit, který představuje bod kódu Unicode (UTF-16).|wchar_t<br /><br /> -nebo-<br /><br /> L'c.|(Určený standardu Unicode)|

## <a name="numeric-types"></a>Číselné typy

V následující tabulce jsou uvedeny předdefinované číselné typy. Číselné typy jsou deklarovány v `default` výrazy TypeDef pro odpovídající C++ vestavěný typ oboru názvů a vyhoví se jim. Ne všechny C++ předdefinovaných typů (například dlouhý) jsou podporovány v modulu Windows Runtime. Konzistence a nejasnostem, doporučujeme použít C++/CX název.

|C++/CX název|Definice|Standardní název jazyka C++|Rozsah hodnot|
|-----------------------------------------------------------------------|----------------|-------------------------|---------------------|
|int8|8bitové podepsaný číselnou hodnotu.|podepsané char|-128 až 127.|
|uint8|8bitové hodnoty bez znaménka číselná.|unsigned char|0 až 255|
|int16|16bitové celé číslo se znaménkem.|short|-32 768 až 32 767|
|uint16|16bitové celé číslo bez znaménka.|unsigned short|0 až 65535|
|int32|32bitové celé číslo se znaménkem.|int|-2,147,483,648 prostřednictvím 2 147 483 647|
|uint32|32bitové celé číslo bez znaménka.|unsigned int|0 až 4 294 967 295|
|int64|64bitové celé číslo se znaménkem.|Long long - nebo - __int64|-9,223,372,036,854, 775,808 prostřednictvím 9,223,372,036,854,775,807|
|uint64|64bitové celé číslo bez znaménka.|unsigned long long - nebo - unsigned __int64|0 až 18,446,744,073,709,551,615|
|float32|IEEE 754 číslo s 32 bitů s plovoucí desetinnou čárkou|float|3, 4e +/-38 (7 číslic)|
|float64|IEEE 754 číslo s 64bitovým kompilátorem s plovoucí desetinnou čárkou|double|1, 7E +/-308 (15 číslic)|

## <a name="windows-runtime-types"></a>Typy Windows Runtime

V následující tabulce jsou uvedeny některé další typy, které jsou definovány pomocí architektury Windows Runtime a jsou integrované do C++/CX. Objekt a řetězce jsou odkazové typy. Ostatní jsou typy hodnot. Všechny tyto typy jsou deklarovány v `Platform` oboru názvů. Úplný seznam najdete v tématu [Platform – obor názvů](../cppcx/platform-namespace-c-cx.md).

|Název|Definice|
|----------|----------------|
|Objekt|Představuje libovolný typ Windows Runtime.|
|String|Posloupnost znaků, které představují text.|
|Rect|Sada s plovoucí desetinnou čárkou čtyři čísla, které představují, umístění a velikost obdélníku.|
|SizeT|Uspořádaná dvojice čísel s plovoucí desetinnou čárkou, určíte výšku a šířku.|
|Bod|Uspořádaná dvojice s plovoucí desetinnou čárkou souřadnice x a y souřadnic, které definují bod do dvourozměrné roviny.|
|Guid|Hodnota nečíselné 128-bit, který se používá jako jedinečný identifikátor.|
|UIntPtr|(Pouze pro interní použití.) Hodnoty bez znaménka 64-bit, který slouží jako ukazatel.|
|IntPtr|(Pouze pro interní použití.)  Podepsané 64 bitů hodnotu, která slouží jako ukazatel.|

## <a name="see-also"></a>Viz také:

[Systém typů](../cppcx/type-system-c-cx.md)
