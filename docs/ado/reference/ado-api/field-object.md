---
title: Objeto Field | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field
helpviewer_keywords:
- Field object [ADO]
ms.assetid: b10a72fc-3c4b-4186-a70b-993dc9f7a092
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 002e0f570aa2143ddba4a5b55f3cba1537389e77
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753323"
---
# <a name="field-object"></a>Objeto Field
Representa una columna de datos con un tipo de datos común.  
  
## <a name="remarks"></a>Comentarios  
 Cada **campo** objeto corresponde a una columna de la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Usa el [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad de **campo** objetos para establecer o devolver datos para el registro actual. Dependiendo de la funcionalidad expone el proveedor, algunas colecciones, métodos o propiedades de un **campo** objeto no esté disponible.  
  
 Con las colecciones, métodos y propiedades de un **campo** objeto, puede hacer lo siguiente:  
  
-   Devolver el nombre de un campo con el [nombre](../../../ado/reference/ado-api/name-property-ado.md) propiedad.  
  
-   Ver o cambiar los datos en el campo con el **valor** propiedad. **Valor** es la propiedad predeterminada de la **campo** objeto.  
  
-   Devolver las características básicas de un campo con el [tipo](../../../ado/reference/ado-api/type-property-ado.md), [precisión](../../../ado/reference/ado-api/precision-property-ado.md), y [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) propiedades.  
  
-   Devolver el tamaño declarado de un campo con el [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) propiedad.  
  
-   Devolver el tamaño real de los datos en un campo determinado con el [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) propiedad.  
  
-   Determinar qué tipos de funcionalidad son compatibles con un campo dado con la [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propiedad y [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
-   Manipular los valores de los campos que contienen datos de caracteres largos o binarios largos con la [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) y [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) métodos.  
  
-   Si el proveedor admite las actualizaciones por lotes, solucionar discrepancias en los valores de campo durante la actualización por lotes con el [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) y [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) propiedades.  
  
 Todas las propiedades de metadatos (**nombre**, **tipo**, **DefinedSize**, **precisión**, y **NumericScale**) están disponibles antes de abrir el **campo** del objeto **Recordset**. Establecerlas en ese momento es útil para la creación dinámica de formularios.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Los eventos, métodos y propiedades del objeto de campo](../../../ado/reference/ado-api/field-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Colección de campos (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
