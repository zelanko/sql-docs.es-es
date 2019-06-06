---
title: Objeto de conjunto de celdas (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset
helpviewer_keywords:
- Cellset object [ADO MD]
ms.assetid: 5e2452c0-cac0-49b2-8099-836c35794d50
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 52ede9c21077c81dd1bd90f12acbfc3dff796d50
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709498"
---
# <a name="cellset-object-ado-md"></a>Objeto de conjunto de celdas (ADO MD)
Representa los resultados de una consulta multidimensional. Es una colección de celdas seleccionadas de cubos u otros conjuntos de celdas.  
  
## <a name="remarks"></a>Comentarios  
 Datos dentro de un **Cellset** se recupera mediante acceso directo a modo de matriz. Puede explorar en profundidad un miembro específico para obtener datos sobre ese miembro. Por ejemplo, el código siguiente devuelve el título del primer miembro en la primera posición del primer eje de un conjunto de celdas denominado `cst`:  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>Comentarios  
 No hay ninguna noción de una celda actual dentro de un conjunto de celdas. En su lugar, el [elemento](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propiedad recupera un determinado [celda](../../../ado/reference/ado-md-api/cell-object-ado-md.md) objeto desde el conjunto de celdas. Los argumentos de la **elemento** propiedad determinan qué celda se recupera. Puede especificar el valor ordinal único de una celda. También puede recuperar las celdas mediante el uso de sus números de posición a lo largo de cada eje del conjunto de celdas. Para obtener más información acerca de cómo recuperar las celdas, vea el [elemento](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propiedad.  
  
 Con las colecciones, métodos y propiedades de un **Cellset** objeto, puede hacer lo siguiente:  
  
-   Asociar una conexión abierta con un **Cellset** objeto estableciendo sus [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) propiedad.  
  
-   Ejecutar y recuperar los resultados de una consulta multidimensional con la [abierto](../../../ado/reference/ado-md-api/open-method-ado-md.md) método.  
  
-   Recuperar un **celda** desde el **Cellset** con el [elemento](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propiedad.  
  
-   Devolver el [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md) objetos que definen el **Cellset** con el [ejes](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) colección.  
  
-   Recuperar información acerca de las dimensiones usadas para filtrar los datos en el **Cellset** con el [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) propiedad.  
  
-   Devolver o especificar la consulta utilizada para definir el **Cellset** con el [origen](../../../ado/reference/ado-md-api/source-property-ado-md.md) propiedad.  
  
-   Devolver el estado actual de la **Cellset** (abierto, cerrado, ejecución o conectando) con el [estado](../../../ado/reference/ado-md-api/state-property-ado-md.md) propiedad.  
  
-   Cerrar una apertura **Cellset** con el [cerrar](../../../ado/reference/ado-md-api/close-method-ado-md.md) método.  
  
-   Recuperar información específica del proveedor sobre el **Cellset** con el estándar de ADO [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de conjunto de celdas (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Colección Axes (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
