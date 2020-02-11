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
ms.openlocfilehash: 5fe89d90510e95468e18b0d744ff566f69654320
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932682"
---
# <a name="fieldenum"></a>FieldEnum
Especifica los campos especiales a los que se hace referencia en la colección de [campos](../../../ado/reference/ado-api/fields-collection-ado.md) de un objeto de [registro](../../../ado/reference/ado-api/record-object-ado.md) .  
  
## <a name="remarks"></a>Observaciones  
 Estas constantes proporcionan un "acceso directo" para obtener acceso a los campos especiales asociados a un **registro**. Recupere el objeto de [campo](../../../ado/reference/ado-api/field-object.md) de la colección de **campos** y, a continuación, obtenga su contenido con la propiedad [Value](../../../ado/reference/ado-api/value-property-ado.md) del objeto de **campo** .  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Hace referencia al campo que contiene el objeto de [secuencia](../../../ado/reference/ado-api/stream-object-ado.md) predeterminado asociado a un **registro**.|  
|**adRecordURL**|-2|Hace referencia al campo que contiene la cadena de dirección URL absoluta del **registro**actual.|
