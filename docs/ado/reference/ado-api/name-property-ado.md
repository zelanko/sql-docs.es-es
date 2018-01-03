---
title: Name (propiedad) (ADO) | Documentos de Microsoft
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
- _Parameter::Name
- Field20::Name
helpviewer_keywords: Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 86549008c17e3df7ad2761b8bb90f12082968c31
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="name-property-ado"></a>Propiedad Name (ADO)
Indica el nombre de un objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** valor que indica el nombre de un objeto.  
  
## <a name="remarks"></a>Comentarios  
 Use la **nombre** propiedad para asignar un nombre a o recuperar el nombre de un **comando**, **propiedad**, **campo**, o **parámetro**  objeto.  
  
 El valor es de lectura/escritura en un **comando** objeto y de solo lectura en un **propiedad** objeto.  
  
 Para una **campo** objeto, **nombre** suele ser de sólo lectura. Sin embargo, para el nuevo **campo** objetos que se han anexado a la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección de un [registro](../../../ado/reference/ado-api/record-object-ado.md), **nombre** es de lectura/escritura sólo después el [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad para la **campo** se ha especificado y el proveedor de datos ha agregado correctamente el nuevo **campo** mediante una llamada a la [ Actualización](../../../ado/reference/ado-api/update-method.md) método de la **campos** colección.  
  
 Para **parámetro** objetos todavía no está anexan a la [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección, el **nombre** propiedad es de lectura/escritura. Para anexar **parámetro** objetos y todos los demás objetos, la **nombre** propiedad es de solo lectura. Nombres no tienen que ser únicos dentro de una colección.  
  
 Puede recuperar el **nombre** propiedad de un objeto mediante una referencia ordinal, después del cual puede hacer referencia al objeto directamente por su nombre. Por ejemplo, si `rstMain.Properties(20).Name` produce `Updatability`, posteriormente, puede hacer referencia a esta propiedad como `rstMain.Properties("Updatability")`.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|  
|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de propiedades de nombre (VB) y atributos](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Atributos y ejemplo de las propiedades nombre (VC ++)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
