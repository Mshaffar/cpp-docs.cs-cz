---
title: Typy zpráv přidružených k objektům uživatelského rozhraní
ms.date: 11/04/2016
f1_keywords:
- vc.codewiz.uiobject.msgs
helpviewer_keywords:
- message types and user interface objects [MFC]
ms.assetid: 681ee1a7-f6e6-4ea0-9fc6-1fb53a35516e
ms.openlocfilehash: 37638d12c65986d40e7df9f0fbfdef4b8207e418
ms.sourcegitcommit: 65ed563a8a1d4d90f872a2a6edcb086f84ec9f77
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2019
ms.locfileid: "66741578"
---
# <a name="message-types-associated-with-user-interface-objects"></a>Typy zpráv přidružených k objektům uživatelského rozhraní

V následující tabulce jsou uvedeny typy objektů, se kterými pracujete a typy zpráv přidružených k jejich.

### <a name="user-interface-objects-and-associated-messages"></a>Objekty uživatelského rozhraní a přidružených zpráv

|ID objektu|Zprávy|
|---------------|--------------|
|Název třídy, představující obsahujícího okna|Zprávy Windows [CWnd](../../mfc/reference/cwnd-class.md)-odvozené třídy: dialogové okno, okna, podřízené okno, podřízené okno MDI nebo nejvyššího rámce okna.|
|Identifikátor nabídky nebo akcelerátoru|– Zpráva příkaz (spustí program funkce).<br />-UPDATE_COMMAND_UI zpráva (dynamicky aktualizuje položku nabídky).|
|Identifikátor ovládacího prvku|Zpráv s oznámením ovládacího prvku pro vybraný typ ovládacího prvku.|

## <a name="see-also"></a>Viz také:

[Mapování zpráv na funkce](../../mfc/reference/mapping-messages-to-functions.md)<br/>
[Přidání funkce pomocí Průvodců kódem](../../ide/adding-functionality-with-code-wizards-cpp.md)<br/>
[Přidání třídy](../../ide/adding-a-class-visual-cpp.md)<br/>
[Přidání členské funkce](../../ide/adding-a-member-function-visual-cpp.md)<br/>
[Přidání členské proměnné](../../ide/adding-a-member-variable-visual-cpp.md)<br/>
[Přepisování virtuální funkce](../../ide/overriding-a-virtual-function-visual-cpp.md)<br/>
[Popisovače zpráv knihovny MFC](../../mfc/reference/adding-an-mfc-message-handler.md)<br/>
[Navigace strukturou třídy](../../ide/navigate-code-cpp.md)
