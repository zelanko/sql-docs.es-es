---
title: Value (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
author: rothja
ms.author: jroth
ms.openlocfilehash: c84ab6806924649bdad9bb712f730c24011cdb38
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243166"
---
# <a name="value-property-ado"></a>Value (propiedad) (ADO)

Indica el valor asignado a un [campo](../../../ado/reference/ado-api/field-object.md), un [parámetro](../../../ado/reference/ado-api/parameter-object.md)o un objeto de [propiedad](../../../ado/reference/ado-api/property-object-ado.md) .
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos

Establece o devuelve un valor **Variant** que indica el valor del objeto. El valor predeterminado depende de la propiedad [Type](../../../ado/reference/ado-api/type-property-ado.md) .
  
## <a name="remarks"></a>Observaciones

Utilice la propiedad **Value** para establecer o devolver datos de objetos de **campo** , para establecer o devolver valores de parámetro con objetos de **parámetro** , o para establecer o devolver la configuración de propiedades con objetos de **propiedad** . El hecho de que la propiedad **Value** sea de lectura/escritura o de solo lectura depende de varios factores. Vea los temas de objetos correspondientes para obtener más información.

ADO permite establecer y devolver datos binarios largos con la propiedad **Value** .
  
> [!NOTE]
> En el caso de los objetos de **parámetro** , ADO lee la propiedad **Value** solo una vez desde el proveedor. Si un comando contiene un **parámetro** cuya **propiedad Value** está vacía y crea un conjunto de [registros](../../../ado/reference/ado-api/recordset-object-ado.md) a partir del comando, asegúrese de cerrar primero el **conjunto de registros** antes de recuperar la propiedad **Value** . De lo contrario, para algunos proveedores, la propiedad **Value** puede estar vacía y no contendrá el valor correcto.
> 
> En el caso de los nuevos objetos de **campo** que se han anexado a la colección [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de un objeto [Record](../../../ado/reference/ado-api/record-object-ado.md) , la propiedad **Value** debe establecerse antes de que se puedan especificar otras propiedades de **campo** . En primer lugar, se debe haber asignado un valor específico para la propiedad **Value** y [actualizarse](../../../ado/reference/ado-api/update-method.md) en la colección **Fields** denominada. A continuación, se puede tener acceso a otras propiedades, como el [tipo](../../../ado/reference/ado-api/type-property-ado.md) o [los atributos](../../../ado/reference/ado-api/attributes-property-ado.md) .
  
## <a name="applies-to"></a>Se aplica a

:::row:::
    :::column:::
        [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
    :::column-end:::
    :::column:::
        [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
    :::column-end:::
    :::column:::
        [Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte también

[Ejemplo de la propiedad Value (VB)](../../../ado/reference/ado-api/value-property-example-vb.md) 
 [Ejemplo de la propiedad Value (VC + +)](../../../ado/reference/ado-api/value-property-example-vc.md) 
