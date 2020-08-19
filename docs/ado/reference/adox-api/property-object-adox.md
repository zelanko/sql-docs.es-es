---
description: Objeto Property (ADOX)
title: Objeto Property (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Property object [ADOX]
ms.assetid: 6a56def6-dbe6-4ccc-a491-8d076889f019
author: rothja
ms.author: jroth
ms.openlocfilehash: 5a836b5b0778aea77732036d1951db81aa790198
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439607"
---
# <a name="property-object-adox"></a>Objeto Property (ADOX)
Representa una característica de un objeto ADOX.  
  
## <a name="remarks"></a>Observaciones  
 Los objetos ADOX tienen dos tipos de propiedades: integrado y dinámico.  
  
 Las propiedades integradas son aquellas que están inmediatamente disponibles para cualquier objeto nuevo, mediante la sintaxis de la propiedad objeto. No aparecen como objetos de propiedad en la [colección de propiedades](../../../ado/reference/ado-api/properties-collection-ado.md)de un objeto, por lo que, aunque se pueden cambiar sus valores, no se pueden modificar sus características.  
  
 El proveedor de datos subyacente define las propiedades dinámicas y aparecen en la colección de propiedades para el objeto ADOX adecuado.  Solo se puede hacer referencia a las propiedades dinámicas a través de la colección mediante la sintaxis de objetos. Properties (0) o DataObject. Properties ("Name").  
  
 No se puede eliminar ningún tipo de propiedad.  
  
 Un objeto de propiedad dinámica tiene cuatro propiedades integradas propias:  
  
 La propiedad [Name](../../../ado/reference/ado-api/name-property-ado.md) es una cadena que identifica la propiedad.  
  
 La propiedad [Type](../../../ado/reference/ado-api/type-property-ado.md) es un entero que especifica el tipo de datos de la propiedad.  
  
 La propiedad [Value](../../../ado/reference/ado-api/value-property-ado.md) es una variante que contiene el valor de la propiedad. Value es la propiedad predeterminada de un objeto Property.  
  
 La propiedad [attributes](../../../ado/reference/ado-api/attributes-property-ado.md) es un valor largo que indica las características de la propiedad específica del proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Property (ADOX)](../../../ado/reference/adox-api/adox-property-object-properties-methods-and-events.md)
