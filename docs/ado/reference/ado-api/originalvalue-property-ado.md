---
title: Propiedad OriginalValue (ADO) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917843"
---
# <a name="originalvalue-property-ado"></a>Propiedad OriginalValue (ADO)
Indica el valor de un [campo](../../../ado/reference/ado-api/field-object.md) que existía en el registro antes de que se realizaron cambios.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **Variant** valor que representa el valor de un campo antes de realizar cualquier cambio.  
  
## <a name="remarks"></a>Comentarios  
 Use la **OriginalValue** propiedad para devolver el valor original del campo para un campo desde el registro actual.  
  
 En *modo de actualización inmediata* (en el que el proveedor escribe los cambios en el origen de datos subyacente después de llamar a la [actualizar](../../../ado/reference/ado-api/update-method.md) método), el **OriginalValue** devuelve de la propiedad el valor del campo que existían antes de cualquier cambio (es decir, desde la última **actualización** llamada al método). Este es el mismo valor que el [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método se usa para reemplazar el [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad.  
  
 En *modo de actualización por lotes* (en el que el proveedor almacena en caché varios cambios y los escribe en el origen de datos subyacente únicamente cuando se llama el [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método), el **OriginalValue** propiedad devuelve el valor del campo que existían antes de cualquier cambio (es decir, desde la última **UpdateBatch** llamada al método). Este es el mismo valor que el [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) método se usa para reemplazar el **valor** propiedad. Cuando se usa esta propiedad con el [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) propiedad, puede resolver los conflictos que surgen de las actualizaciones por lotes.  
  
## <a name="record"></a>Grabar  
 Para [registro](../../../ado/reference/ado-api/record-object-ado.md) objetos, el **OriginalValue** propiedad estará vacía para los campos agregados antes de [actualización](../../../ado/reference/ado-api/update-method.md) se llama.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo OriginalValue y UnderlyingValue propiedades (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Ejemplo OriginalValue y UnderlyingValue propiedades (VC ++)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [Propiedad UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)
