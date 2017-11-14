---
title: Objeto de conjunto de celdas (ADO MD) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Cellset
helpviewer_keywords:
- Cellset object [ADO MD]
ms.assetid: 5e2452c0-cac0-49b2-8099-836c35794d50
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f53e9ec68a4375a9c8d07dc3937750c2e7ba3d46
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="cellset-object-ado-md"></a>Objeto de conjunto de celdas (ADO MD)
Representa los resultados de una consulta multidimensional. Es una colección de celdas seleccionadas de cubos u otros conjuntos de celdas.  
  
## <a name="remarks"></a>Comentarios  
 Datos dentro de un **Cellset** se recupera mediante acceso directo en forma de matriz. Puede desglosar un miembro específico para obtener datos sobre ese miembro. Por ejemplo, el código siguiente devuelve el título del primer miembro de la primera posición en el primer eje de un conjunto de celdas con nombre `cst`:  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>Comentarios  
 No hay ninguna noción de una celda actual dentro de un conjunto de celdas. En su lugar, el [elemento](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propiedad recupera un determinado [celda](../../../ado/reference/ado-md-api/cell-object-ado-md.md) objeto desde el conjunto de celdas. Los argumentos de la **elemento** propiedad determinan la celda que se recupera. Puede especificar el valor ordinal único de una celda. También puede recuperar celdas mediante sus números de posición a lo largo de cada eje del conjunto de celdas. Para obtener más información sobre cómo recuperar celdas, vea el [elemento](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propiedad.  
  
 Con las colecciones, métodos y propiedades de un **Cellset** objeto, puede hacer lo siguiente:  
  
-   Asociar una conexión abierta con un **Cellset** objeto estableciendo su [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) propiedad.  
  
-   Ejecutar y recuperar los resultados de una consulta multidimensional con la [abiertos](../../../ado/reference/ado-md-api/open-method-ado-md.md) método.  
  
-   Recuperar un **celda** desde el **Cellset** con el [elemento](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propiedad.  
  
-   Devolver el [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md) objetos que definen la **Cellset** con el [ejes](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) colección.  
  
-   Recuperar información acerca de las dimensiones que se usan para filtrar los datos en el **Cellset** con el [PivotView](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) propiedad.  
  
-   Devolver o especificar la consulta utilizada para definir la **Cellset** con el [origen](../../../ado/reference/ado-md-api/source-property-ado-md.md) propiedad.  
  
-   Devolver el estado actual de la **Cellset** (abierto, cerrado, en ejecución o en conexión) con la [estado](../../../ado/reference/ado-md-api/state-property-ado-md.md) propiedad.  
  
-   Cerrar abierto **Cellset** con el [cerrar](../../../ado/reference/ado-md-api/close-method-ado-md.md) método.  
  
-   Recuperar información específica del proveedor sobre la **Cellset** con ADO estándar [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de conjunto de celdas (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Colección Axes (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)

