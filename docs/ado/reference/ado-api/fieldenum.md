---
description: FieldEnum
title: FieldEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2bdcec83c211f71803ea64b7b78f3e6f8c76dee6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973136"
---
# <a name="fieldenum"></a>FieldEnum
Especifica los campos especiales a los que se hace referencia en la colección de [campos](./fields-collection-ado.md) de un objeto de [registro](./record-object-ado.md) .  
  
## <a name="remarks"></a>Observaciones  
 Estas constantes proporcionan un "acceso directo" para obtener acceso a los campos especiales asociados a un **registro**. Recupere el objeto de [campo](./field-object.md) de la colección de **campos** y, a continuación, obtenga su contenido con la propiedad [Value](./value-property-ado.md) del objeto de **campo** .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Hace referencia al campo que contiene el objeto de [secuencia](./stream-object-ado.md) predeterminado asociado a un **registro**.|  
|**adRecordURL**|-2|Hace referencia al campo que contiene la cadena de dirección URL absoluta del **registro**actual.|