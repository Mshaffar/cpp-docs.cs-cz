---
title: Vlastností okna ATL
ms.date: 11/04/2016
helpviewer_keywords:
- window traits
ms.assetid: c90cf850-9e91-49da-9cf3-ad4efb30347d
ms.openlocfilehash: 29549e54051405fc3dd4d5d7ae70a382ad7a62ea
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62196180"
---
# <a name="understanding-window-traits"></a>Principy vlastností okna

Třídy oken s vlastností poskytují jednoduchý způsob pro standardizaci stylů použitých pro vytvoření objektu ATL okna. Okno vlastností jsou přijímány jako parametry šablony podle [CWindowImpl](../atl/reference/cwindowimpl-class.md) a jiných tříd oken ATL a tak poskytuje výchozí styly oken na úrovni třídy.

Pokud autor instanci okna neposkytuje styly explicitně při volání funkce [vytvořit](../atl/reference/cwindowimpl-class.md#create), třída vlastností můžete použít k zajištění, že v okně stále vytváření správné styly. Dokonce můžete zajistit, že určité styly jsou nastavené pro všechny instance této třídy okna při povolení další styly nastavení na základě jednotlivé instance.

## <a name="atl-window-traits-templates"></a>ATL – okno vlastností šablony

Knihovna ATL poskytuje dvě okna Vlastnosti šablony, které umožňují nastavení výchozích stylů v době kompilace pomocí jejich parametry šablony.

|Třída|Popis|
|-----------|-----------------|
|[Cwintraits –](../atl/reference/cwintraits-class.md)|Tuto šablonu použít, pokud chcete zadat výchozí styly oken, které budou použity pouze v případě, že žádné další styly jsou zadány při volání funkce `Create`. Styly získanou v době běhu přednost styly nastavit v době kompilace.|
|[Cwintraitsor –](../atl/reference/cwintraitsor-class.md)|Tuto třídu používejte, pokud chcete zadat stylů, které musí být vždycky nastavená pro třídu okna. Styly k dispozici v době běhu spolu se styly nastavit v době kompilace pomocí bitového operátoru OR.|

Kromě těchto šablon, knihovna ATL poskytuje řadu předdefinovaných specializace `CWinTraits` šablony pro běžně používané kombinací styly oken. Zobrazit [cwintraits –](../atl/reference/cwintraits-class.md) referenční dokumentaci pro všechny podrobnosti.

## <a name="custom-window-traits"></a>Okno vlastních vlastností

V nepravděpodobné situaci není dostatečná, že specializace jedna z šablony, které poskytuje knihovny ATL a je potřeba vytvořit své vlastní vlastnosti třídy, je třeba pouze vytvořit třídu, která implementuje dvě statické funkce: `GetWndStyle` a `GetWndStyleEx`:

[!code-cpp[NVC_ATL_Windowing#68](../atl/codesnippet/cpp/understanding-window-traits_1.h)]

Každá z těchto funkcí v době běhu, který můžete použít k vytvoření nové hodnoty styl předat některá z hodnot stylu. Pokud vaše třída vlastností okna se používá jako argument šablony pro třídu okna ATL, styl hodnoty předané do těchto statické funkce bude všechno, co byl předán jako argument stylu [vytvořit](../atl/reference/cwindowimpl-class.md#create).

## <a name="see-also"></a>Viz také:

[Třídy oken](../atl/atl-window-classes.md)
