---
title: Platform::disconnectedexception – třída
ms.date: 12/30/2016
ms.topic: reference
f1_keywords:
- VCCORLIB/Platform::DisconnectedException
- VCCORLIB/Platform::DisconnectedException::DisconnectedException
helpviewer_keywords:
- Platform::DisconnectedException
ms.assetid: c25e0d64-5bff-4c21-88e5-c4ec2776fa7f
ms.openlocfilehash: 56276a7d09cc82e05886c2c67a4784993083adb5
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62387614"
---
# <a name="platformdisconnectedexception-class"></a>Platform::disconnectedexception – třída

Vyvolána, když se pokusí odkazovat na server COM, který již existuje objekt proxy modelu COM

## <a name="syntax"></a>Syntaxe

```
public ref class DisconnectedException : COMException,    IException,    IPrintable,    IEquatable
```

### <a name="remarks"></a>Poznámky

Když třídy A odkazy na jiné třídy (třídy B), který je v samostatném procesu, třídy A vyžaduje objekt proxy pro komunikaci se serverem COM mimo proces, který obsahuje třídu B. Někdy přejít na serveru nedostatek paměti bez třídy znalosti o něm. V takovém případě je vyvolána výjimka RPC_E_DISCONNECTED a získá přeložit na Platform::disconnectedexception –. Jeden scénář, ve kterém je, vyvolá se při zdroje událostí vyvolá delegáta, který byl předán, ale delegáta zlikvidování v určitém okamžiku po odběru přihlásili k této události. Pokud k tomu dojde, zdroj události tohoto delegátu zruší jeho vyvolávacím seznamu.

Další informace najdete v tématu [COMException](../cppcx/platform-comexception-class.md) třídy.

### <a name="requirements"></a>Požadavky

**Minimální podporovaná klienta:** Windows 8

**Minimální podporovaná serveru:** Windows Server 2012

**Namespace:** Platforma

**Metadata:** platform.winmd

## <a name="see-also"></a>Viz také:

[Platform::COMException – třída](../cppcx/platform-comexception-class.md)
