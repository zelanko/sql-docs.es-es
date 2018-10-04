---
title: FieldEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 204ffb54eb0a48f55d4ec1974b123ed4a0e430be
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741583"
---
# <a name="fieldenum"></a>FieldEnum
Especifica los campos especiales que se hace referenciados en un [registro](../../../ado/reference/ado-api/record-object-ado.md) del objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección.  
  
## <a name="remarks"></a>Comentarios  
 Estas constantes proporcionan un "acceso directo" para obtener acceso a campos especiales asociados con un **registro**. Recuperar el [campo](../../../ado/reference/ado-api/field-object.md) objeto desde el **campos** colección y, a continuación, obtenga su contenido con el **campo** del objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Hace referencia al campo que contiene el valor predeterminado [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto asociado con un **registro**.|  
|**adRecordURL**|-2|Hace referencia al campo que contiene la cadena de dirección URL absoluta para el actual **registro**.|
