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
ms.openlocfilehash: 6d405113044d10244d8c4fc3483c6220bf630dc5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921427"
---
# <a name="actualsize-property-ado"></a>Propiedad ActualSize (ADO)
Indica la longitud real del valor de un campo en bytes.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Devuelve un valor **Long** .  
  
## <a name="remarks"></a>Observaciones  
 Use la propiedad **ActualSize** para devolver la longitud real del valor de un objeto de [campo](../../../ado/reference/ado-api/field-object.md) . En todos los campos, la propiedad **ActualSize** es de solo lectura. Si ADO no puede determinar la longitud del valor del objeto de **campo** , la propiedad **ActualSize** devuelve **adUnknown**.  
  
 Las propiedades **ActualSize** y [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) son diferentes, tal como se muestra en el ejemplo siguiente. Un objeto de **campo** con un tipo declarado de **advarchar** y una longitud máxima de 50 caracteres devuelve el valor de la propiedad **DefinedSize** de 50, pero el valor de la propiedad **ActualSize** que devuelve es la longitud de los datos almacenados en el campo para el registro actual. **Los campos** con un **DefinedSize** mayor que 255 bytes se tratan como columnas de longitud variable.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedades ActualSize y DefinedSize (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [Ejemplo de propiedades ActualSize y DefinedSize (VC + +)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [Propiedad DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)
