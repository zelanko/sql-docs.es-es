---
description: Propiedad Name (ADO)
title: Name (propiedad) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Name
- Field20::Name
helpviewer_keywords:
- Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
author: rothja
ms.author: jroth
ms.openlocfilehash: 60bf64f57c4373d814f2b207808aa2d7dbe7c497
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443137"
---
# <a name="name-property-ado"></a>Propiedad Name (ADO)
Indica el nombre de un objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de **cadena** que indica el nombre de un objeto.  
  
## <a name="remarks"></a>Observaciones  
 Utilice la propiedad **nombre** para asignar un nombre al nombre de un objeto de **comando**, **propiedad**, **campo**o **parámetro** .  
  
 El valor es de lectura y escritura en un objeto de **comando** y de solo lectura en un objeto de **propiedad** .  
  
 Para un objeto de **campo** , **el nombre** es normalmente de solo lectura. Sin embargo, para los nuevos objetos de **campo** que se han anexado a la colección [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de un [registro](../../../ado/reference/ado-api/record-object-ado.md), **Name** es Read/Write solo después de que se haya especificado la propiedad [Value](../../../ado/reference/ado-api/value-property-ado.md) para el **campo** y el proveedor de datos haya agregado correctamente el nuevo **campo** llamando al método [Update](../../../ado/reference/ado-api/update-method.md) de la colección **Fields** .  
  
 En el caso de los objetos de **parámetro** que todavía no se han anexado a la colección [Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) , la propiedad **Name** es de lectura y escritura. Para los objetos de **parámetro** anexados y todos los demás objetos, la propiedad **Name** es de solo lectura. Los nombres no tienen que ser únicos dentro de una colección.  
  
 Puede recuperar la propiedad **Name** de un objeto mediante una referencia ordinal, después de la cual puede hacer referencia al objeto directamente por su nombre. Por ejemplo, si `rstMain.Properties(20).Name` produce `Updatability` , puede hacer referencia posteriormente a esta propiedad como `rstMain.Properties("Updatability")` .  
  
## <a name="applies-to"></a>Se aplica a  

:::row:::
    :::column:::
        [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
        [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter (objeto)](../../../ado/reference/ado-api/parameter-object.md)  
        [Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedades de atributos y nombres (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Ejemplo de propiedades de atributos y nombres (VC + +)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
