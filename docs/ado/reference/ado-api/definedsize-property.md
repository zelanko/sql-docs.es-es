---
title: Propiedad DefinedSize | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::DefinedSize
helpviewer_keywords:
- DefinedSize property [ADO]
ms.assetid: 3ee27314-a305-4fbc-8433-9ee9a909afd6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b78fe75314e6e2aacf5c6f0d9c599f5cb6db6292
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="definedsize-property"></a>Propiedad DefinedSize
Indica la capacidad de datos de un [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **largo** valor que refleja el tamaño definido de un campo, que depende del tipo de datos del objeto field; vea [tipo](../../../ado/reference/ado-api/type-property-ado.md) para obtener más información. Para un campo que utiliza un tipo de datos de longitud fija, el valor devuelto es el tamaño del tipo de datos en bytes. Para un campo que utiliza un tipo de datos de longitud variable, esta es una de las siguientes acciones:  
  
1.  La longitud máxima del campo en caracteres (para **parámetros** y **adVarWChar**) o en bytes (para **adVarBinary**, y **adVarNumeric**) si el campo tiene una longitud definida. Por ejemplo, **adVarChar(5)** campo tiene una longitud máxima de 5.  
  
2.  La longitud máxima del tipo de datos de caracteres (para **cada** y **adWChar**) o en bytes (para **adBinary** y **adNumeric**) si el campo no tiene una longitud definida.  
  
3.  ~ 0 (bit a bit, el valor no es 0; todos los bits se establecen en 1) si el campo ni el tipo de datos tiene una longitud máxima definida.  
  
4.  Para los tipos de datos que no tienen una longitud, se establece en ~ 0 (bit a bit, el valor no es 0; todos los bits se establecen en 1).  
  
## <a name="remarks"></a>Comentarios  
 Use la **DefinedSize** propiedad para determinar la capacidad de datos de un **campo** objeto.  
  
 El **DefinedSize** y [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) propiedades son diferentes. Por ejemplo, considere un **campo** objeto con un tipo declarado de **parámetros** y un **DefinedSize** valor de la propiedad de 50, que contiene un único carácter. El **ActualSize** devuelve el valor de propiedad es la longitud en bytes del carácter único.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo ActualSize y DefinedSize propiedades (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [Ejemplo ActualSize y DefinedSize propiedades (VC ++)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [Propiedad ActualSize (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
