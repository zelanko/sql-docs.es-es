---
title: Información de Error relacionado con el campo | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: e18698d7fba50ce6a63938df574408367b8b20cf
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702011"
---
# <a name="field-related-error-information"></a>Información de Error relacionado con el campo
Si un error está directamente relacionado con un campo, por ejemplo, si los datos no se encuentra o si es del tipo incorrecto para el campo - se puede recuperar más información sobre la causa del problema examinando la **campo** del objeto **estado**  propiedad. Esta propiedad se ha mejorado para proporcionar información específica acerca del problema. Así, por ejemplo, cuando una llamada a **UpdateBatch** se produce un error, la causa del problema se puede determinar examinando el **estado** propiedad de la **campos** en cada uno de los afectados registros. La propiedad contendrá uno de los valores en el **FieldStatusEnum** constante. En la tabla siguiente incluye los valores que son de especial interés cuando se produce un error.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|Indica que el campo no puede recuperarse o almacenado sin pérdida de datos.|  
|**adFieldDataOverflow**|6|Indica que los datos devueltos por el proveedor ha desbordado el tipo de datos del campo.|  
|**adFieldDefault**|13|Indica que el valor predeterminado para el campo se utiliza al establecer los datos.|  
|**adFieldIgnore**|15|Indica que se ha omitido este campo cuando los valores de los datos de configuración en el origen. El proveedor se estableció ningún valor.|  
|**adFieldIntegrityViolation**|10|Indica que el campo no se puede modificar porque es una entidad calculada o derivada.|  
|**adFieldIsNull**|3|Indica que el proveedor devolvió un valor null.|  
|**adFieldOutOfSpace**|22|Indica que el proveedor no se puede obtener el espacio de almacenamiento suficiente para completar un movimiento o la operación de copia.|
