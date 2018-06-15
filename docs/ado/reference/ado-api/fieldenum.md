---
title: FieldEnum | Documentos de Microsoft
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
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c9633fff954251a6a7e1d6153b86ad0b4545b3f
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278671"
---
# <a name="fieldenum"></a>FieldEnum
Especifica los campos especiales que se hace referencia en un [registro](../../../ado/reference/ado-api/record-object-ado.md) del objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección.  
  
## <a name="remarks"></a>Notas  
 Estas constantes proporcionan "métodos abreviados" para obtener acceso a campos especiales asociados con un **registro**. Recuperar el [campo](../../../ado/reference/ado-api/field-object.md) objeto desde el **campos** colección y, a continuación, obtenga su contenido con el **campo** del objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Hace referencia al campo que contiene el valor predeterminado [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto asociado con un **registro**.|  
|**adRecordURL**|-2|Hace referencia al campo que contiene la cadena de dirección URL absoluta para el actual **registro**.|
