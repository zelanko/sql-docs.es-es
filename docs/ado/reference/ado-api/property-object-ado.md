---
title: Objeto Property (ADO) | Documentos de Microsoft
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
- Property
helpviewer_keywords:
- Property object [ADO]
ms.assetid: b2a4767c-03c7-4935-a3bc-df3e1a38a009
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 774ed0d33d3066f600c6af98ea89b91a2770ed3c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="property-object-ado"></a>Objeto Property (ADO)
Representa una característica dinámica de un objeto ADO definido por el proveedor.  
  
## <a name="remarks"></a>Comentarios  
 Objetos ADO tienen dos tipos de propiedades: integradas y dinámicas.  
  
 Las propiedades integradas son aquellas propiedades implementadas en ADO y disponibles inmediatamente para cualquier objeto nuevo, utilizando el `MyObject.Property` sintaxis. No aparecen como **propiedad** objetos en un objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección, por lo que aunque se pueden cambiar sus valores, no se puede modificar sus características.  
  
 Propiedades dinámicas se definen mediante el proveedor de datos subyacente y aparecen en la **propiedades** colección para el objeto ADO apropiado. Por ejemplo, una propiedad específica del proveedor puede indicar si una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto admite transacciones o actualizaciones. Estas propiedades adicionales aparecerán como **propiedad** objetos que **Recordset** del objeto **propiedades** colección. Pueden hacer referencia a las propiedades dinámicas sólo a través de la colección, usando la `MyObject.Properties(0)` o `MyObject.Properties("Name")` sintaxis.  
  
 No se puede eliminar cualquier tipo de propiedad.  
  
 Dinámico **propiedad** objeto tiene cuatro propiedades integradas de su propio:  
  
-   El [nombre](../../../ado/reference/ado-api/name-property-ado.md) propiedad es una cadena que identifica la propiedad.  
  
-   El [tipo](../../../ado/reference/ado-api/type-property-ado.md) propiedad es un entero que especifica el tipo de datos de propiedad.  
  
-   El [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad es una variante que contiene el valor de propiedad. **Valor** es la propiedad predeterminada para un **propiedad** objeto.  
  
-   El [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propiedad es un valor long que indica características de la propiedad específica del proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Objeto de propiedades, métodos y eventos](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto de comando (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
