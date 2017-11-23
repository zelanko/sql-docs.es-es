---
title: "Información de Error relacionado con el campo | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- field-related errors [ADO]
- errors [ADO], field-related
ms.assetid: 5e7b1af4-996b-47c5-9161-c5575ad4fec9
caps.latest.revision: "4"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d37d91f2b35cf211044f2ac1f2bf8705bbc1ef16
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="field-related-error-information"></a>Información de Error relacionado con el campo
Si un error está directamente relacionado con un campo, por ejemplo, si los datos no se encuentra o si es del tipo correcto para el campo, puede recuperar más información sobre la causa del problema examinando la **campo** del objeto **estado**  propiedad. Esta propiedad se ha mejorado para proporcionar información específica acerca del problema. Así, por ejemplo, cuando una llamada a **UpdateBatch** se produce un error, la causa del problema se puede determinar examinando la **estado** propiedad de la **campos** en cada uno de los afectados registros. La propiedad contendrá uno de los valores en el **FieldStatusEnum** constante. En la tabla siguiente incluye los valores que son de especial interés cuando se produce un error.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|Indica que el campo no se puede recuperar ni almacenar sin pérdida de datos.|  
|**adFieldDataOverflow**|6|Indica que los datos devueltos por el proveedor ha desbordado el tipo de datos del campo.|  
|**adFieldDefault**|13|Indica que se utilizó el valor predeterminado para el campo al establecer los datos.|  
|**adFieldIgnore**|15|Indica que este campo se omite cuando los valores de datos de configuración en el origen. No se estableció ningún valor por el proveedor.|  
|**adFieldIntegrityViolation**|10|Indica que el campo no se puede modificar porque es una entidad calculada o derivada.|  
|**adFieldIsNull**|3|Indica que el proveedor devolvió un valor null.|  
|**adFieldOutOfSpace**|22|Indica que el proveedor no se puede obtener suficiente espacio de almacenamiento para completar una operación de traslado o la operación de copia.|
