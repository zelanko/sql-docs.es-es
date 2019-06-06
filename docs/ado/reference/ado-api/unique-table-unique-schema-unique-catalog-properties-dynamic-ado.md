---
title: El control cambia a la tabla Base del conjunto de registros (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Unique Table property [ADO]
- Unique Schema property [ADO]
- Unique Catalog property [ADO]
ms.assetid: d0e775d8-e353-46a1-ad10-ed4cc240dfaa
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9f653af8294002bf73b98bd4adc096fac8ba1658
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710484"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>Tabla única, Unique Schema, único catálogo propiedades dinámicos (ADO)
Le permite controlar las modificaciones realizadas en una tabla base concreta en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) que estaba formada por una operación de combinación en varias tablas base.  
  
-   **Tabla única** especifica el nombre de la tabla base en la que se permiten actualizaciones, inserciones y eliminaciones.  
  
-   **Esquema único** especifica la *esquema*, o el nombre del propietario de la tabla.  
  
-   **Catálogo único** especifica la *catálogo*, o el nombre de la base de datos que contiene la tabla.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** valor que es el nombre de una tabla, esquema o catálogo.  
  
## <a name="remarks"></a>Comentarios  
 La tabla base deseada se identifica por su catálogo, esquema y los nombres de tabla. Cuando el **Unique Table** propiedad está establecida, los valores de la **Unique Schema** o **Unique Catalog** propiedades se utilizan para buscar la tabla base. Se recomienda, aunque no es necesario, que uno o ambos el **Unique Schema** y **Unique Catalog** propiedades se establecen antes de la **Unique Table** propiedad está establecida.  
  
 La clave principal de la **Unique Table** se trata como la clave principal de todo el **Recordset**. Esta es la clave que se usa para cualquier método que requiere una clave principal.  
  
 Mientras **Unique Table** se establece, el [eliminar](../../../ado/reference/ado-api/delete-method-ado-recordset.md) método afecta solo a la tabla con nombre. El [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [actualización](../../../ado/reference/ado-api/update-method.md), y [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) métodos afectan a cualquier tabla base subyacente de la **Recordset**.  
  
 **Tabla única** debe especificarse antes de realizar cualquier sincronización personalizada. Si **Unique Table** no se ha especificado, el [resincronizar comando](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) propiedad no tiene ningún efecto.  
  
 Se produce un error de tiempo de ejecución si no se encuentra una única tabla base.  
  
 Estas propiedades dinámicas se anexan a la **Recordset** objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección cuando el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad está establecida en  **adUseClient**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
