---
title: is, isw – rutiny
ms.date: 11/04/2016
api_location:
- msvcr110_clr0400.dll
- msvcr90.dll
- msvcr80.dll
- msvcr100.dll
- msvcr110.dll
- msvcr120.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- isw
- is
helpviewer_keywords:
- is routines
- isw routines
ms.assetid: 1e171a57-2cde-41f6-a75f-a080fa3c12e5
ms.openlocfilehash: 4dad7ff74112da7fc7d0d01714b0cf0dd4e4495c
ms.sourcegitcommit: f19474151276d47da77cdfd20df53128fdcc3ea7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/12/2019
ms.locfileid: "70940176"
---
# <a name="is-isw-routines"></a>is, isw – rutiny

|||
|-|-|
|[isalnum, iswalnum, _isalnum_l, _iswalnum_l](../c-runtime-library/reference/isalnum-iswalnum-isalnum-l-iswalnum-l.md)|[isgraph, iswgraph, _isgraph_l, _iswgraph_l](../c-runtime-library/reference/isgraph-iswgraph-isgraph-l-iswgraph-l.md)|
|[isalpha, iswalpha, _isalpha_l, _iswalpha_l](../c-runtime-library/reference/isalpha-iswalpha-isalpha-l-iswalpha-l.md)|[isleadbyte, _isleadbyte_l](../c-runtime-library/reference/isleadbyte-isleadbyte-l.md)|
|[isascii, __isascii, iswascii](../c-runtime-library/reference/isascii-isascii-iswascii.md)|[islower, iswlower, _islower_l, _iswlower_l](../c-runtime-library/reference/islower-iswlower-islower-l-iswlower-l.md)|
|[isblank, iswblank, _isblank_l, _iswblank_l](../c-runtime-library/reference/isblank-iswblank-isblank-l-iswblank-l.md)|[isprint, iswprint, _isprint_l, _iswprint_l](../c-runtime-library/reference/isprint-iswprint-isprint-l-iswprint-l.md)|
|[iscntrl, iswcntrl, _iscntrl_l, _iswcntrl_l](../c-runtime-library/reference/iscntrl-iswcntrl-iscntrl-l-iswcntrl-l.md)|[ispunct, iswpunct, _ispunct_l, _iswpunct_l](../c-runtime-library/reference/ispunct-iswpunct-ispunct-l-iswpunct-l.md)|
|[iscsym, iscsymf, __iscsym, \__iswcsym, \__iscsymf, \__iswcsymf, _iscsym_l, _iswcsym_l, _iscsymf_l, _iswcsymf_l](../c-runtime-library/reference/iscsym-functions.md)|[isspace, iswspace, _isspace_l, _iswspace_l](../c-runtime-library/reference/isspace-iswspace-isspace-l-iswspace-l.md)|
|[_isctype, iswctype, _isctype_l, _iswctype_l](../c-runtime-library/reference/isctype-iswctype-isctype-l-iswctype-l.md)|[isupper, _isupper_l, iswupper, _iswupper_l](../c-runtime-library/reference/isupper-isupper-l-iswupper-iswupper-l.md)|
|[isdigit, iswdigit, _isdigit_l, _iswdigit_l](../c-runtime-library/reference/isdigit-iswdigit-isdigit-l-iswdigit-l.md)|[isxdigit, iswxdigit, _isxdigit_l, _iswxdigit_l](../c-runtime-library/reference/isxdigit-iswxdigit-isxdigit-l-iswxdigit-l.md)|

## <a name="remarks"></a>Poznámky

Tyto rutiny testují znaky pro zadané podmínky.

Rutiny **is** poskytují smysluplné výsledky pro libovolný celočíselný argument z-1`EOF`() do **UCHAR_MAX** (0xFF) včetně. Očekávaný typ argumentu je `int`.

> [!CAUTION]
> Pro rutiny **is** může předání argumentu typu `char` vracet nepředvídatelné výsledky. Jednobajtové znaky SBCS nebo MBCS typu `char` s hodnotou větší než 0x7F jsou záporné. Pokud je předán, kompilátor může převést hodnotu na signed `int` nebo signed **Long**. `char` Tato hodnota může být pro kompilátor prodloužena znaménkem s neočekávanými výsledky.

Rutiny **ISW** poskytují smysluplné výsledky pro celočíselnou hodnotu z hodnoty-1 (**WEOF**) až 0xFFFF (včetně). Datový typ **wint_t** je definován v WCHAR. H jako **nepodepsaný krátký**; může obsahovat jakýkoli velký znak nebo hodnotu**WEOF**(celý znak konce souboru).

Výstupní hodnota je ovlivněna nastavením `LC_CTYPE` kategorie národního prostředí; viz [setlocale](../c-runtime-library/reference/setlocale-wsetlocale.md) pro další informace. Verze těchto funkcí bez přípony **_l** používají aktuální národní prostředí pro toto chování závislé na národním prostředí; verze s příponou **_l** jsou stejné s tím rozdílem, že místo toho používají předaný parametr národního prostředí.

V národním prostředí "C" jsou testovací podmínky **pro rutiny** následující:

`isalnum`<br/>
Alfanumerické znaky (A-Z, A-z nebo 0-9).

`isalpha`<br/>
Abecední znaky (A-Z nebo A-z).

`__isascii`<br/>
Znak ASCII (0x00-0x7F).

`isblank`<br/>
Horizontální tabulátor nebo znak mezery (0x09 nebo 0x20).

`iscntrl`<br/>
Řídicí znak (0x00-0x1F nebo 0x7F).

`__iscsym`<br/>
Písmeno, podtržítko nebo číslice.

`__iscsymf`<br/>
Písmeno nebo podtržítko.

`isdigit`<br/>
Desítková číslice (0-9).

`isgraph`<br/>
Tisknutelný znak s výjimkou mezerníku ().

`islower`<br/>
Malé písmeno (a – z).

`isprint`<br/>
Tisknutelný znak včetně prostoru (0x20-0x7E).

`ispunct`<br/>
Znak interpunkce.

`isspace`<br/>
Prázdný znak (0x09-0x0D nebo 0x20).

`isupper`<br/>
Velké písmeno (A – Z).

`isxdigit`<br/>
Šestnáctková číslice (A-F, A-f nebo 0-9).

Pro rutiny **ISW** je výsledek testu pro zadanou podmínku nezávislý na národním prostředí. Testovací podmínky pro funkce **ISW** jsou následující:

`iswalnum`<br/>
`iswalpha`nebo `iswdigit`.

`iswalpha`<br/>
Libovolný širší znak, který je jednou ze sad definovaných implementací, pro kterou žádná `iswcntrl`z `iswdigit`hodnot `iswpunct`,, `iswspace` ani není nenulová. `iswalpha`vrátí nenulovou hodnotu pouze pro velké znaky, `iswupper` pro `iswlower` které nebo je nenulové.

`iswascii`<br/>
Reprezentace znaku ASCII (0x0000-0x007F) s velkým počtem znaků.

`iswblank`<br/>
Širší znak, který odpovídá standardnímu znaku mezery nebo je jednou ze sad definovaných implementací velkých znaků, pro které `iswalnum` je hodnota false. Standardní prázdné znaky jsou mezera (L ' ') a horizontální tabelátor (L ' \t ').

`iswcntrl`<br/>
Ovládat širší znak.

`__iswcsym`<br/>
Libovolný širší znak, pro `isalnum` který je true nebo znak "_".

`__iswcsymf`<br/>
Libovolný širší znak, pro `iswalpha` který je true nebo znak "_".

`iswctype`<br/>
Znak má vlastnost určenou `desc` argumentem. Pro každou platnou hodnotu `desc` argumentu třídy `iswctype`existuje ekvivalentní rutina klasifikace se stejnou šířkou znaku, jak je znázorněno v následující tabulce:

### <a name="equivalence-of-iswctypec-desc-to-other-isw-testing-routines"></a>Rovnocennost iswctype (c, desc) pro jiné rutiny testování ISW

|Hodnota argumentu *DESC*|iswctype ( *c, desc* ) – ekvivalent|
|------------------------------|----------------------------------------|
|**_ALPHA**|**iswalpha (** `c` **)**|
|**_ALPHA** &#124; **_DIGIT**|**iswalnum (** `c` **)**|
|**_BLANK**|**iswblank (** `c` **)**|
|**_CONTROL**|**iswcntrl(** `c` **)**|
|**_DIGIT**|**iswdigit(** `c` **)**|
|**_ALPHA** &#124; **_DIGIT** &#124; **_PUNCT**|**iswgraph(** `c` **)**|
|**_LOWER**|**iswlower (** `c` **)**|
|**_ALPHA** &#124; **_BLANK** &#124; **_DIGIT** &#124; **_PUNCT**|**iswprint(** `c` **)**|
|**_PUNCT**|**iswpunct (** `c` **)**|
|**_BLANK**|**iswblank (** `c` **)**|
|**_SPACE**|**iswspace (** `c` **)**|
|**_UPPER**|**iswupper (** `c` **)**|
|**_HEX**|**iswxdigit (** `c` **)**|

`iswdigit`<br/>
Velký znak odpovídající znaku desítkové číslice.

`iswgraph`<br/>
Tisknutelný libovolný znak s výjimkou širšího znaku mezery (L ' ').

`iswlower`<br/>
Malé písmeno nebo jedna ze sad definovaných implementací velkých znaků, pro které žádná z hodnot `iswcntrl`, `iswdigit`, `iswpunct`ani `iswspace` není nenulová. `iswlower`vrátí nenulovou hodnotu pouze pro velké znaky, které odpovídají malým písmenům.

`iswprint`<br/>
Tisknutelný libovolný znak, včetně prostoru v šířce (L).

`iswpunct`<br/>
Tisknutelný libovolný znak, který není širší než mezera (L ' ') ani širší znak, pro `iswalnum` který je nenulový.

`iswspace`<br/>
Širší znak, který odpovídá standardnímu prázdnému znaku nebo je jednou ze sad definovaných implementací velkých znaků, pro které `iswalnum` je hodnota false. Standardní prázdné znaky jsou: mezera (L ' '), posun formuláře (L ' \f '), nový řádek (L ' \n '), návratová hodnota (L ' \r '), vodorovná karta (L ' \t ') a svislá karta (L ' \v ').

`iswupper`<br/>
Libovolný znak, který je velkými písmeny nebo je jednou ze sad definovaných implementací velkých znaků, pro které `iswcntrl`žádná `iswdigit`z `iswpunct`hodnot, `iswspace` , ani není nenulová. `iswupper`vrátí nenulovou hodnotu pouze pro velké znaky, které odpovídají velkým znakům.

`iswxdigit`<br/>
Širší znak, který odpovídá hexadecimálnímu znaku.

## <a name="example"></a>Příklad

```C
// crt_isfam.c
/* This program tests all characters between 0x0
* and 0x7F, then displays each character with abbreviations
* for the character-type codes that apply.
*/

#include <stdio.h>
#include <ctype.h>

int main( void )
{
   int ch;
   for( ch = 0; ch <= 0x7F; ch++ )
   {
      printf( "%.2x  ", ch );
      printf( " %c", isprint( ch )  ? ch   : ' ' );
      printf( "%4s", isalnum( ch )  ? "AN" : "" );
      printf( "%3s", isalpha( ch )  ? "A"  : "" );
      printf( "%3s", __isascii( ch )  ? "AS" : "" );
      printf( "%3s", iscntrl( ch )  ? "C"  : "" );
      printf( "%3s", __iscsym( ch )  ? "CS "  : "" );
      printf( "%3s", __iscsymf( ch )  ? "CSF"  : "" );
      printf( "%3s", isdigit( ch )  ? "D"  : "" );
      printf( "%3s", isgraph( ch )  ? "G"  : "" );
      printf( "%3s", islower( ch )  ? "L"  : "" );
      printf( "%3s", ispunct( ch )  ? "PU" : "" );
      printf( "%3s", isspace( ch )  ? "S"  : "" );
      printf( "%3s", isprint( ch )  ? "PR" : "" );
      printf( "%3s", isupper( ch )  ? "U"  : "" );
      printf( "%3s", isxdigit( ch ) ? "X"  : "" );
      printf( ".\n" );
   }
}
```

## <a name="output"></a>Výstup

```Output
00            AS  C                              .
01            AS  C                              .
02            AS  C                              .
03            AS  C                              .
04            AS  C                              .
05            AS  C                              .
06            AS  C                              .
07            AS  C                              .
08            AS  C                              .
09            AS  C                    S         .
0a            AS  C                    S         .
0b            AS  C                    S         .
0c            AS  C                    S         .
0d            AS  C                    S         .
0e            AS  C                              .
0f            AS  C                              .
10            AS  C                              .
11            AS  C                              .
12            AS  C                              .
13            AS  C                              .
14            AS  C                              .
15            AS  C                              .
16            AS  C                              .
17            AS  C                              .
18            AS  C                              .
19            AS  C                              .
1a            AS  C                              .
1b            AS  C                              .
1c            AS  C                              .
1d            AS  C                              .
1e            AS  C                              .
1f            AS  C                              .
20            AS                       S PR      .
21   !        AS              G    PU    PR      .
22   "        AS              G    PU    PR      .
23   #        AS              G    PU    PR      .
24   $        AS              G    PU    PR      .
25   %        AS              G    PU    PR      .
26   &        AS              G    PU    PR      .
27   '        AS              G    PU    PR      .
28   (        AS              G    PU    PR      .
29   )        AS              G    PU    PR      .
2a   *        AS              G    PU    PR      .
2b   +        AS              G    PU    PR      .
2c   ,        AS              G    PU    PR      .
2d   -        AS              G    PU    PR      .
2e   .        AS              G    PU    PR      .
2f   /        AS              G    PU    PR      .
30   0  AN    AS   CS      D  G          PR     X.
31   1  AN    AS   CS      D  G          PR     X.
32   2  AN    AS   CS      D  G          PR     X.
33   3  AN    AS   CS      D  G          PR     X.
34   4  AN    AS   CS      D  G          PR     X.
35   5  AN    AS   CS      D  G          PR     X.
36   6  AN    AS   CS      D  G          PR     X.
37   7  AN    AS   CS      D  G          PR     X.
38   8  AN    AS   CS      D  G          PR     X.
39   9  AN    AS   CS      D  G          PR     X.
3a   :        AS              G    PU    PR      .
3b   ;        AS              G    PU    PR      .
3c   <        AS              G    PU    PR      .
3d   =        AS              G    PU    PR      .
3e   >        AS              G    PU    PR      .
3f   ?        AS              G    PU    PR      .
40   @        AS              G    PU    PR      .
41   A  AN  A AS   CS CSF     G          PR  U  X.
42   B  AN  A AS   CS CSF     G          PR  U  X.
43   C  AN  A AS   CS CSF     G          PR  U  X.
44   D  AN  A AS   CS CSF     G          PR  U  X.
45   E  AN  A AS   CS CSF     G          PR  U  X.
46   F  AN  A AS   CS CSF     G          PR  U  X.
47   G  AN  A AS   CS CSF     G          PR  U   .
48   H  AN  A AS   CS CSF     G          PR  U   .
49   I  AN  A AS   CS CSF     G          PR  U   .
4a   J  AN  A AS   CS CSF     G          PR  U   .
4b   K  AN  A AS   CS CSF     G          PR  U   .
4c   L  AN  A AS   CS CSF     G          PR  U   .
4d   M  AN  A AS   CS CSF     G          PR  U   .
4e   N  AN  A AS   CS CSF     G          PR  U   .
4f   O  AN  A AS   CS CSF     G          PR  U   .
50   P  AN  A AS   CS CSF     G          PR  U   .
51   Q  AN  A AS   CS CSF     G          PR  U   .
52   R  AN  A AS   CS CSF     G          PR  U   .
53   S  AN  A AS   CS CSF     G          PR  U   .
54   T  AN  A AS   CS CSF     G          PR  U   .
55   U  AN  A AS   CS CSF     G          PR  U   .
56   V  AN  A AS   CS CSF     G          PR  U   .
57   W  AN  A AS   CS CSF     G          PR  U   .
58   X  AN  A AS   CS CSF     G          PR  U   .
59   Y  AN  A AS   CS CSF     G          PR  U   .
5a   Z  AN  A AS   CS CSF     G          PR  U   .
5b   [        AS              G    PU    PR      .
5c   \        AS              G    PU    PR      .
5d   ]        AS              G    PU    PR      .
5e   ^        AS              G    PU    PR      .
5f   _        AS   CS CSF     G    PU    PR      .
60   `        AS              G    PU    PR      .
61   a  AN  A AS   CS CSF     G  L       PR     X.
62   b  AN  A AS   CS CSF     G  L       PR     X.
63   c  AN  A AS   CS CSF     G  L       PR     X.
64   d  AN  A AS   CS CSF     G  L       PR     X.
65   e  AN  A AS   CS CSF     G  L       PR     X.
66   f  AN  A AS   CS CSF     G  L       PR     X.
67   g  AN  A AS   CS CSF     G  L       PR      .
68   h  AN  A AS   CS CSF     G  L       PR      .
69   i  AN  A AS   CS CSF     G  L       PR      .
6a   j  AN  A AS   CS CSF     G  L       PR      .
6b   k  AN  A AS   CS CSF     G  L       PR      .
6c   l  AN  A AS   CS CSF     G  L       PR      .
6d   m  AN  A AS   CS CSF     G  L       PR      .
6e   n  AN  A AS   CS CSF     G  L       PR      .
6f   o  AN  A AS   CS CSF     G  L       PR      .
70   p  AN  A AS   CS CSF     G  L       PR      .
71   q  AN  A AS   CS CSF     G  L       PR      .
72   r  AN  A AS   CS CSF     G  L       PR      .
73   s  AN  A AS   CS CSF     G  L       PR      .
74   t  AN  A AS   CS CSF     G  L       PR      .
75   u  AN  A AS   CS CSF     G  L       PR      .
76   v  AN  A AS   CS CSF     G  L       PR      .
77   w  AN  A AS   CS CSF     G  L       PR      .
78   x  AN  A AS   CS CSF     G  L       PR      .
79   y  AN  A AS   CS CSF     G  L       PR      .
7a   z  AN  A AS   CS CSF     G  L       PR      .
7b   {        AS              G    PU    PR      .
7c   |        AS              G    PU    PR      .
7d   }        AS              G    PU    PR      .
7e   ~        AS              G    PU    PR      .
7f            AS  C                              .
```

## <a name="see-also"></a>Viz také:

[Klasifikace znaků](../c-runtime-library/character-classification.md)<br/>
[Národní prostředí](../c-runtime-library/locale.md)<br/>
[setlocale, _wsetlocale](../c-runtime-library/reference/setlocale-wsetlocale.md)<br/>
[Výklad sekvencí vícebajtových znaků](../c-runtime-library/interpretation-of-multibyte-character-sequences.md)<br/>
[to – funkce](../c-runtime-library/to-functions.md)
