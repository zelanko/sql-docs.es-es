---
description: MemberTypeEnum
title: MemberTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- MemberTypeEnum
helpviewer_keywords:
- MemberTypeEnum enumeration [ADO MD]
ms.assetid: 5d8132c0-7ca2-4f86-8336-1b34213869ad
author: rothja
ms.author: jroth
ms.openlocfilehash: 186ef16dfaafac2151436a3cd63e944de2468457
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777964"
---
# <a name="membertypeenum"></a>MemberTypeEnum
Especifica el valor para la propiedad [Type](./type-property-ado-md.md) de un objeto [miembro](./member-object-ado-md.md) .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adMemberAll**|4|Indica que el objeto **miembro** representa todos los miembros del nivel.|  
|**adMemberFormula**|3|Indica que el objeto **miembro** se calcula mediante una expresión de fórmula.|  
|**adMemberMeasure**|2|Indica que el objeto **miembro** pertenece a la dimensión Measures y representa un atributo cuantitativo.|  
|**adMemberRegular**|1|Predeterminada. Indica que el objeto **miembro** representa una instancia de una entidad comercial.|  
|**adMemberUnknown**|0|No se puede determinar el tipo del miembro.|