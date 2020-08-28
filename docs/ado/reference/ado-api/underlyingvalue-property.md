---
description: Propiedad UnderlyingValue
title: Propiedad UnderlyingValue | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a96924a682a0c916da8c6834ea7b290b88b6f690
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988176"
---
# <a name="underlyingvalue-property"></a>Propiedad UnderlyingValue
Indica el valor actual de un objeto de [campo](./field-object.md) en la base de datos.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor de **tipo Variant** que indica el valor del **campo**.  
  
## <a name="remarks"></a>Observaciones  
 Utilice la propiedad **UnderlyingValue** para devolver el valor de campo actual de la base de datos. El valor de campo de la propiedad **UnderlyingValue** es el valor que es visible para la transacción y puede ser el resultado de una actualización reciente de otra transacción. Esto puede diferir de la propiedad [OriginalValue](./originalvalue-property-ado.md) , que refleja el valor que se devolvió originalmente al [conjunto de registros](./recordset-object-ado.md).  
  
 Esto es similar al uso del método [Resync](./resync-method.md) , pero la propiedad **UnderlyingValue** solo devuelve el valor de un campo específico del registro actual. Este es el mismo valor que utiliza el método [Resync](./resync-method.md) para reemplazar la propiedad [Value](./value-property-ado.md) .  
  
 Cuando se usa esta propiedad con la propiedad **OriginalValue** , se pueden resolver los conflictos que surgen de las actualizaciones por lotes.  
  
## <a name="record"></a>Registro  
 En el caso de los objetos de [registro](./record-object-ado.md) , esta propiedad estará vacía para los campos agregados antes de llamar a [Update](./update-method.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Field](./field-object.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades OriginalValue y UnderlyingValue (VB)](./originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Ejemplo de las propiedades OriginalValue y UnderlyingValue (VC + +)](./originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [OriginalValue (propiedad, ADO)](./originalvalue-property-ado.md)   
 [Método Resync](./resync-method.md)