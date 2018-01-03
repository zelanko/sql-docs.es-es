---
title: FieldStatusEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: FieldStatusEnum
helpviewer_keywords: FieldStatusEnum enumeration [ADO]
ms.assetid: e06da1e2-303f-41b2-a3b0-61e233da152c
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 12e543a4baa7bbcc46ea39e906d57d001ea5f078
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="fieldstatusenum"></a>FieldStatusEnum
Especifica la [estado](../../../ado/reference/ado-api/status-property-ado-field.md) de un [objeto Field](../../../ado/reference/ado-api/field-object.md).  
  
 El **adFieldPending\***  valores indican la operación que provocó el estado esté establecido y se puede combinar con otros valores de estado.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adFieldAlreadyExists**|26|Indica que el campo especificado ya existe.|  
|**adFieldBadStatus**|12|Indica que se envió un valor de estado no válido desde ADO al proveedor OLE DB. Las causas posibles incluyen una OLE DB 1.0 o 1.1 proveedor o una combinación incorrecta de [valor](../../../ado/reference/ado-api/value-property-ado.md) y [estado](../../../ado/reference/ado-api/status-property-ado-field.md).|  
|**adFieldCannotComplete**|20|Indica que el servidor de la dirección URL especificada por [origen](../../../ado/reference/ado-api/source-property-ado-record.md) no se pudo completar la operación.|  
|**adFieldCannotDeleteSource**|23|Indica que, durante una operación de movimiento, un árbol o subárbol se movió a una nueva ubicación, pero no se pudo eliminar el origen.|  
|**adFieldCantConvertValue**|2|Indica que el campo no se puede recuperar ni almacenar sin pérdida de datos.|  
|**adFieldCantCreate**|7|Indica que no se pudo agregar el campo porque el proveedor superó una limitación (por ejemplo, el número de campos permitido).|  
|**adFieldDataOverflow**|6|Indica que los datos devueltos por el proveedor ha desbordado el tipo de datos del campo.|  
|**adFieldDefault**|13|Indica que se utilizó el valor predeterminado para el campo al establecer los datos.|  
|**adFieldDoesNotExist**|16|Indica que el campo especificado no existe.|  
|**adFieldIgnore**|15|Indica que este campo se omite cuando los valores de datos de configuración en el origen. El proveedor no establece ningún valor.|  
|**adFieldIntegrityViolation**|10|Indica que el campo no se puede modificar porque es una entidad calculada o derivada.|  
|**adFieldInvalidURL**|17|Indica que la dirección URL de origen de datos contiene caracteres no válidos.|  
|**adFieldIsNull**|3|Indica que el proveedor devolvió un valor de tipo VARIANT de tipo VT_NULL y que el campo no está vacío.|  
|**adFieldOK**|0|Predeterminado: Indica que el campo se ha agregado o eliminado correctamente.|  
|**adFieldOutOfSpace**|22|Indica que el proveedor no se puede obtener suficiente espacio de almacenamiento para completar una operación de traslado o la operación de copia.|  
|**adFieldPendingChange**|0x40000|Indica que el campo se ha eliminado y, a continuación, volver a agregar, quizás con un tipo de datos diferente, o que el valor del campo que anteriormente tenía un estado de **adFieldOK** ha cambiado. La forma final del campo modificará la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección después de la [actualización](../../../ado/reference/ado-api/update-method.md) se llama al método.|  
|**adFieldPendingDelete**|0x20000|Indica que la **eliminar** operación que ha causado el establecimiento del estado. El campo se ha marcado para su eliminación de la **campos** colección después de la **actualización** se llama al método.|  
|**adFieldPendingInsert**|0x10000|Indica que la **anexado** operación que ha causado el establecimiento del estado. El **campo** se ha marcado para poder agregarla a la **campos** colección después de la **actualización** se llama al método.|  
|**adFieldPendingUnknown**|0x80000|Indica que el proveedor no puede determinar el estado del campo de qué operación causado establecerse.|  
|**adFieldPendingUnknownDelete**|0x100000|Indica que el proveedor no puede determinar qué operación causó el estado del campo establecerse y que el campo se eliminarán de la **campos** colección después de la **actualización** se llama al método.|  
|**adFieldPermissionDenied**|9|Indica que el campo no se puede modificar porque está definido como de solo lectura.|  
|**adFieldReadOnly**|24|Indica que el campo del origen de datos se define como de solo lectura.|  
|**adFieldResourceExists**|19|Indica que el proveedor no pudo realizar la operación porque ya existe un objeto en la dirección URL de destino y no puede sobrescribir el objeto.|  
|**adFieldResourceLocked**|18|Indica que el proveedor no pudo realizar la operación porque el origen de datos está bloqueado por uno o varios otros procesos o aplicaciones.|  
|**adFieldResourceOutOfScope**|25|Indica que una dirección URL de origen o destino está fuera del ámbito del registro actual.|  
|**adFieldSchemaViolation**|11|Indica que el valor infringió la restricción de esquema de origen de datos para el campo.|  
|**adFieldSignMismatch**|5|Indica que el valor de datos devuelto por el proveedor tenía signo pero el tipo de datos del valor del campo de ADO no tenía signo.|  
|**adFieldTruncated**|4|Indica que se truncaron los datos de longitud variable al leer desde el origen de datos.|  
|**adFieldUnavailable**|8|Indica que el proveedor no pudo determinar el valor al leer desde el origen de datos. Por ejemplo, la fila recién creada, el valor predeterminado de la columna no estaba disponible, y todavía no había ha especificado un nuevo valor.|  
|**adFieldVolumeNotFound**|21|Indica que el proveedor no se puede encontrar el volumen de almacenamiento indicado por la dirección URL.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad Status (Field ADO)](../../../ado/reference/ado-api/status-property-ado-field.md)
