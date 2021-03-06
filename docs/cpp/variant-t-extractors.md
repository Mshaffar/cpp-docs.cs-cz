---
title: _variant_t – extraktory
ms.date: 11/04/2016
f1_keywords:
- _variant_t.operatordouble
- operatorlong
- _variant_t::operator_bstr_t
- operatordouble
- _variant_t.operatorCY
- operatorCY
- _variant_t::operatorCY
- _variant_t::operatordouble
- operatorfloat
- operatorBYTE
- _variant_t.operatorDECIMAL
- _variant_t::operatorlong
- operatorIDispatch
- _variant_t.operatorBYTE
- operatorDECIMAL
- _variant_t.operator_bstr_t
- _variant_t::operatorDECIMAL
- _variant_t.operatorIUnknown
- _variant_t.operatorlong
- _variant_t::operatorIDispatch
- _variant_t::operatorIUnknown
- operatorIUnknown
- _variant_t.operatorbool
- _variant_t::operatorBYTE
- _variant_t.operatorfloat
- operator_bstr_t
- _variant_t::operatorbool
- operatorshort
- _variant_t::operatorshort
- _variant_t::operatorfloat
- _variant_t.operatorIDispatch
- _variant_t.operatorshort
helpviewer_keywords:
- extractors, _variant_t class
- operator CY
- operator IDispatch
- operator SHORT
- operator double
- operator long
- operator _bstr_t
- operator DECIMAL
- operator float
- operator bool
- operator BYTE
- operator IUnknown
ms.assetid: 33c1782f-045a-4673-9619-1d750efc83a9
ms.openlocfilehash: 685df7285e58e0cf2ceeded5ac27641364897298
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80187697"
---
# <a name="_variant_t-extractors"></a>_variant_t – extraktory

**Specifické pro společnost Microsoft**

Extrahuje data ze zapouzdřeného objektu `VARIANT`.

## <a name="syntax"></a>Syntaxe

```
operator short( ) const;
operator long( ) const;
operator float( ) const;
operator double( ) const;
operator CY( ) const;
operator _bstr_t( ) const;
operator IDispatch*( ) const;
operator bool( ) const;
operator IUnknown*( ) const;
operator DECIMAL( ) const;
operator BYTE( ) const;
operator VARIANT() const throw();
operator char() const;
operator unsigned short() const;
operator unsigned long() const;
operator int() const;
operator unsigned int() const;
operator __int64() const;
operator unsigned __int64() const;
```

## <a name="remarks"></a>Poznámky

Extrahuje nezpracovaná data ze zapouzdřených `VARIANT`. Pokud `VARIANT` ještě není správného typu, `VariantChangeType` se použije k pokusu o převod a při selhání se vygeneruje chyba:

- **short – operátor ()** Extrahuje **krátkou** celočíselnou hodnotu.

- **Long – operátor ()** Extrahuje **dlouhé** celočíselné hodnoty.

- **Operator float () – operátor** Extrahuje číselnou hodnotu **typu float** .

- **Double – operátor ()** Extrahuje **dvojitou** celočíselnou hodnotu.

- **Operator CY () – operátor** Extrahuje objekt `CY`.

- **bool – operátor ()** Extrahuje **logickou** hodnotu.

- **Decimal – operátor ()** Extrahuje `DECIMAL`ou hodnotu.

- **Byte – operátor ()** Extrahuje `BYTE`ou hodnotu.

- **operátor _bstr_t ()** Extrahuje řetězec, který je zapouzdřený v objektu `_bstr_t`.

- **operátor IDispatch\*()** Extrahuje ukazatel odesílajícího rozhraní ze zapouzdřeného `VARIANT`. `AddRef` se volá na výsledný ukazatel, takže je k dispozici pro volání `Release` k uvolnění.

- **operátor IUnknown\*()** Extrahuje ukazatel rozhraní modelu COM ze zapouzdřeného `VARIANT`. `AddRef` se volá na výsledný ukazatel, takže je k dispozici pro volání `Release` k uvolnění.

**Specifické pro konec Microsoftu**

## <a name="see-also"></a>Viz také

[_variant_t – třída](../cpp/variant-t-class.md)
