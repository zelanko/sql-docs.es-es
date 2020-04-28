---
title: Type (propiedad) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Type
- Field20::Type
helpviewer_keywords:
- Type property [ADO]
ms.assetid: 8a4c079f-9f4f-4545-801d-85983b8db71e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ee1058299becb4a7a4234debc097516cb02dd41
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67937868"
---
# <a name="type-property-ado"></a>Tipo (propiedad, ADO)
Indica el tipo operativo o el tipo de datos de un [parámetro](../../../ado/reference/ado-api/parameter-object.md), [campo](../../../ado/reference/ado-api/field-object.md)o objeto de [propiedad](../../../ado/reference/ado-api/property-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) .  
  
## <a name="remarks"></a>Observaciones  
 En el caso de los objetos de **parámetro** , la propiedad **Type** es de lectura y escritura. En el caso de los nuevos objetos de **campo** que se han anexado a la colección [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de un [registro](../../../ado/reference/ado-api/record-object-ado.md), el **tipo** es Read/Write solo después de que se haya especificado la propiedad [Value](../../../ado/reference/ado-api/value-property-ado.md) para el **campo** y el proveedor de datos haya agregado correctamente el nuevo **campo** llamando al método [Update](../../../ado/reference/ado-api/update-method.md) de la colección **Fields** .  
  
 Para todos los demás objetos, la propiedad **Type** es de solo lectura.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de la propiedad de tipo (campo) (VB)](../../../ado/reference/ado-api/type-property-example-field-vb.md)   
 [Ejemplo de propiedad de tipo (propiedad) (VC + +)](../../../ado/reference/ado-api/type-property-example-property-vc.md)   
 [RecordType (propiedad, ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Propiedad Type (objeto Stream de ADO)](../../../ado/reference/ado-api/type-property-ado-stream.md)
