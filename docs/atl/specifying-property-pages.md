---
title: Zadání stránek vlastností (ATL)
ms.date: 11/04/2016
helpviewer_keywords:
- ISpecifyPropertyPages method
- property pages, specifying
ms.assetid: ee8678cf-c708-49ab-b0ad-fc2db31f1ac3
ms.openlocfilehash: 47ee0c7d6d2ed464318ab80385ac71cff426a002
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62196558"
---
# <a name="specifying-property-pages"></a>Zadání stránek vlastností

Při vytváření ovládacího prvku ActiveX se často chcete přidružit stránky vlastností, které lze použít k nastavení vlastností ovládacího prvku. Řízení používání kontejnerů `ISpecifyPropertyPages` rozhraní a zjistěte, jaké stránky vlastností je možné nastavit vlastnosti ovládacího prvku. Je potřeba implementovat toto rozhraní ovládacího prvku.

K implementaci `ISpecifyPropertyPages` pomocí knihovny ATL, proveďte následující kroky:

1. Odvodit třídu z [ISpecifyPropertyPagesImpl](../atl/reference/ispecifypropertypagesimpl-class.md).

1. Přidat položku pro `ISpecifyPropertyPages` do vaší třídy modelu COM mapy.

1. Přidat [PROP_PAGE](reference/property-map-macros.md#prop_page) položku do mapy vlastností pro každou stránku přidružený ovládací prvek.

> [!NOTE]
> Při generování standardního ovládacího prvku pomocí [Průvodce ovládacími prvky ATL](../atl/reference/atl-control-wizard.md), pouze je nutné přidat položky PROP_PAGE do mapy vlastností. Průvodce vygeneruje kód nezbytné pro další kroky.

Které jsou v pořádku kontejnery se zobrazí na stránkách vlastností zadané ve stejném pořadí jako PROP_PAGE položky na mapě vlastnost. Obecně byste měli umístit standardní vlastnosti stránky položky po položky pro svoje vlastní stránky v mapě vlastností tak, aby se uživatelům zobrazí na stránkách, které jsou specifické pro váš ovládací prvek nejprve.

## <a name="example"></a>Příklad

Následující třídy pro kalendář používá ovládací prvek `ISpecifyPropertyPages` rozhraní říct kontejnerů, které její vlastnosti lze nastavit pomocí vlastní datum stránky a stránky uložených barvu.

[!code-cpp[NVC_ATL_Windowing#72](../atl/codesnippet/cpp/specifying-property-pages_1.h)]

## <a name="see-also"></a>Viz také:

[Stránky vlastností](../atl/atl-com-property-pages.md)<br/>
[Ukázka ATLPages](../overview/visual-cpp-samples.md)
