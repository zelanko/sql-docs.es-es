---
title: Propiedad UnderlyingValue | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field20::GetUnderlyingValue
- Field20::get_UnderlyingValue
- Field20::UnderlyingValue
helpviewer_keywords: UnderlyingValue property
ms.assetid: 00a0c8b8-8b63-433f-95b8-020ab05874a0
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d4f3014350f4e29461a6208802d3f82f8c95535
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="underlyingvalue-property"></a>Propiedad UnderlyingValue
Indica el valor actual de un [campo](../../../ado/reference/ado-api/field-object.md) objeto en la base de datos.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **Variant** valor que indica el valor de la **campo**.  
  
## <a name="remarks"></a>Comentarios  
 Use la **UnderlyingValue** propiedad para devolver el valor del campo actual de la base de datos. El valor del campo en el **UnderlyingValue** propiedad es el valor que es visible en la transacción y puede ser el resultado de una actualización reciente por otra transacción. Ésta puede ser diferente de la [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) propiedad, que refleja el valor devuelto originalmente para la [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Esto es similar al uso de la [Resync](../../../ado/reference/ado-api/resync-method.md) método, pero la **UnderlyingValue** propiedad devuelve solo el valor de un campo específico del registro actual. Este es el mismo valor que el [Resync](../../../ado/reference/ado-api/resync-method.md) método se usa para reemplazar la [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad.  
  
 Cuando esta propiedad se usa con la **OriginalValue** propiedad, es posible solucionar conflictos que surgen de las actualizaciones por lotes.  
  
## <a name="record"></a>Grabar  
 Para [registro](../../../ado/reference/ado-api/record-object-ado.md) objetos, esta propiedad estará vacía para los campos agregados antes de [actualización](../../../ado/reference/ado-api/update-method.md) se llama.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo OriginalValue y UnderlyingValue propiedades (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Ejemplo OriginalValue y UnderlyingValue propiedades (VC ++)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [Propiedad OriginalValue (ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Método Resync](../../../ado/reference/ado-api/resync-method.md)
