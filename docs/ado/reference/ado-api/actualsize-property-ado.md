---
title: Propiedad ActualSize (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::ActualSize
helpviewer_keywords:
- ActualSize property [ADO]
ms.assetid: 722803d0-cef5-4d4c-b79d-3f2f58052229
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b864f480542c7ff649bf9b830ba445517dafb91b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698894"
---
# <a name="actualsize-property-ado"></a>Propiedad ActualSize (ADO)
Indica la longitud real de un valor de campo en bytes.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Devuelve un **largo** valor.  
  
## <a name="remarks"></a>Comentarios  
 Use la **ActualSize** propiedad para devolver la longitud real de un [campo](../../../ado/reference/ado-api/field-object.md) valor del objeto. Todos los campos, el **ActualSize** propiedad es de solo lectura. Si ADO no puede determinar la longitud de la **campo** valor del objeto, el **ActualSize** propiedad devuelve **adUnknown**.  
  
 El **ActualSize** y [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) propiedades son diferentes, como se muestra en el ejemplo siguiente. Un **campo** objeto con un tipo declarado de **parámetros** y una longitud máxima de 50 caracteres devuelve un **DefinedSize** valor de propiedad de 50, pero la  **Ejemplo ActualSize** devuelve el valor de propiedad es la longitud de los datos almacenados en el campo para el registro actual. **Campos** con un **DefinedSize** mayores de 255 bytes se tratan como columnas de longitud variable.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo ActualSize y DefinedSize propiedades (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [Ejemplo ActualSize y DefinedSize propiedades (VC ++)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [Propiedad DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)
