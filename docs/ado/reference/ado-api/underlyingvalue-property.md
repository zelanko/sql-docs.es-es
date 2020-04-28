---
title: Propiedad UnderlyingValue | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::GetUnderlyingValue
- Field20::get_UnderlyingValue
- Field20::UnderlyingValue
helpviewer_keywords:
- UnderlyingValue property
ms.assetid: 00a0c8b8-8b63-433f-95b8-020ab05874a0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 582d0b87edd4729ce54cc2a7323b0a63443cab82
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938855"
---
# <a name="underlyingvalue-property"></a>Propiedad UnderlyingValue
Indica el valor actual de un objeto de [campo](../../../ado/reference/ado-api/field-object.md) en la base de datos.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor de **tipo Variant** que indica el valor del **campo**.  
  
## <a name="remarks"></a>Observaciones  
 Utilice la propiedad **UnderlyingValue** para devolver el valor de campo actual de la base de datos. El valor de campo de la propiedad **UnderlyingValue** es el valor que es visible para la transacción y puede ser el resultado de una actualización reciente de otra transacción. Esto puede diferir de la propiedad [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) , que refleja el valor que se devolvió originalmente al [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Esto es similar al uso del método [Resync](../../../ado/reference/ado-api/resync-method.md) , pero la propiedad **UnderlyingValue** solo devuelve el valor de un campo específico del registro actual. Este es el mismo valor que utiliza el método [Resync](../../../ado/reference/ado-api/resync-method.md) para reemplazar la propiedad [Value](../../../ado/reference/ado-api/value-property-ado.md) .  
  
 Cuando se usa esta propiedad con la propiedad **OriginalValue** , se pueden resolver los conflictos que surgen de las actualizaciones por lotes.  
  
## <a name="record"></a>Registro  
 En el caso de los objetos de [registro](../../../ado/reference/ado-api/record-object-ado.md) , esta propiedad estará vacía para los campos agregados antes de llamar a [Update](../../../ado/reference/ado-api/update-method.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades OriginalValue y UnderlyingValue (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Ejemplo de las propiedades OriginalValue y UnderlyingValue (VC + +)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [OriginalValue (propiedad, ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Método Resync](../../../ado/reference/ado-api/resync-method.md)
