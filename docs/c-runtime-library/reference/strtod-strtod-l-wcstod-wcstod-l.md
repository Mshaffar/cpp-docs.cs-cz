---
title: strtod, _strtod_l, wcstod, _wcstod_l
ms.date: 4/2/2020
api_name:
- wcstod
- _wcstod_l
- _strtod_l
- strtod
- _o__strtod_l
- _o__wcstod_l
- _o_strtod
- _o_wcstod
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
- api-ms-win-crt-convert-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _tcstod
- strtod
- wcstod
- _strtod_l
- _wcstod_l
- stdlib/strtod
- corecrt_wstdlib/wcstod
- stdlib/_strtod_l
- corecrt_wstdlib/_wcstod_l
helpviewer_keywords:
- wcstod_l function
- tcstod_l function
- _tcstod_l function
- strtod function
- _wcstod_l function
- wcstod function
- strtod_l function
- tcstod function
- _tcstod function
- _strtod_l function
- string conversion, to floating point values
ms.assetid: 0444f74a-ba2a-4973-b7f0-1d77ba88c6ed
ms.openlocfilehash: 410d339789ef4a29a6760a4118f967b22f4f3a8c
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82910880"
---
# <a name="strtod-_strtod_l-wcstod-_wcstod_l"></a>strtod, _strtod_l, wcstod, _wcstod_l

Převede řetězce na hodnotu s dvojitou přesností.

## <a name="syntax"></a>Syntaxe

```C
double strtod(
   const char *strSource,
   char **endptr
);
double _strtod_l(
   const char *strSource,
   char **endptr,
   _locale_t locale
);
double wcstod(
   const wchar_t *strSource,
   wchar_t **endptr
);
double wcstod_l(
   const wchar_t *strSource,
   wchar_t **endptr,
   _locale_t locale
);
```

### <a name="parameters"></a>Parametry

*strSource*<br/>
Řetězec zakončený hodnotou null pro převod.

*endptr*<br/>
Ukazatel na znak, který zastaví skenování.

*locale*<br/>
Národní prostředí, které se má použít

## <a name="return-value"></a>Návratová hodnota

**strtod** vrací hodnotu čísla s plovoucí desetinnou čárkou, s výjimkou případů, kdy by reprezentace způsobila přetečení. v takovém případě funkce vrací hodnotu +/-**HUGE_VAL**. Znaménko **HUGE_VAL** odpovídá znaménku hodnoty, kterou nelze reprezentovat. **strtod** vrátí hodnotu 0, pokud převod nelze provést, nebo dojde k podtečení.

**wcstod** vrací hodnoty obdobně **strtod**. Pro obě funkce je **errno** nastaveno na **ERANGE** , pokud dojde k přetečení nebo podtečení a je vyvolána obslužná rutina neplatného parametru, jak je popsáno v tématu [ověřování parametru](../../c-runtime-library/parameter-validation.md). Další informace o tomto a dalších návratových kódech naleznete v tématu [_doserrno, errno, _sys_errlist a _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md) .

## <a name="remarks"></a>Poznámky

Každá funkce převede vstupní řetězec *strSource* na **typ Double**. Funkce **strtod** převede *strSource* na hodnotu s dvojitou přesností. **strtod** zastaví čtení řetězce *strSource* u prvního znaku, který nelze rozpoznat jako součást čísla. Může to být ukončující znak null. **wcstod** je **strtod**verze s velkým znakem; jeho argument *strSource* je řetězec s velkým znakem. Tyto funkce se chovají identicky jinak.

Ve výchozím nastavení je globální stav této funkce vymezen na aplikaci. Pokud ho chcete změnit, přečtěte si téma [globální stav v CRT](../global-state.md).

### <a name="generic-text-routine-mappings"></a>Mapování rutin obecného textu

|Rutina TCHAR.H|_UNICODE & _MBCS není definováno.|_MBCS definováno|_UNICODE definováno|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_tcstod**|**strtod**|**strtod**|**wcstod**|
|**_tcstod_l**|**_strtod_l**|**_strtod_l**|**_wcstod_l**|

Nastavení kategorie **LC_NUMERIC** aktuálního národního prostředí Určuje rozpoznávání znaku bodu základu v *strSource*. Další informace naleznete v tématu [setlocale](setlocale-wsetlocale.md). Funkce bez přípony **_l** používají aktuální národní prostředí; **_strtod_l** je identická s **_strtod_l** s tím rozdílem, že místo toho používají předané *národní prostředí* . Další informace najdete v tématu [národní prostředí](../../c-runtime-library/locale.md).

Pokud *endptr* není **null**, ukazatel na znak, který zastavil skenování, je uložen v umístění, na které odkazuje *endptr*. Pokud převod nelze provést (nebyly nalezeny žádné platné číslice nebo byla zadána neplatná základna), hodnota *strSource* je uložena v umístění, na které odkazuje *endptr*.

**strtod** očekává, že *strSource* odkazuje na řetězec jedné z následujících forem:

[*prázdné znaky*] [*Sign*] {*číslice* [ *číslice**základů* ] &#124;ch *základových* *číslic*} [{**e** &#124; **e**} [*Sign*] *číslice*] [*prázdné*] [*Sign*] {**0x** &#124; **0x**} {*hexdigits* [*základ* *hexdigits* *] &#124; sequence* *hexdigits*} [{**p** &#124; **p**} [*Sign*] *hexdigits*]*[prázdné*] [*Sign*] {**INF** &#124; **Infinite**} [*prázdné*] [*Sign*] **NaN** [*Sequence*]

Volitelný úvodní *mezera* se může skládat z mezer a znaků tabulátoru, které jsou ignorovány; *znaménko* je buď znaménko plus (+) nebo minus (-); *číslice* jsou jednu nebo více desítkových číslic; *hexdigits* jsou jedna nebo více hexadecimálních číslic; *základ* je znak bodu základu, buď tečka (.) ve výchozím národním prostředí "C", nebo hodnota specifická pro národní prostředí, pokud je aktuální národní prostředí jiné nebo pokud je zadané *národní prostředí* . *sekvence* je posloupnost alfanumerických znaků nebo znaků podtržítka. V desítkových i hexadecimálních číslech, pokud se neobjeví žádné číslice před znakem číselného bodu, musí být alespoň jedna uvedena po znaku bodu základu. V desítkovém formátu může za desetinnou čárkou následovat exponent, který se skládá z úvodního písmene (**e** nebo **e**) a volitelně podepsaného celého čísla. V hexadecimálním formátu může být šestnáctkové číslo následováno exponentem, který se skládá z úvodního písmene (**p** nebo **p**) a volitelně podepsaného šestnáctkového čísla, které představuje exponent jako mocninu 2. V obou formách, pokud se nezobrazí část exponentu ani znak číselného bodu, předpokládá se, že se za poslední číslici v řetězci má použít znak bodu základu. Případ se ignoruje ve formulářích **INF** i **NaN** . První znak, který není vhodný pro jednu z těchto forem, zastaví kontrolu.

Verze UCRT těchto funkcí nepodporují konverzi exponentů pro styl FORTRAN (**d** nebo **d**). Toto nestandardní rozšíření bylo podporováno staršími verzemi CRT a může být zásadní změnou kódu. Verze UCRT podporují hexadecimální řetězce a kulaté Trip hodnot INF a NAN, které se v dřívějších verzích nepodporovaly. To může také způsobit zásadní změny v kódu. Například řetězec "0x1a" by byl interpretován **strtod** jako 0,0 v předchozích verzích, ale jako 26,0 ve verzi UCRT.

## <a name="requirements"></a>Požadavky

|Rutina|Požadovaný hlavičkový soubor|
|-------------|---------------------|
|**strtod**, **_strtod_l**|C: &lt;Stdlib. h> C++: &lt;cstdlib> nebo &lt;Stdlib. h> |
|**wcstod**, **_wcstod_l**|C: &lt;Stdlib. h> nebo &lt;WCHAR. h> C++: &lt;cstdlib>, &lt;stdlib. h> nebo &lt;WCHAR. h> |

Další informace o kompatibilitě naleznete v tématu [Kompatibilita](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Příklad

```C
// crt_strtod.c
// This program uses strtod to convert a
// string to a double-precision value; strtol to
// convert a string to long integer values; and strtoul
// to convert a string to unsigned long-integer values.
//

#include <stdlib.h>
#include <stdio.h>

int main( void )
{
   char   *string, *stopstring;
   double x;
   long   l;
   int    base;
   unsigned long ul;

   string = "3.1415926This stopped it";
   x = strtod( string, &stopstring );
   printf( "string = %s\n", string );
   printf("   strtod = %f\n", x );
   printf("   Stopped scan at: %s\n\n", stopstring );

   string = "-10110134932This stopped it";
   l = strtol( string, &stopstring, 10 );
   printf( "string = %s\n", string );
   printf("   strtol = %ld\n", l );
   printf("   Stopped scan at: %s\n\n", stopstring );

   string = "10110134932";
   printf( "string = %s\n", string );

   // Convert string using base 2, 4, and 8:
   for( base = 2; base <= 8; base *= 2 )
   {
      // Convert the string:
      ul = strtoul( string, &stopstring, base );
      printf( "   strtol = %ld (base %d)\n", ul, base );
      printf( "   Stopped scan at: %s\n", stopstring );
   }
}
```

```Output
string = 3.1415926This stopped it
   strtod = 3.141593
   Stopped scan at: This stopped it

string = -10110134932This stopped it
   strtol = -2147483648
   Stopped scan at: This stopped it

string = 10110134932
   strtol = 45 (base 2)
   Stopped scan at: 34932
   strtol = 4423 (base 4)
   Stopped scan at: 4932
   strtol = 2134108 (base 8)
   Stopped scan at: 932
```

## <a name="see-also"></a>Viz také

[Převod dat](../../c-runtime-library/data-conversion.md)<br/>
[Podpora plovoucí desetinné čárky](../../c-runtime-library/floating-point-support.md)<br/>
[Výklad sekvencí vícebajtových znaků](../../c-runtime-library/interpretation-of-multibyte-character-sequences.md)<br/>
[Jazyka](../../c-runtime-library/locale.md)<br/>
[Funkce řetězců na numerické hodnoty](../../c-runtime-library/string-to-numeric-value-functions.md)<br/>
[strtol, wcstol, _strtol_l, _wcstol_l](strtol-wcstol-strtol-l-wcstol-l.md)<br/>
[strtoul, _strtoul_l, wcstoul, _wcstoul_l](strtoul-strtoul-l-wcstoul-wcstoul-l.md)<br/>
[atof, _atof_l, _wtof, _wtof_l](atof-atof-l-wtof-wtof-l.md)<br/>
[localeconv](localeconv.md)<br/>
[_create_locale, _wcreate_locale](create-locale-wcreate-locale.md)<br/>
[_free_locale](free-locale.md)<br/>
