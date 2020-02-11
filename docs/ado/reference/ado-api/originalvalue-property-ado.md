---
title: OriginalValue (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::OriginalValue
helpviewer_keywords:
- OriginalValue property [ADO]
ms.assetid: 6e33c6ec-14d9-4b1d-ba9b-cb99862e7bac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 512569ce2baa8acabdf8bcbf8f637ebf20e4f613
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917843"
---
# <a name="originalvalue-property-ado"></a>Propiedad OriginalValue (ADO)
Indica el valor de un [campo](../../../ado/reference/ado-api/field-object.md) que existía en el registro antes de que se realizaran cambios.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor de **tipo Variant** que representa el valor de un campo antes de cualquier cambio.  
  
## <a name="remarks"></a>Observaciones  
 Utilice la propiedad **OriginalValue** para devolver el valor de campo original de un campo del registro actual.  
  
 En el *modo de actualización inmediata* (en el que el proveedor escribe los cambios en el origen de datos subyacente después de llamar al método [Update](../../../ado/reference/ado-api/update-method.md) ), la propiedad **OriginalValue** devuelve el valor del campo que existía antes de cualquier cambio (es decir, desde la última llamada al método **Update** ). Este es el mismo valor que utiliza el método [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) para reemplazar la propiedad [Value](../../../ado/reference/ado-api/value-property-ado.md) .  
  
 En el *modo de actualización por lotes* (en el que el proveedor almacena en caché varios cambios y los escribe en el origen de datos subyacente solo cuando se llama al método [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) ), la propiedad **OriginalValue** devuelve el valor del campo que existía antes de cualquier cambio (es decir, desde la última llamada al método **UpdateBatch** ). Este es el mismo valor que utiliza el método [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) para reemplazar la propiedad **Value** . Cuando se usa esta propiedad con la propiedad [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) , se pueden resolver los conflictos que surgen de las actualizaciones por lotes.  
  
## <a name="record"></a>Registro  
 En el caso de los objetos de [registro](../../../ado/reference/ado-api/record-object-ado.md) , la propiedad **OriginalValue** estará vacía para los campos agregados antes de llamar a [Update](../../../ado/reference/ado-api/update-method.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades OriginalValue y UnderlyingValue (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Ejemplo de las propiedades OriginalValue y UnderlyingValue (VC + +)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [Propiedad UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)
