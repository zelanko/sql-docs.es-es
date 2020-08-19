---
description: Objeto Property (ADO)
title: Property (objeto) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Property
helpviewer_keywords:
- Property object [ADO]
ms.assetid: b2a4767c-03c7-4935-a3bc-df3e1a38a009
author: rothja
ms.author: jroth
ms.openlocfilehash: 8901f4b0f5372063b8aff88a47a7fddae13e66d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442627"
---
# <a name="property-object-ado"></a>Objeto Property (ADO)
Representa una característica dinámica de un objeto ADO definido por el proveedor.  
  
## <a name="remarks"></a>Observaciones  
 Los objetos ADO tienen dos tipos de propiedades: integrado y dinámico.  
  
 Las propiedades integradas son aquellas que se implementan en ADO y que están inmediatamente disponibles para cualquier objeto nuevo, utilizando la `MyObject.Property` Sintaxis. No aparecen como objetos de **propiedad** en la colección de [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) de un objeto, por lo que, aunque se pueden cambiar sus valores, no se pueden modificar sus características.  
  
 El proveedor de datos subyacente define las propiedades dinámicas y aparecen en la colección de **propiedades** para el objeto ADO adecuado. Por ejemplo, una propiedad específica del proveedor puede indicar si un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) admite transacciones o actualizaciones. Estas propiedades adicionales aparecerán como objetos de **propiedad** en la colección de **propiedades** del objeto de **conjunto de registros** . Solo se puede hacer referencia a las propiedades dinámicas a través de la colección mediante la `MyObject.Properties(0)` `MyObject.Properties("Name")` Sintaxis o.  
  
 No se puede eliminar ningún tipo de propiedad.  
  
 Un objeto de **propiedad** dinámica tiene cuatro propiedades integradas propias:  
  
-   La propiedad [Name](../../../ado/reference/ado-api/name-property-ado.md) es una cadena que identifica la propiedad.  
  
-   La propiedad [Type](../../../ado/reference/ado-api/type-property-ado.md) es un entero que especifica el tipo de datos de la propiedad.  
  
-   La propiedad [Value](../../../ado/reference/ado-api/value-property-ado.md) es una variante que contiene el valor de la propiedad. **Value** es la propiedad predeterminada de un objeto **Property** .  
  
-   La propiedad [attributes](../../../ado/reference/ado-api/attributes-property-ado.md) es un valor largo que indica las características de la propiedad específica del proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Property](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Command (objeto) (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Connection (objeto) (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Field (objeto)](../../../ado/reference/ado-api/field-object.md)   
 [Colección Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
