---
title: NumericScale (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::NumericScale
- Field20::NumericScale
helpviewer_keywords:
- NumericScale property [ADO]
ms.assetid: 29a02992-64be-4fcd-be13-445cba205893
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 39650433fb8b88fb45d38347440d2d612481fb21
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719183"
---
# <a name="numericscale-property-ado"></a>NumericScale (propiedad, ADO)
Indica la escala de valores numéricos en un [parámetro](../../../ado/reference/ado-api/parameter-object.md) o [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **bytes** se resolverá el valor que indica el número de posiciones decimales que los valores numéricos.  
  
## <a name="remarks"></a>Comentarios  
 Use la **NumericScale** propiedad para determinar cuántos dígitos a la derecha del separador decimal que se usará para representar valores de un tipo numérico **parámetro** o **campo** objeto.  
  
 Para **parámetro** objetos, el **NumericScale** propiedad es de lectura/escritura.  
  
 Para un **campo**objeto, **NumericScale** suele ser de sólo lectura. Sin embargo, para el nuevo **campo** objetos que se han anexado a la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección de un [registro](../../../ado/reference/ado-api/record-object-ado.md), **NumericScale** es de lectura/escritura sólo después la [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad para el **campo** se ha especificado y el proveedor de datos ha agregado correctamente el nuevo **campo** mediante una llamada a la [ Actualización](../../../ado/reference/ado-api/update-method.md) método de la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|  
  
## <a name="see-also"></a>Vea también  
 [NumericScale y Precision propiedades (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale y Precision propiedades (VC ++)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Propiedad Precision (ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
