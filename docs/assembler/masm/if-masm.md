---
title: IF (MASM)
ms.date: 12/17/2019
helpviewer_keywords:
- IF directive
ms.assetid: 82e43712-4f0c-4bf6-90ce-0663e81af707
ms.openlocfilehash: 6e63f5c8075b3c94370ad8863d224c097cf0ecdf
ms.sourcegitcommit: 63784729604aaf526de21f6c6b62813882af930a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/17/2020
ms.locfileid: "79440746"
---
# <a name="if"></a>IF

Udělí sestavení *ifstatements* , je-li hodnota *expression1* true (nenulová) nebo *elseifstatements* , pokud je hodnota *Výraz1* false (0) a vlastnost *Výraz2* je true.

## <a name="syntax"></a>Syntaxe

> **If** *Výraz1*\
> *příkazy if*\
> ⟦**ElseIf** *Výraz2*\
> *ElseIf-příkazy*⟧ \
> ⟦**ELSE**\
> *else-příkazy*⟧ \
> **ENDIF**

## <a name="remarks"></a>Poznámky

Pro [ElseIf](elseif-masm.md): **ELSEIFB**, **elseifdef –** , **ELSEIFDIF**, **ELSEIFDIFI**, **ELSEIFE**, **ELSEIFIDN**, **ELSEIFIDNI**, **ELSEIFNB**a **elseifndef –** mohou být nahrazeny následující direktivy. Volitelně sestaví *Další příkazy* , pokud je předchozí výraz nepravdivý. Všimněte si, že výrazy jsou vyhodnocovány v době sestavení.

## <a name="see-also"></a>Viz také

\ – [referenční informace o direktivách](directives-reference.md)
[Gramatika BNF MASM](masm-bnf-grammar.md)
