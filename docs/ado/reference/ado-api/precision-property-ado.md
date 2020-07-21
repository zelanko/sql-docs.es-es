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
author: rothja
ms.author: jroth
ms.openlocfilehash: f3a72234a6d5e5cbb8e0dc9f5d625b93f15f437f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763336"
---
# <a name="precision-property-ado"></a>Propiedad Precision (ADO)
Indica el grado de precisión de los valores numéricos de un objeto de [parámetro](../../../ado/reference/ado-api/parameter-object.md) o de los objetos de [campo](../../../ado/reference/ado-api/field-object.md) numérico.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de **byte** que indica el número máximo de dígitos utilizados para representar valores.  
  
## <a name="remarks"></a>Observaciones  
 Utilice la propiedad **precisión** para determinar el número máximo de dígitos que se usan para representar valores para un **parámetro** numérico o un objeto de **campo** .  
  
 El valor es de lectura y escritura en un objeto de **parámetro** .  
  
 Para un objeto de **campo**, la **precisión** suele ser de solo lectura. Sin embargo, para los nuevos objetos de **campo** que se han anexado a la colección [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de un [registro](../../../ado/reference/ado-api/record-object-ado.md), la **precisión** es Read/Write solo después de que se haya especificado la propiedad [Value](../../../ado/reference/ado-api/value-property-ado.md) para el **campo** y el proveedor de datos haya agregado correctamente el nuevo **campo** llamando al método [Update](../../../ado/reference/ado-api/update-method.md) de la colección **Fields** .  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades NumericScale y Precision (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [Ejemplo de las propiedades NumericScale y Precision (VC + +)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [NumericScale (propiedad, ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)
