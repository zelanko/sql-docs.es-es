---
title: FieldEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1a8533cd43964bf7bd2a456ff2cadce1be00b223
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="fieldenum"></a>FieldEnum
Especifica los campos especiales que se hace referencia en un [registro](../../../ado/reference/ado-api/record-object-ado.md) del objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección.  
  
## <a name="remarks"></a>Comentarios  
 Estas constantes proporcionan "métodos abreviados" para obtener acceso a campos especiales asociados con un **registro**. Recuperar el [campo](../../../ado/reference/ado-api/field-object.md) objeto desde el **campos** colección y, a continuación, obtenga su contenido con el **campo** del objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Hace referencia al campo que contiene el valor predeterminado [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto asociado con un **registro**.|  
|**adRecordURL**|-2|Hace referencia al campo que contiene la cadena de dirección URL absoluta para el actual **registro**.|
