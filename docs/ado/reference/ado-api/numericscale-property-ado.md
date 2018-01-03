---
title: Propiedad NumericScale (ADO) | Documentos de Microsoft
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
f1_keywords:
- _Parameter::NumericScale
- Field20::NumericScale
helpviewer_keywords: NumericScale property [ADO]
ms.assetid: 29a02992-64be-4fcd-be13-445cba205893
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a4c162e5880176f56d30d3e973d8fa16d8cb351a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="numericscale-property-ado"></a>NumericScale (propiedad, ADO)
Indica la escala de valores numéricos en un [parámetro](../../../ado/reference/ado-api/parameter-object.md) o [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **bytes** se resolverá el valor que indica el número de posiciones decimales con qué valores numéricos.  
  
## <a name="remarks"></a>Comentarios  
 Use la **NumericScale** propiedad para determinar cuántos dígitos a la derecha del separador decimal se usará para representar valores de un tipo numérico **parámetro** o **campo** objeto.  
  
 Para **parámetro** objetos, el **NumericScale** propiedad es de lectura/escritura.  
  
 Para una **campo**objeto, **NumericScale** suele ser de sólo lectura. Sin embargo, para el nuevo **campo** objetos que se han anexado a la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección de un [registro](../../../ado/reference/ado-api/record-object-ado.md), **NumericScale** es de lectura/escritura sólo después la [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad para la **campo** se ha especificado y el proveedor de datos ha agregado correctamente el nuevo **campo** mediante una llamada a la [ Actualización](../../../ado/reference/ado-api/update-method.md) método de la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|  
  
## <a name="see-also"></a>Vea también  
 [NumericScale y ejemplo de las propiedades Precision (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale y ejemplo de las propiedades Precision (VC ++)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Propiedad Precision (ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
