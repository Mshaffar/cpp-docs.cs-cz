---
title: sin, sinf, sinl
ms.date: 4/2/2020
api_name:
- sinl
- sinf
- sin
- _o_sin
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-math-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _sinl
- sinf
- sinl
- sin
helpviewer_keywords:
- _sinl function
- sinl function
- calculating sines
- sin function
- trigonometric functions
- sinf function
ms.assetid: 737de73e-3590-45f9-8257-dc1c0c489dfc
ms.openlocfilehash: ecd6a03fb7a933391f50de9eb075d8247d60924f
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82915771"
---
# <a name="sin-sinf-sinl"></a>sin, sinf, sinl

Vypočítá sinus hodnoty s plovoucí desetinnou čárkou.

## <a name="syntax"></a>Syntaxe

```C
double sin(double x);
float sinf(float x);
long double sinl(long double x);
```

```cpp
float sin(float x);  // C++ only
long double sin(long double x);  // C++ only
```

### <a name="parameters"></a>Parametry

*znak*<br/>
Úhel v radiánech.

## <a name="return-value"></a>Návratová hodnota

Funkce **Sin** Vrátí sinus hodnoty *x*. Pokud *x* je větší nebo rovno 263 nebo menší než nebo rovno-263, dojde ke ztrátě významnosti ve výsledku.

|Vstup|Výjimka SEH|Výjimka matherr|
|-----------|-------------------|-----------------------|
|QNAN, ZASÁHNOUT|Žádné|_DOMAIN|
|± ∞ (sin, sinf –, Sinl)|NENÍ|_DOMAIN|

Další informace o návratových kódech naleznete v tématu [errno, _doserrno, _sys_errlist a _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md).

## <a name="remarks"></a>Poznámky

Vzhledem k tomu, že jazyk C++ umožňuje přetížení, můžete volat přetížení **Sin** , která přijímají a vracejí hodnoty **float** nebo **Long** **Double** . V programu v jazyce C funkce **Sin** vždycky bere a vrací hodnotu **Double**.

Ve výchozím nastavení je globální stav této funkce vymezen na aplikaci. Pokud ho chcete změnit, přečtěte si téma [globální stav v CRT](../global-state.md).

## <a name="requirements"></a>Požadavky

|Rutina|Požadovaná hlavička (C)|Požadovaná hlavička (C++)|
|-|-|-|
|**Sin**, **sinf –**, **Sinl**|\<Math. h>|\<cmath> nebo \<Math. h>|

Další informace o kompatibilitě naleznete v tématu [Kompatibilita](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Příklad

```C
// crt_sincos.c
// This program displays the sine and cosine of pi / 2.
// Compile by using: cl /W4 crt_sincos.c

#include <math.h>
#include <stdio.h>

int main( void)
{
   double pi = 3.1415926535;
   double x, y;

   x = pi / 2;
   y = sin( x );
   printf( "sin( %f ) = %f\n", x, y );
   y = cos( x );
   printf( "cos( %f ) = %f\n", x, y );
}
```

```Output
sin( 1.570796 ) = 1.000000
cos( 1.570796 ) = 0.000000
```

## <a name="see-also"></a>Viz také

[Podpora plovoucí desetinné čárky](../../c-runtime-library/floating-point-support.md)<br/>
[acos, acosf, acosl](acos-acosf-acosl.md)<br/>
[asin, asinf, asinl](asin-asinf-asinl.md)<br/>
[atan, atanf, atanl, atan2, atan2f, atan2l](atan-atanf-atanl-atan2-atan2f-atan2l.md)<br/>
[cos, cosf, cosl](cos-cosf-cosl.md)<br/>
[tan, tanf, tanl](tan-tanf-tanl.md)<br/>
[_CIsin](../../c-runtime-library/cisin.md)<br/>
