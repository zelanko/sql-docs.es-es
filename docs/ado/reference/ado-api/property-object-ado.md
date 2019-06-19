---
title: Objeto Property (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: af077c1606148eacb4f93ba6cfb52c3bb5eeefce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702949"
---
# <a name="property-object-ado"></a>Objeto Property (ADO)
Representa una característica dinámica de un objeto ADO que está definida por el proveedor.  
  
## <a name="remarks"></a>Comentarios  
 Los objetos ADO tienen dos tipos de propiedades: integradas y dinámicas.  
  
 Las propiedades integradas son aquellas propiedades implementadas en ADO y disponibles inmediatamente para cualquier objeto nuevo, utilizando el `MyObject.Property` sintaxis. No aparecen como **propiedad** objetos en un objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección, por lo que aunque se pueden cambiar sus valores, no se puede modificar sus características.  
  
 Propiedades dinámicas se definen mediante el proveedor de datos subyacente y aparecen en la **propiedades** colección para el objeto ADO apropiado. Por ejemplo, una propiedad específica del proveedor puede indicar si un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto admite transacciones o actualizaciones. Estas propiedades adicionales aparecerán como **propiedad** objetos en el que **Recordset** del objeto **propiedades** colección. Propiedades dinámicas se pueden hacer referencia únicamente a través de la colección, utilizando el `MyObject.Properties(0)` o `MyObject.Properties("Name")` sintaxis.  
  
 No se puede eliminar cualquier tipo de propiedad.  
  
 Dinámico **propiedad** objeto tiene cuatro propiedades integradas de su propio:  
  
-   El [nombre](../../../ado/reference/ado-api/name-property-ado.md) propiedad es una cadena que identifica la propiedad.  
  
-   El [tipo](../../../ado/reference/ado-api/type-property-ado.md) propiedad es un entero que especifica el tipo de datos de propiedad.  
  
-   El [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad es una variante que contiene el valor de propiedad. **Valor** es la propiedad predeterminada para un **propiedad** objeto.  
  
-   El [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propiedad es un valor long que indica características de la propiedad específica del proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Objeto de propiedades, métodos y eventos](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
