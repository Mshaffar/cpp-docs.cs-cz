---
title: _lsearch_s
ms.date: 4/2/2020
api_name:
- _lsearch_s
- _o__lsearch_s
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
- api-ms-win-crt-utility-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _lsearch_s
- lsearch_s
helpviewer_keywords:
- linear searching
- values, searching for
- keys, finding in arrays
- arrays [CRT], searching
- searching, linear
- _lsearch_s function
- lsearch_s function
ms.assetid: d2db0635-be7a-4799-8660-255f14450882
ms.openlocfilehash: d8c421eb3c7a6a617ce073cbf5f36416294c1874
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82920449"
---
# <a name="_lsearch_s"></a>_lsearch_s

Provede lineární hledání hodnoty. Verze [_lsearch](lsearch.md) s vylepšeními zabezpečení, jak je popsáno v [části funkce zabezpečení v CRT](../../c-runtime-library/security-features-in-the-crt.md).

## <a name="syntax"></a>Syntaxe

```C
void *_lsearch_s(
   const void *key,
   void *base,
   unsigned int *num,
   size_t size,
   int (__cdecl *compare)(void *, const void *, const void *),
   void * context
);
```

### <a name="parameters"></a>Parametry

*zkrat*<br/>
Objekt, který chcete vyhledat.

*base*<br/>
Ukazatel na základ pole, které má být prohledáno.

*Automatické*<br/>
Počet elementů.

*hodnota*<br/>
Velikost každého prvku pole v bajtech

*porovnán*<br/>
Ukazatel na srovnávací rutinu. Druhým parametrem je ukazatel na klíč pro hledání. Třetí parametr je ukazatel na prvek pole, který má být porovnán s klíčem.

*souvislost*<br/>
Ukazatel na objekt, který je pravděpodobně k dispozici ve funkci porovnání.

## <a name="return-value"></a>Návratová hodnota

Pokud je *klíč* nalezen, **_lsearch_s** vrátí ukazatel na prvek pole na *bázi Base* , který odpovídá *klíči*. Pokud *klíč* není nalezen, **_lsearch_s** vrátí ukazatel na nově přidanou položku na konci pole.

Pokud jsou funkci předány neplatné parametry, je vyvolána obslužná rutina neplatného parametru, jak je popsáno v tématu [ověřování parametru](../../c-runtime-library/parameter-validation.md). Pokud provádění může pokračovat, pak je **errno** nastaveno na **EINVAL** a funkce vrátí **hodnotu null**. Další informace najdete v tématu [errno, _doserrno, _sys_errlist a _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md).

### <a name="error-conditions"></a>Chybové stavy

|*zkrat*|*base*|*porovnán*|*Automatické*|*hodnota*|**errno**|
|-----------|------------|---------------|-----------|------------|-------------|
|**PLATNOST**|jakýmikoli|jakýmikoli|jakýmikoli|jakýmikoli|**EINVAL**|
|jakýmikoli|**PLATNOST**|jakýmikoli|! = 0|jakýmikoli|**EINVAL**|
|jakýmikoli|jakýmikoli|jakýmikoli|jakýmikoli|nula|**EINVAL**|
|jakýmikoli|jakýmikoli|**PLATNOST**|an|jakýmikoli|**EINVAL**|

## <a name="remarks"></a>Poznámky

Funkce **_lsearch_s** provede lineární hledání *klíč* hodnoty v poli *číselných* prvků, přičemž každý z nich má *šířku* . Na rozdíl **bsearch_s**od bsearch_s **_lsearch_s** nevyžaduje řazení pole. Pokud se *klíč* nenajde, **_lsearch_s** ho přidá na konec pole a zvýší *číslo*.

Funkce *Compare* je ukazatel na uživatelsky zadanou rutinu, která porovná dva prvky pole a vrátí hodnotu určující jejich relaci. Funkce *Compare* také převezme ukazatel na kontext jako první argument. **_lsearch_s** volání *porovnávají* během hledání jednou nebo víckrát a předají ukazatelům na dva prvky pole při každém volání. *porovnání* musí porovnat prvky a pak vracet buď nenulové hodnoty (což znamená, že prvky jsou rozdílné) nebo 0 (což znamená, že prvky jsou identicky).

*Kontextový* ukazatel může být užitečný, pokud je struktura prohledávaných dat součástí objektu a funkce *Compare* potřebuje přístup k členům objektu. Například kód ve funkci *Compare* může přetypovat ukazatel void na příslušný typ objektu a přistupovat ke členům tohoto objektu. Přidání *kontextového* ukazatele zajišťuje **_lsearch_sější** zabezpečení, protože další kontext lze použít k tomu, aby se předešlo Vícenásobný přístup chybám přidruženým k použití statických proměnných k zpřístupnění dat funkci *Compare* .

Ve výchozím nastavení je globální stav této funkce vymezen na aplikaci. Pokud ho chcete změnit, přečtěte si téma [globální stav v CRT](../global-state.md).

## <a name="requirements"></a>Požadavky

|Rutina|Požadovaný hlavičkový soubor|
|-------------|---------------------|
|**_lsearch_s**|\<Hledat. h>|

Další informace o kompatibilitě naleznete v tématu [Kompatibilita](../../c-runtime-library/compatibility.md).

## <a name="see-also"></a>Viz také

[Hledání a řazení](../../c-runtime-library/searching-and-sorting.md)<br/>
[bsearch_s](bsearch-s.md)<br/>
[_lfind_s](lfind-s.md)<br/>
[_lsearch](lsearch.md)<br/>
