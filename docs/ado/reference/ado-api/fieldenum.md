---
description: FieldEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: cad540a13fbad480f795049df0d0150188df4283
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775454"
---
# <a name="fieldenum"></a>FieldEnum
Especifica los campos especiales a los que se hace referencia en la colección de [campos](./fields-collection-ado.md) de un objeto de [registro](./record-object-ado.md) .  
  
## <a name="remarks"></a>Observaciones  
 Estas constantes proporcionan un "acceso directo" para obtener acceso a los campos especiales asociados a un **registro**. Recupere el objeto de [campo](./field-object.md) de la colección de **campos** y, a continuación, obtenga su contenido con la propiedad [Value](./value-property-ado.md) del objeto de **campo** .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Hace referencia al campo que contiene el objeto de [secuencia](./stream-object-ado.md) predeterminado asociado a un **registro**.|  
|**adRecordURL**|-2|Hace referencia al campo que contiene la cadena de dirección URL absoluta del **registro**actual.|