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
ms.openlocfilehash: b0a54b02cf748d8ff1144e50e3531295dbfe8c55
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778124"
---
# <a name="getschemaobject-method-ado-md"></a>Método GetSchemaObject (ADO MD)
Recupera un objeto de esquema ADO MD ([dimensión](./dimension-object-ado-md.md), [jerarquía](./hierarchy-object-ado-md.md), [nivel](./level-object-ado-md.md)o [miembro](./member-object-ado-md.md)) por su [UniqueName](./uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ObjType*  
 Un valor [SchemaObjectTypeEnum](./schemaobjecttypeenum.md) que especifica el tipo de objeto de esquema (dimensión, jerarquía, nivel o miembro) que se va a recuperar.  
  
 *UniqueName*  
 **Cadena** que especifica el valor de la propiedad **UniqueName** del objeto que se va a recuperar.  
  
## <a name="remarks"></a>Observaciones  
 **GetSchemaObject** recupera objetos usando sus nombres únicos, tal como se especifica en la propiedad **UniqueName** . No es necesario conocer los nombres de los objetos primarios y no es necesario rellenar las colecciones primarias para recuperar un objeto de esquema.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto CubeDef (ADO MD)](./cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [Objeto CubeDef (ADO MD)](./cubedef-object-ado-md.md)