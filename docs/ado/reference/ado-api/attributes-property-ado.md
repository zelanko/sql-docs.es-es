---
title: Attributes (propiedad) (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::Attributes
- Field20::Attributes
- _Parameter::Attributes
helpviewer_keywords:
- Attributes property [ADO]
ms.assetid: acc15d40-68a6-4ba9-85bd-12d331aecaa6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bffe5215cbb93e24f6914d6d56a349c9d35f6b7
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="attributes-property-ado"></a>Propiedad Attributes (ADO)
Indica una o varias características de un objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **largo** valor.  
  
 Para una [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto, el **atributos** propiedad es de lectura/escritura y su valor puede ser la suma de uno o varios [XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md) valores. El valor predeterminado es cero (0).  
  
 Para una [parámetro](../../../ado/reference/ado-api/parameter-object.md) objeto, el **atributos** propiedad es de lectura/escritura y su valor puede ser la suma de uno o más [ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md) valores. El valor predeterminado es **adParamSigned**.  
  
 Para una [campo](../../../ado/reference/ado-api/field-object.md) objeto, el **atributos** propiedad puede ser la suma de uno o varios [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) valores. Es normalmente de solo lectura. Sin embargo, para el nuevo **campo** objetos que se han anexado a la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección de un [registro](../../../ado/reference/ado-api/record-object-ado.md), **atributos** es de solo lectura/escritura Después de la [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad para la **campo** se ha especificado y la nueva **campo** se ha agregado correctamente el proveedor de datos mediante una llamada a la [ Actualización](../../../ado/reference/ado-api/update-method.md) método de la **campos** colección.  
  
 Para una [propiedad](../../../ado/reference/ado-api/property-object-ado.md) objeto, el **atributos** propiedad es de sólo lectura y su valor puede ser la suma de uno o más [PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md) valores.  
  
## <a name="remarks"></a>Comentarios  
 Use la **atributos** propiedad para establecer o devolver las características de **conexión** objetos, **parámetro** objetos, **campo** objetos, o **Propiedad** objetos.  
  
 Cuando establece varios atributos, puede sumar las constantes apropiadas. Si establece el valor de propiedad en una suma que incluye constantes incompatibles, se produce un error.  
  
> [!NOTE]
>  **Uso de servicios de datos remoto** esta propiedad no está disponible en un cliente **conexión** objeto.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|  
|[Objeto de parámetro](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de propiedades de nombre (VB) y atributos](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Atributos y ejemplo de las propiedades nombre (VC ++)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [Método AppendChunk (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [BeginTrans, CommitTrans y RollbackTrans métodos (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [Método GetChunk (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)

