---
title: Propiedad Precision (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Precision
- Field20::Precision
helpviewer_keywords:
- Precision property [ADO]
ms.assetid: 1fa38e78-6b5b-414d-ba0a-3dd26b29b766
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9819567ebe48a7654ee7a90f516ba14c8062bdcf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027856"
---
# <a name="precision-property-ado"></a>Propiedad Precision (ADO)
Indica el grado de precisión para los valores numéricos en un [parámetro](../../../ado/reference/ado-api/parameter-object.md) objeto o numérico [campo](../../../ado/reference/ado-api/field-object.md) objetos.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **bytes** valor que indica el número máximo de dígitos utilizados para representar los valores.  
  
## <a name="remarks"></a>Comentarios  
 Use la **precisión** propiedad para determinar el número máximo de dígitos utilizados para representar valores de un tipo numérico **parámetro** o **campo** objeto.  
  
 El valor es de lectura/escritura en un **parámetro** objeto.  
  
 Para un **campo**objeto, **precisión** suele ser de sólo lectura. Sin embargo, para el nuevo **campo** objetos que se han anexado a la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección de un [registro](../../../ado/reference/ado-api/record-object-ado.md), **precisión** es de solo lectura/escritura Después de la [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad para el **campo** se ha especificado y el proveedor de datos ha agregado correctamente el nuevo **campo** mediante una llamada a la [Actualización](../../../ado/reference/ado-api/update-method.md) método de la **campos** colección.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>Vea también  
 [NumericScale y Precision propiedades (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale y Precision propiedades (VC ++)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [NumericScale (propiedad, ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)
