---
title: Okna s rámečkem
ms.date: 11/19/2018
helpviewer_keywords:
- document frame windows [MFC]
- windows [MFC], MDI
- window classes [MFC], frame
- single document interface (SDI) [MFC]
- single document interface (SDI) [MFC], frame windows
- views [MFC], and frame windows
- CFrameWnd class [MFC], frame windows
- frame windows [MFC]
- frame windows [MFC], about frame windows
- MFC, frame windows
- MDI [MFC], frame windows
- splitter windows [MFC], and frame windows
ms.assetid: 40677339-8135-4f5e-aba6-3fced3078077
ms.openlocfilehash: 939230753f25db38e6ba2f26340f40ddf74d23bf
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62219828"
---
# <a name="frame-windows"></a>Okna s rámečkem

Pokud je aplikace spuštěna v rámci Windows, kterou uživatel komunikuje dokumenty, které jsou zobrazeny v oken s rámečkem. Okno rámce dokumentu tvoří dvě hlavní součásti: rámce a obsah, který ho snímků. Okno rámce dokumentu může být [rozhraní jednoho dokumentu](../mfc/sdi-and-mdi.md) okno rámce (SDI) nebo [rozhraní více dokumentů](../mfc/sdi-and-mdi.md) podřízené okno (MDI). Windows spravuje většinu interakce uživatele s oknem rámce: přesunutí a mění velikost okna, zavření a minimalizace a maximalizuje ho. Můžete spravovat obsah uvnitř rámečku.

## <a name="frame-windows-and-views"></a>Zobrazení a rámečku Windows

Rozhraní MFC používá tak, aby obsahovala zobrazení oken s rámečkem. Dvě komponenty – rámce a obsah, jsou reprezentovány a spravuje dvěma různými třídami v knihovně MFC. Třídy oken s rámečkem spravuje rámce a zobrazit třídu spravuje obsah. V okně zobrazení je podřízeným oknem rámce. Vykreslování a další interakce uživatele s dokumentem probíhat v klientské oblasti zobrazení, nikoli klientské oblasti okna rámce. Okno rámce poskytuje viditelná rámeček kolek zobrazení, včetně záhlaví a standardní okno Ovládací prvky, jako je například ovládací prvek nabídky, tlačítka Minimalizovat a maximalizujte okno a ovládací prvky pro změnu velikosti okna. "Obsah" skládají z klientské oblasti okna, plně obsazenou podřízené okno – zobrazení. Následující obrázek ukazuje vztah mezi okno rámce a zobrazení.

![Rámeček okna zobrazení](../mfc/media/vc37fx1.gif "rámec okna zobrazení") <br/>
Okno rámce a zobrazení

## <a name="frame-windows-and-splitter-windows"></a>Rámce Windows a Windows rozdělovač

Další běžné uspořádání je okno rámce jak výklad více zobrazení, obvykle pomocí [okno s rozdělovačem](../mfc/multiple-document-types-views-and-frame-windows.md). V okně rozdělovač klientské oblasti okna rámce je obsazena rozděleného okna, která naopak má více podřízených oken, volá podoken, které jsou zobrazení.

### <a name="what-do-you-want-to-know-more-about"></a>Co chcete zjistit více informací

**Hlavní okno rámce témata**

- [Objekty oken](../mfc/window-objects.md)

- [Třídy oken s rámečkem](../mfc/frame-window-classes.md)

- [Třídy oken s rámečkem vytvořené průvodcem aplikací](../mfc/frame-window-classes-created-by-the-application-wizard.md)

- [Styly oken rámce](../mfc/frame-window-styles-cpp.md)

- [Co dělat oken s rámečkem](../mfc/what-frame-windows-do.md)

**Témata týkající se použití rámce Windows**

- [Použití oken s rámečkem](../mfc/using-frame-windows.md)

- [Vytváření oken s rámečkem v dokumentu](../mfc/creating-document-frame-windows.md)

- [Zničení oken s rámečkem](../mfc/destroying-frame-windows.md)

- [Správa podřízených oken MDI](../mfc/managing-mdi-child-windows.md)

- [Správa aktuálního zobrazení](../mfc/managing-the-current-view.md) v okně rámce, který obsahuje více než jedno zobrazení

- [Správa nabídek, ovládacích pruhů a akcelerátorů (jiné objekty, které sdílet místa okno rámce)](../mfc/managing-menus-control-bars-and-accelerators.md)

**Témata týkající se možností speciální rámce okna**

- [Přetahování souborů](../mfc/dragging-and-dropping-files-in-a-frame-window.md) z Průzkumníka souborů nebo Správce souborů v okně s rámečkem

- [Odpověď na dynamickou výměnu dat (DDE)](../mfc/responding-to-dynamic-data-exchange-dde.md)

- [Semimodální stavy: Kontextová nápověda Windows (Orchestrace dalších akcí okna)](../mfc/orchestrating-other-window-actions.md)

- [Semimodální stavy: tisku a tiskového náhledu (Orchestrace dalších akcí okna)](../mfc/orchestrating-other-window-actions.md)

**Témata týkající se jiných typů Windows**

- [Použití zobrazení](../mfc/using-views.md)

- [Dialogová okna](../mfc/dialog-boxes.md)

- [Ovládací prvky](../mfc/controls-mfc.md)

## <a name="see-also"></a>Viz také:

[Windows](../mfc/windows.md)
