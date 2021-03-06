---
title: _invalid_parameter, _invalid_parameter_noinfo, _invalid_parameter_noinfo_noreturn, _invoke_watson
ms.date: 4/2/2020
api_name:
- _invalid_parameter
- _invalid_parameter_noinfo
- _invalid_parameter_noinfo_noreturn
- _invoke_watson
- _o__invalid_parameter_noinfo
- _o__invalid_parameter_noinfo_noreturn
api_location:
- api-ms-win-crt-runtime-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- CORECRT/_invalid_parameter
- _invalid_parameter
- CORECRT/_invalid_parameter_noinfo
- _invalid_parameter_noinfo
- CORECRT/_invalid_parameter_noinfo_noreturn
- _invalid_parameter_noinfo_noreturn
- CORECRT/_invoke_watson
- _invoke_watson
ms.assetid: a4d6f1fd-ce56-4783-8719-927151a7a814
ms.openlocfilehash: 7138e9cb7381e4d40911054e1473536b6e639e2d
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82919823"
---
# <a name="_invalid_parameter-_invalid_parameter_noinfo-_invalid_parameter_noinfo_noreturn-_invoke_watson"></a>_invalid_parameter, _invalid_parameter_noinfo, _invalid_parameter_noinfo_noreturn, _invoke_watson

Tyto funkce používá běhová knihovna jazyka C ke zpracování neplatných parametrů předaných funkcím knihovny CRT. Váš kód může také používat tyto funkce k podpoře výchozího nebo přizpůsobitelného zpracování neplatných parametrů.

## <a name="syntax"></a>Syntaxe

```C
extern "C" void __cdecl
_invalid_parameter(
    wchar_t const* const expression,
    wchar_t const* const function_name,
    wchar_t const* const file_name,
    unsigned int   const line_number,
    uintptr_t      const reserved);

extern "C" void __cdecl
_invalid_parameter_noinfo(void);

extern "C" __declspec(noreturn) void __cdecl
_invalid_parameter_noinfo_noreturn(void);

extern "C" __declspec(noreturn) void __cdecl
_invoke_watson(
    wchar_t const* const expression,
    wchar_t const* const function_name,
    wchar_t const* const file_name,
    unsigned int   const line_number,
    uintptr_t      const reserved);
```

## <a name="parameters"></a>Parametry

*vyjádření*<br/>
Řetězec představující výraz parametru zdrojového kódu, který není platný.

*function_name*<br/>
Název funkce, která se nazývá obslužná rutina.

*file_name*<br/>
Soubor zdrojového kódu, kde byla obslužná rutina volána.

*line_number*<br/>
Číslo řádku ve zdrojovém kódu, kde byla obslužná rutina volána.

*rezervovaný*<br/>
Nepoužívá se.

## <a name="return-value"></a>Návratová hodnota

Tyto funkce nevracejí hodnotu. Funkce **_invalid_parameter_noinfo_noreturn** a **_invoke_watson** se nevrátí volajícímu a v některých případech **_invalid_parameter** a **_invalid_parameter_noinfo** se nemusí vrátit volajícímu.

## <a name="remarks"></a>Poznámky

Když jsou funkce běhové knihovny jazyka C předány neplatným parametrům, funkce knihovny volá *neplatnou obslužnou rutinu parametru*, funkci, která může být určena programátorem k provedení některé z několika věcí. Může například nahlásit problém uživateli, zapsat do protokolu, přerušit ladicí program, ukončit program nebo neprovádět žádné akce. Není-li programátorem určena žádná funkce, je volána výchozí obslužná rutina **_invoke_watson**.

Ve výchozím nastavení, pokud je v kódu ladění identifikován neplatný parametr, funkce knihovny CRT volá funkci **_invalid_parameter** pomocí podrobných parametrů. V kódu bez ladění je volána funkce **_invalid_parameter_noinfo** , která volá funkci **_invalid_parameter** s použitím prázdných parametrů. Pokud funkce knihovny CRT bez ladění vyžaduje ukončení programu, je volána funkce **_invalid_parameter_noinfo_noreturn** , která volá funkci **_invalid_parameter** pomocí prázdných parametrů následovaných voláním funkce **_invoke_watson** pro vynucení ukončení programu.

Funkce **_invalid_parameter** kontroluje, zda byl nastaven uživatelsky definovaný neplatný parametr obslužné rutiny, a pokud ano, zavolá ho. Například pokud uživatelem definovaná obslužná rutina místního vlákna byla nastavena voláním [set_thread_local_invalid_parameter_handler](set-invalid-parameter-handler-set-thread-local-invalid-parameter-handler.md) v aktuálním vlákně, je volána, poté funkce vrátí. V opačném případě, pokud byla uživatelem definovaná obslužná rutina globálního neplatného parametru nastavena voláním [set_invalid_parameter_handler](set-invalid-parameter-handler-set-thread-local-invalid-parameter-handler.md), je volána, funkce vrátí. V opačném případě je volána výchozí obslužná rutina **_invoke_watson** . Výchozím chováním **_invoke_watson** je ukončení programu. Může skončit nebo vracet uživatelsky definované obslužné rutiny. Doporučujeme, aby uživatelsky definované obslužné rutiny ukončily program, pokud není jisté obnovení.

Pokud je volána výchozí obslužná rutina **_invoke_watson** , pokud procesor podporuje operaci [__fastfail](../../intrinsics/fastfail.md) , je vyvolána pomocí parametru **FAST_FAIL_INVALID_ARG** a proces je ukončen. V opačném případě je vyvolána rychlá výjimka selhání, která může být zachycena připojeným ladicím programem. Pokud může proces pokračovat, je ukončen voláním funkce Windows **TerminateProcess** pomocí stavu kódu výjimky **STATUS_INVALID_CRUNTIME_PARAMETER**.

Ve výchozím nastavení je globální stav této funkce vymezen na aplikaci. Pokud ho chcete změnit, přečtěte si téma [globální stav v CRT](../global-state.md).

## <a name="requirements"></a>Požadavky

|Funkce|Požadovaný hlavičkový soubor|
|--------------|------------------|
|**_invalid_parameter**, **_invalid_parameter_noinfo**, **_invalid_parameter_noinfo_noreturn** **_invoke_watson**|\<corecrt. h>|

Další informace o kompatibilitě naleznete v tématu [Kompatibilita](../../c-runtime-library/compatibility.md).

## <a name="see-also"></a>Viz také

[Abecední seznam odkazů na funkce](crt-alphabetical-function-reference.md)<br/>
[_get_invalid_parameter_handler, _get_thread_local_invalid_parameter_handler](get-invalid-parameter-handler-get-thread-local-invalid-parameter-handler.md)<br/>
[_set_invalid_parameter_handler, _set_thread_local_invalid_parameter_handler](set-invalid-parameter-handler-set-thread-local-invalid-parameter-handler.md)<br/>
[Ověřování parametru](../../c-runtime-library/parameter-validation.md)<br/>
