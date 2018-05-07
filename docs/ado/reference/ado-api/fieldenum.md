---
title: FieldEnum | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2d38463ec703335530e33017f77b46cf91c68f0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="fieldenum"></a>FieldEnum
Especifica los campos especiales que se hace referencia en un [registro](../../../ado/reference/ado-api/record-object-ado.md) del objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección.  
  
## <a name="remarks"></a>Comentarios  
 Estas constantes proporcionan "métodos abreviados" para obtener acceso a campos especiales asociados con un **registro**. Recuperar el [campo](../../../ado/reference/ado-api/field-object.md) objeto desde el **campos** colección y, a continuación, obtenga su contenido con el **campo** del objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Hace referencia al campo que contiene el valor predeterminado [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto asociado con un **registro**.|  
|**adRecordURL**|-2|Hace referencia al campo que contiene la cadena de dirección URL absoluta para el actual **registro**.|
