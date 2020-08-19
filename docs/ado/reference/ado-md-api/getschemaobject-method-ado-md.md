---
description: Método GetSchemaObject (ADO MD)
title: Método GetSchemaObject (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- GetSchemaObject
- Cellset::GetSchemaObject
helpviewer_keywords:
- GetSchemaObject method [ADO MD]
ms.assetid: 36b754b4-6b17-4dd1-a925-bca46938b7c4
author: rothja
ms.author: jroth
ms.openlocfilehash: 19af2bf0e7058a8f483da25c0db926ebc19807c6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441017"
---
# <a name="getschemaobject-method-ado-md"></a>Método GetSchemaObject (ADO MD)
Recupera un objeto de esquema ADO MD ([dimensión](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [jerarquía](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md)o [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md)) por su [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ObjType*  
 Un valor [SchemaObjectTypeEnum](../../../ado/reference/ado-md-api/schemaobjecttypeenum.md) que especifica el tipo de objeto de esquema (dimensión, jerarquía, nivel o miembro) que se va a recuperar.  
  
 *UniqueName*  
 **Cadena** que especifica el valor de la propiedad **UniqueName** del objeto que se va a recuperar.  
  
## <a name="remarks"></a>Observaciones  
 **GetSchemaObject** recupera objetos usando sus nombres únicos, tal como se especifica en la propiedad **UniqueName** . No es necesario conocer los nombres de los objetos primarios y no es necesario rellenar las colecciones primarias para recuperar un objeto de esquema.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
