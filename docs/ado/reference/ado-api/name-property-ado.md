---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a919bb377eee2da1c3c1a65e85ddfb9807ed8d50
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918035"
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
  
 Puede recuperar la propiedad **Name** de un objeto mediante una referencia ordinal, después de la cual puede hacer referencia al objeto directamente por su nombre. Por ejemplo, si `rstMain.Properties(20).Name` produce `Updatability`, puede hacer referencia posteriormente a esta propiedad como `rstMain.Properties("Updatability")`.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|  
|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedades de atributos y nombres (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Ejemplo de propiedades de atributos y nombres (VC + +)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
