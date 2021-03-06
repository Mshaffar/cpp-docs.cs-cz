---
title: CEnumeratorAccessor – třída
ms.date: 11/04/2016
f1_keywords:
- ATL::CEnumeratorAccessor
- CEnumeratorAccessor
- ATL.CEnumeratorAccessor
- CEnumeratorAccessor.m_bIsParent
- ATL::CEnumeratorAccessor::m_bIsParent
- m_bIsParent
- ATL.CEnumeratorAccessor.m_bIsParent
- CEnumeratorAccessor::m_bIsParent
- ATL::CEnumeratorAccessor::m_nType
- CEnumeratorAccessor.m_nType
- CEnumeratorAccessor::m_nType
- ATL.CEnumeratorAccessor.m_nType
- ATL::CEnumeratorAccessor::m_szDescription
- CEnumeratorAccessor.m_szDescription
- CEnumeratorAccessor::m_szDescription
- ATL.CEnumeratorAccessor.m_szDescription
- CEnumeratorAccessor::m_szName
- ATL.CEnumeratorAccessor.m_szName
- ATL::CEnumeratorAccessor::m_szName
- CEnumeratorAccessor.m_szName
- CEnumeratorAccessor::m_szParseName
- ATL::CEnumeratorAccessor::m_szParseName
- m_szParseName
- CEnumeratorAccessor.m_szParseName
- ATL.CEnumeratorAccessor.m_szParseName
helpviewer_keywords:
- CEnumeratorAccessor class
- m_bIsParent
- m_nType
- m_szDescription
- m_szName
- m_szParseName
ms.assetid: 21e8e7ea-3511-4afe-b33f-d520f4ff82bb
ms.openlocfilehash: f238c0b5b2a3988f08d910f605415bbe6403ea3d
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80211820"
---
# <a name="cenumeratoraccessor-class"></a>CEnumeratorAccessor – třída

Používá se v [CEnumerator –](../../data/oledb/cenumerator-class.md) pro přístup k datům ze sady řádků výčtu.

## <a name="syntax"></a>Syntaxe

```cpp
class CEnumeratorAccessor
```

## <a name="requirements"></a>Požadavky

**Záhlaví:** atldbcli. h

## <a name="members"></a>Členové

### <a name="data-members"></a>Datové členy

|||
|-|-|
|[m_bIsParent](#bisparent)|Proměnná, která označuje, zda je enumerátor nadřazeným enumerátorem, pokud je řádek enumerátor.|
|[m_nType](#ntype)|Proměnná, která označuje, zda řádek popisuje zdroj dat nebo enumerátor.|
|[m_szDescription](#szdescription)|Popis zdroje dat nebo čítače výčtu.|
|[m_szName](#szname)|Název zdroje dat nebo čítače výčtu.|
|[m_szParseName](#szparsename)|Řetězec, který se má předat [IParseDisplayName](/windows/win32/api/oleidl/nn-oleidl-iparsedisplayname) a získat moniker pro zdroj dat nebo enumerátor.|

## <a name="remarks"></a>Poznámky

Tato sada řádků se skládá ze zdrojů dat a enumerátorů viditelných z aktuálního enumerátoru.

## <a name="cenumeratoraccessorm_bisparent"></a><a name="bisparent"></a>CEnumeratorAccessor:: m_bIsParent

Proměnná, která označuje, zda je enumerátor nadřazeným enumerátorem, pokud je řádek enumerátor.

### <a name="syntax"></a>Syntaxe

```cpp
VARIANT_BOOL m_bIsParent;
```

### <a name="remarks"></a>Poznámky

Další informace najdete v tématu [ISourcesRowset:: GetSourcesRowset](/previous-versions/windows/desktop/ms711200(v=vs.85)) v *Referenční příručce programátora OLE DB* .

## <a name="cenumeratoraccessorm_ntype"></a><a name="ntype"></a>CEnumeratorAccessor:: m_nType

Proměnná, která označuje, zda řádek popisuje zdroj dat nebo enumerátor.

### <a name="syntax"></a>Syntaxe

```cpp
USHORT m_nType;
```

### <a name="remarks"></a>Poznámky

Další informace najdete v tématu [ISourcesRowset:: GetSourcesRowset](/previous-versions/windows/desktop/ms711200(v=vs.85)) v *Referenční příručce programátora OLE DB* .

## <a name="cenumeratoraccessorm_szdescription"></a><a name="szdescription"></a>CEnumeratorAccessor:: m_szDescription

Popis zdroje dat nebo čítače výčtu.

### <a name="syntax"></a>Syntaxe

```cpp
WCHAR m_szDescription[129];
```

### <a name="remarks"></a>Poznámky

Další informace najdete v tématu [ISourcesRowset:: GetSourcesRowset](/previous-versions/windows/desktop/ms711200(v=vs.85)) v *Referenční příručce programátora OLE DB* .

## <a name="cenumeratoraccessorm_szname"></a><a name="szname"></a>CEnumeratorAccessor:: m_szName

Název zdroje dat nebo čítače výčtu.

### <a name="syntax"></a>Syntaxe

```cpp
WCHAR m_szName[129];
```

### <a name="remarks"></a>Poznámky

Další informace najdete v tématu [ISourcesRowset:: GetSourcesRowset](/previous-versions/windows/desktop/ms711200(v=vs.85)) v *Referenční příručce programátora OLE DB* .

## <a name="cenumeratoraccessorm_szparsename"></a><a name="szparsename"></a>CEnumeratorAccessor:: m_szParseName

Řetězec, který se má předat [IParseDisplayName](/windows/win32/api/oleidl/nn-oleidl-iparsedisplayname) a získat moniker pro zdroj dat nebo enumerátor.

### <a name="syntax"></a>Syntaxe

```cpp
WCHAR m_szParseName[129];
```

### <a name="remarks"></a>Poznámky

Další informace najdete v tématu [ISourcesRowset:: GetSourcesRowset](/previous-versions/windows/desktop/ms711200(v=vs.85)) v *Referenční příručce programátora OLE DB* .

## <a name="see-also"></a>Viz také

[Šablony OLE DB příjemců](../../data/oledb/ole-db-consumer-templates-cpp.md)<br/>
[Referenční dokumentace k šablonám příjemců OLE DB](../../data/oledb/ole-db-consumer-templates-reference.md)
