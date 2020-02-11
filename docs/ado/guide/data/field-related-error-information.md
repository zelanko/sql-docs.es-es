---
title: Información de error relacionada con campos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- field-related errors [ADO]
- errors [ADO], field-related
ms.assetid: 5e7b1af4-996b-47c5-9161-c5575ad4fec9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7094c2dba004e35593f5ab11b1162efbdf3283c1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925310"
---
# <a name="field-related-error-information"></a>Información de Error relacionado con el campo
Si un error está relacionado directamente con un campo (por ejemplo, si faltan los datos o si es un tipo incorrecto para el campo), puede recuperar más información sobre la causa del problema examinando la propiedad de **Estado** del objeto de **campo** . Esta propiedad se ha mejorado para proporcionar información específica sobre el problema. Así, por ejemplo, cuando se produce un error en una llamada a **UpdateBatch** , la causa del problema se puede determinar mediante el examen de la propiedad **status** de los **campos** de cada uno de los registros afectados. La propiedad contendrá uno de los valores de la constante **FieldStatusEnum** . En la tabla siguiente se incluyen los valores que son de especial interés cuando se produce un error.  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|Indica que el campo no se puede recuperar ni almacenar sin pérdida de datos.|  
|**adFieldDataOverflow**|6|Indica que los datos devueltos del proveedor han desbordado el tipo de datos del campo.|  
|**adFieldDefault**|13|Indica que se utilizó el valor predeterminado para el campo al establecer los datos.|  
|**adFieldIgnore**|15|Indica que este campo se omitió al establecer los valores de datos en el origen. El proveedor no estableció ningún valor.|  
|**adFieldIntegrityViolation**|10|Indica que el campo no se puede modificar porque es una entidad calculada o derivada.|  
|**adFieldIsNull**|3|Indica que el proveedor devolvió un valor null.|  
|**adFieldOutOfSpace**|22|Indica que el proveedor no puede obtener suficiente espacio de almacenamiento para completar una operación de movimiento o copia.|
