---
title: FieldEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: FieldEnum
helpviewer_keywords: FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 10555100d93b931f3b07c2118cf70556171ba831
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="fieldenum"></a>FieldEnum
Especifica los campos especiales que se hace referencia en un [registro](../../../ado/reference/ado-api/record-object-ado.md) del objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección.  
  
## <a name="remarks"></a>Comentarios  
 Estas constantes proporcionan "métodos abreviados" para obtener acceso a campos especiales asociados con un **registro**. Recuperar el [campo](../../../ado/reference/ado-api/field-object.md) objeto desde el **campos** colección y, a continuación, obtenga su contenido con el **campo** del objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Hace referencia al campo que contiene el valor predeterminado [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto asociado con un **registro**.|  
|**adRecordURL**|-2|Hace referencia al campo que contiene la cadena de dirección URL absoluta para el actual **registro**.|
