---
title: Asynchronní agenti
ms.date: 11/19/2018
helpviewer_keywords:
- asynchronous agents
- agents [Concurrency Runtime]
ms.assetid: 6cf6ccc6-87f1-4e14-af15-ea8ba58fef1a
ms.openlocfilehash: ff6fa851519066c3c399a28557fd8f103d0e94be
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62412807"
---
# <a name="asynchronous-agents"></a>Asynchronní agenti

*Asynchronní agent* (nebo jen *agenta*) je součástí aplikace, která funguje asynchronně pomocí jiných agentů k řešení větší výpočetní úlohy. Agenta můžete představit jako úlohu, která se má nastavit životního cyklu. Například jeden agent může číst data z vstupně výstupní zařízení (například klávesnici, soubor na disku nebo připojení k síti) a jiného agenta může provádět akce na těchto datech, jakmile je k dispozici. První agent používá předávání zpráv informovat druhou agenta, že je k dispozici další data. Plánovač Concurrency Runtime poskytuje efektivní mechanismus pro povolení agentů blokovat a yield kooperativně bez nutnosti přerušení méně efektivní.

Knihovna agentů definuje [concurrency::agent](../../parallel/concrt/reference/agent-class.md) třídy představující asynchronní agent. `agent` je abstraktní třída, která deklaruje virtuální metodu [concurrency::agent::run](reference/agent-class.md#run). `run` Metoda spustí úloha, která je prováděné tímto agentem. Protože `run` je abstraktní, je nutné implementovat tuto metodu v každé třídy, která jsou odvozeny z `agent`.

## <a name="agent-life-cycle"></a>Agent životního cyklu

Agenta došlo k nastavení životního cyklu. [Concurrency::agent_status](reference/concurrency-namespace-enums.md#agent_status) výčet definuje různé stavy agenta. Na následujícím obrázku je diagram stavu, který ukazuje, jak agenty průběhu z jednoho stavu do druhého. Na tomto obrázku pevné řádky představují metody, které je možné volat z aplikace; tečkované čáry představují metody, které jsou volány z modulu runtime.

![Diagram stavu agenta](../../parallel/concrt/media/agentstate.png "Diagram stavu agenta")

Následující tabulka popisuje každý stav v `agent_status` výčtu.

|Stav agenta|Popis|
|-----------------|-----------------|
|`agent_created`|Agent nebyl naplánován ke spuštění.|
|`agent_runnable`|Modul runtime je plánování agenta pro spuštění.|
|`agent_started`|Agent byla spuštěna a je spuštěná.|
|`agent_done`|Agenta se dokončila.|
|`agent_canceled`|Agent byla zrušena dříve, než je zadaný `started` stavu.|

`agent_created` je počáteční stav agenta, `agent_runnable` a `agent_started` jsou aktivní stavy a `agent_done` a `agent_canceled` jsou státy, terminálu.

Použití [concurrency::agent::status](reference/agent-class.md#status) metody k získání aktuálního stavu `agent` objektu. I když `status` metoda je bezpečná pro souběžnost, stav agenta můžete změnit čas `status` metoda vrátí hodnotu. Například může být agenta v `agent_started` stavu při volání `status` metoda, ale přesunuta do `agent_done` hned za stavu `status` metoda vrátí hodnotu.

## <a name="methods-and-features"></a>Metody a funkce

V následující tabulce jsou uvedeny některé důležité metody, které patří do `agent` třídy. Další informace o všech `agent` metod najdete v tématu [agent – třída](../../parallel/concrt/reference/agent-class.md).

|Metoda|Popis|
|------------|-----------------|
|[start](reference/agent-class.md#start)|Plány `agent` objekt pro provedení a nastaví ji `agent_runnable` stavu.|
|[Spuštění](reference/agent-class.md#run)|Úloha, která se má provést pomocí provádí `agent` objektu.|
|[Hotovo](reference/agent-class.md#done)|Přesune agenta, aby `agent_done` stavu.|
|[Zrušit](../../parallel/concrt/cancellation-in-the-ppl.md#cancel)|Pokud agenta nebyla spuštěna, tato metoda zruší spuštění agenta a nastaví na `agent_canceled` stavu.|
|[status](reference/agent-class.md#status)|Načte aktuální stav `agent` objektu.|
|[Počkej](reference/agent-class.md#wait)|Čeká `agent` objektu k zadání `agent_done` nebo `agent_canceled` stavu.|
|[wait_for_all](reference/agent-class.md#wait_for_all)|Čeká na všechny zadané `agent` objekty k zadání `agent_done` nebo `agent_canceled` stavu.|
|[wait_for_one](reference/agent-class.md#wait_for_one)|Čeká na nejméně jednoho ze zadaných `agent` objekty k zadání `agent_done` nebo `agent_canceled` stavu.|

Po vytvoření objektu agenta volání [concurrency::agent::start](reference/agent-class.md#start) metoda ji naplánovat na spuštění. Modul runtime zavolá `run` metoda po naplánuje agenta a nastaví ji na `agent_runnable` stavu.

Modul runtime nedokáže spravovat výjimky, které jsou vyvolány asynchronních agentů. Další informace o zpracování výjimek a agentů najdete v tématu [zpracování výjimek](../../parallel/concrt/exception-handling-in-the-concurrency-runtime.md).

## <a name="example"></a>Příklad

Příklad, který ukazuje, jak vytvořit základní aplikaci založené na agentovi, naleznete v tématu [názorný postup: Vytvoření aplikace založené na agentovi](../../parallel/concrt/walkthrough-creating-an-agent-based-application.md).

## <a name="see-also"></a>Viz také:

[Knihovna asynchronních agentů](../../parallel/concrt/asynchronous-agents-library.md)
