---
title: Elementos secundarios (propiedad, ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Children
- Children
helpviewer_keywords:
- Children property [ADO MD]
ms.assetid: 61d36468-1ccd-467a-9cb5-17d0bfacc766
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f489a87573dabbd091f5d2dce8a084b53cc5771e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62653541"
---
# <a name="children-property-ado-md"></a>Los elementos secundarios (propiedad, ADO MD)
Devuelve un [miembros](../../../ado/reference/ado-md-api/members-collection-ado-md.md) colección para el que actual [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) es la entidad primaria en la jerarquía.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **miembros** colección y es de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 El **hijos** propiedad contiene un **miembros** colección para el que actual **miembro** es el elemento primario jerárquico. Nivel de hoja **miembro** objetos no tienen elementos secundarios el **miembros** colección. Esta propiedad solo se admite en **miembro** objetos que pertenecen a un [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md) objeto. Se produce un error cuando se hace referencia a esta propiedad desde **miembro** objetos que pertenecen a un [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad ChildCount (ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
