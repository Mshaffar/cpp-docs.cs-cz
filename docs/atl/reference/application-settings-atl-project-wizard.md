---
title: Nastavení aplikace, Průvodce projektem ATL
ms.date: 11/04/2016
f1_keywords:
- vc.appwiz.atl.com.appset
helpviewer_keywords:
- ATL Project Wizard, application settings
ms.assetid: d48c9fc5-f439-49fd-884c-8bcfa7d52991
ms.openlocfilehash: bd9d5c6ef1ccb86f2968b1e2d2706092b6db45e9
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62248997"
---
# <a name="application-settings-atl-project-wizard"></a>Nastavení aplikace, Průvodce projektem ATL

Použití **nastavení aplikace** stránky Průvodce projektem ATL pro návrh a přidat do nového projektu ATL základní funkce.

## <a name="server-type"></a>Typ serveru

Vyberte jednu ze tří typů serveru:

- **Dynamická knihovna (DLL)**

   Vyberte vytvoření serveru v rámci procesu.

- **Spustitelný soubor (EXE)**

   Vyberte pro vytvoření místního serveru mimo proces. Tato možnost není povolena podpora knihovny MFC nebo knihovny modelu COM + 1.0. Nepovoluje se sloučení kódu proxy/zástupné procedury.

- **Služby (EXE)**

   Vyberte vytvořit aplikaci Windows, která běží na pozadí při spuštění Windows. Tuto možnost nelze povolit podporu pro knihovny MFC nebo knihovny modelu COM + 1.0 nebo neumožňuje sloučení kódu proxy/zástupné procedury.

## <a name="additional-options"></a>Další možnosti

> [!NOTE]
> Všechny další možnosti jsou k dispozici pro pouze projekty knihovny DLL.

- **Sloučení kódu proxy/zástupné procedury**

   Vyberte **sloučení kódu proxy/zástupné procedury** zaškrtávací políčko v zájmu usnadnění práce při zařazování rozhraní je povinný. Tato možnost umístí MIDL generovaný proxy a zástupných procedur kód v rámci stejného spustitelného souboru jako server.

- **Podpora knihovny MFC**

   Vyberte, chcete-li určit, že váš objekt zahrnuje podporu knihovny MFC. Tato možnost propojí vaše projekty pro knihovny MFC, které můžete přístup k některé z třídy a funkce, které obsahují.

- **Podpora COM + 1.0**

   Vyberte, chcete-li změnit nastavení projektu sestavení pro podporu komponenty modelu COM + 1.0. Kromě standardní seznamu knihoven průvodce přidá comsvcs.lib knihovny specifické pro komponenty modelu COM + 1.0

   Kromě toho knihovna mtxex.dll zpožděné načtení v hostitelském systému, když je aplikace spuštěna.

- **Podpora registrátora komponent**

   Pokud váš projekt knihovny ATL obsahuje podporu pro komponenty modelu COM + 1.0, můžete nastavit tuto možnost. Registrátora komponent umožňuje váš objekt modelu COM + 1.0 mohl získat seznam součástí, zaregistrovat součásti nebo zrušit registraci součásti (jednotlivě nebo celou najednou).

## <a name="see-also"></a>Viz také:

[Průvodce projektem ATL](../../atl/reference/atl-project-wizard.md)<br/>
[Vytvoření projektu ATL](../../atl/reference/creating-an-atl-project.md)<br/>
[Výchozí konfigurace projektu ATL](../../atl/reference/default-atl-project-configurations.md)
