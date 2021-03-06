---
title: Přidání třídy z průvodce knihovnou typů
ms.date: 05/09/2019
helpviewer_keywords:
- COM interfaces, adding classes
ms.assetid: 96152afd-9374-4649-a6ab-b0fa2a5592a3
ms.openlocfilehash: 7a866c0e6b772a992f5ae81dbb17646765f172e6
ms.sourcegitcommit: fc1de63a39f7fcbfe2234e3f372b5e1c6a286087
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2019
ms.locfileid: "65708330"
---
# <a name="add-class-from-typelib-wizard"></a>Přidání třídy z průvodce knihovnou typů

::: moniker range="vs-2019"

Tento průvodce není k dispozici v aplikaci Visual Studio 2019 a novějším.

::: moniker-end

::: moniker range="<=vs-2017"

Tohoto průvodce použijte k přidání třídy knihovny MFC z knihovny typů k dispozici. Průvodce vytvoří třídu pro každé rozhraní, kterou přidáte z vybrané knihovny typů.

- **Přidat třídu z:**

   Určuje umístění knihovny typů, ze kterého se vytvoří třídu.

   |Možnost|Popis|
   |------------|-----------------|
   |**Registru**|Knihovna typů je registrován v systému. Zaregistrované knihovny typů jsou uvedeny v **dostupné knihovny typů**.|
   |**File**|Knihovna typů není nutně registrován v systému, ale je obsažena v souboru. Je nutné zadat umístění souborů v **umístění**.|

- **Dostupné knihovny typů**

   Obsahuje knihovny typů, které jsou aktuálně registrované v systému. Vyberte knihovnu typů z tohoto seznamu zobrazíte jeho rozhraní **rozhraní** seznamu.

   Viz "uvnitř Distributed COM: Knihovny typů a jazyk integrace "v knihovně MSDN pro další informace o registraci knihovny typů.

- **Poloha**

   Určuje umístění knihovny typů. Vyberete-li **souboru** pod **přidat třídu z**, můžete uvést umístění souboru, který obsahuje knihovnu typů. Přejděte do umístění souboru, klikněte na tlačítko se třemi tečkami.

- **Rozhraní**

   Seznam rozhraní v aktuálně vybrané v knihovně typů **dostupné knihovny typů** seznamu.

   |Tlačítka převodu|Popis|
   |---------------------|-----------------|
   |**>**|Přidá rozhraní vybrané v **rozhraní** seznamu. Neaktivní, pokud není vybrané žádné rozhraní.|
   |**>>**|Přidá všechna rozhraní v aktuálně vybrané v knihovně typů **dostupné knihovny typů** seznamu.|
   |**\<**|Odebere aktuálně vybranou v třídu **generované třídy** seznamu. Neaktivní, pokud žádná třída je aktuálně vybrána v **generované třídy** seznamu.|
   |**\<\<**|Odebere všechny třídy v **generované třídy** seznamu. Neaktivní if **generované třídy** seznam je prázdný.|

- **Generované třídy**

   Určuje názvy tříd, které mají být vygenerovány z rozhraní přidaných pomocí **>** nebo **>>** tlačítko. Můžete kliknout na toto políčko, aby vyberte třídu a potom použít nahoru nebo dolů kláves procházejte seznam, název každé třídy v zobrazení **třídy** a název souboru v **soubor** pole, Průvodce generuje při můžete Klikněte na tlačítko **Dokončit**. V tomto poli můžete vybrat pouze jednu třídu najednou.

   Třídu můžete odebrat tak, že ji vyberete v tomto seznamu a kliknete na **<**. Není potřeba vybrat třídu do vygenerované třídy pole odebrat všechny třídy; Kliknutím na **<<**, odeberte všechny třídy v **generované třídy** pole.

- **Třída**

   Určuje název třídy vybraný v **generované třídy** pole, které průvodce přidá po kliknutí na **Dokončit**. Můžete upravit název v **třídy** pole.

- **File**

   Nastaví název souboru hlaviček pro novou třídu. Ve výchozím nastavení, tento název je založen na názvu je zadat v **generované třídy**. Klikněte na tlačítko se třemi tečkami uložení názvu souboru do umístění podle vaší volby, nebo připojit k existujícímu souboru deklaraci třídy. Pokud zvolíte existující soubor, Průvodce neuloží se do vybraného umístění dokud kliknutím **Dokončit** v průvodci.

   Průvodce nepřepisuje soubor. Pokud jste vybrali název existujícího souboru, po kliknutí na **Dokončit**, Průvodce vás vyzve k označení, zda by měla být k obsah souboru připojen deklaraci třídy. Klikněte na tlačítko **Ano** pro připojení k souboru, klikněte na tlačítko **ne** pro návrat do průvodce a zadejte jiný název souboru.

::: moniker-end

## <a name="see-also"></a>Viz také:

[Třída knihovny MFC z knihovny typů](../../mfc/reference/adding-an-mfc-class-from-a-type-library.md)<br/>
[Klienti automatizace: Použití knihoven typů](../../mfc/automation-clients-using-type-libraries.md)
