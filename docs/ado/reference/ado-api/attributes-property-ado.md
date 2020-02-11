---
title: Propiedad Attributes (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Attributes
- Field20::Attributes
- _Parameter::Attributes
helpviewer_keywords:
- Attributes property [ADO]
ms.assetid: acc15d40-68a6-4ba9-85bd-12d331aecaa6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b40b71dee32608756721d84a2e13f5f54f7bcbfa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920540"
---
# <a name="attributes-property-ado"></a>Propiedad Attributes (ADO)
Indica una o más características de un objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor **Long** .  
  
 Para un objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) , la propiedad **attributes** es de lectura y escritura, y su valor puede ser la suma de uno o más valores [XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md) . El valor predeterminado es cero (0).  
  
 Para un objeto de [parámetro](../../../ado/reference/ado-api/parameter-object.md) , la propiedad **attributes** es de lectura y escritura, y su valor puede ser la suma de uno o más valores [ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md) . El valor predeterminado es **adParamSigned**.  
  
 Para un objeto de [campo](../../../ado/reference/ado-api/field-object.md) , la propiedad **attributes** puede ser la suma de uno o más valores de [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) . Normalmente es de solo lectura. Sin embargo, para los nuevos objetos de **campo** que se han anexado a la colección [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de un [registro](../../../ado/reference/ado-api/record-object-ado.md), **los atributos** son de lectura y escritura solo después de que se haya especificado la propiedad [Value](../../../ado/reference/ado-api/value-property-ado.md) para el **campo** y el proveedor de datos haya agregado correctamente el nuevo **campo** llamando al método [Update](../../../ado/reference/ado-api/update-method.md) de la colección **Fields** .  
  
 Para un objeto de [propiedad](../../../ado/reference/ado-api/property-object-ado.md) , la propiedad **attributes** es de solo lectura y su valor puede ser la suma de uno o más valores [PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md) .  
  
## <a name="remarks"></a>Observaciones  
 Utilice la propiedad **attributes** para establecer o devolver características de objetos de **conexión** , objetos de **parámetro** , objetos de **campo** o objetos de **propiedad** .  
  
 Al establecer varios atributos, puede sumar las constantes adecuadas. Si establece el valor de la propiedad en una suma que incluye constantes incompatibles, se produce un error.  
  
> [!NOTE]
>  **Uso del servicio de datos remotos** Esta propiedad no está disponible en un objeto de **conexión** del lado cliente.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|  
|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedades de atributos y nombres (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Ejemplo de propiedades de atributos y nombres (VC + +)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [AppendChunk (método) (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Métodos BeginTrans, CommitTrans y RollbackTrans (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [Método GetChunk (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
