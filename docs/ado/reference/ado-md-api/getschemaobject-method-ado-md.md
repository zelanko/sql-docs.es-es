---
title: Método GetSchemaObject (ADO MD) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- GetSchemaObject
- Cellset::GetSchemaObject
helpviewer_keywords:
- GetSchemaObject method [ADO MD]
ms.assetid: 36b754b4-6b17-4dd1-a925-bca46938b7c4
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3068635d252b4c79f08bc88102796f0fc85a1315
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35283874"
---
# <a name="getschemaobject-method-ado-md"></a>Método GetSchemaObject (ADO MD)
Recupera un objeto de esquema de ADO MD ([dimensión](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [jerarquía](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md), o [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md)) por su [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ObjType*  
 A [SchemaObjectTypeEnum](../../../ado/reference/ado-md-api/schemaobjecttypeenum.md) valor que especifica el tipo de objeto de esquema (dimensión, jerarquía, nivel o miembro) para recuperar.  
  
 *UniqueName*  
 A **cadena** especificando la **UniqueName** valor de propiedad de objeto que se va a recuperar.  
  
## <a name="remarks"></a>Notas  
 **GetSchemaObject** recupera objetos mediante sus nombres únicos, según lo especificado por el **UniqueName** propiedad. No es necesario conocer los nombres de los objetos primarios y colecciones de elementos primarios no es necesario que se debe rellenar para recuperar un objeto de esquema.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
