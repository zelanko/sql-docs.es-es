---
title: Trabajar con datos multidimensionales | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f7721018d887fdb4c24293c4076f384167f38a55
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695083"
---
# <a name="working-with-multidimensional-data"></a>Trabajo con datos multidimensionales
Un *cellset* es el resultado de una consulta de datos multidimensionales. Consta de una colección de ejes, normalmente no más de cuatro ejes y normalmente sólo dos o tres. Un *eje* es una colección de miembros de una o varias dimensiones, que se usa para buscar o filtrar valores específicos de un cubo.  
  
 Un *posición* es un punto de un eje. Para un eje que consta de una sola dimensión, estas posiciones son un subconjunto de los miembros de dimensión. Si un eje consta de más de una dimensión, cada posición es una entidad compuesta, que tiene *n* partes where *n* es el número de dimensiones orientadas a lo largo del eje. Cada parte de la posición es un miembro de una dimensión constituyente.  
  
 Por ejemplo, si las dimensiones de geografía y producto de un cubo que contiene los datos de ventas se orientan a lo largo del eje x de un conjunto de celdas, una posición a lo largo de este eje puede contener a los miembros "EE" y "Equipos". En este ejemplo, para determinar una posición a lo largo del eje x requiere que los miembros de cada dimensión se orientan a lo largo del eje.  
  
 Un *celda* es un objeto situado en la intersección de coordenadas del eje. Cada celda tiene varias piezas de información asociada con él, incluidos los propios datos, una cadena con formato (el formulario que se puede mostrar de los datos de celda) y el valor ordinal de la celda. (Cada celda es un valor ordinal único en el conjunto de celdas. El valor ordinal de la primera celda en el conjunto de celdas es cero, mientras que la celda situada en la segunda fila de un conjunto de celdas con ocho columnas tendría un valor ordinal de ocho.)  
  
 Por ejemplo, un cubo tiene las seis dimensiones siguientes (tenga en cuenta que este esquema de cubo difiere ligeramente el ejemplo proporcionado [información general de esquemas y datos multidimensionales](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)):  
  
-   Empleado de ventas  
  
-   Zona geográfica (jerarquía natural): continentes, países, Estados etc.  
  
-   Trimestres: Días de trimestres, meses,  
  
-   Years  
  
-   Medidas: Ventas, CambioPorcentual, VentasPresupuestadas  
  
-   Productos  
  
 El siguiente conjunto de celdas representa las ventas de 1991 para todos los productos:  
  
> [!NOTE]
>  Los valores de celda en el ejemplo pueden verse como pares ordenados de ordinales de posición del eje donde el primer dígito representa la posición del eje x y el segundo dígito de la posición del eje y.  
  
 Las características de este conjunto de celdas son los siguientes:  
  
-   Dimensiones de eje: trimestres, vendedor, Geography  
  
-   Filtrar las dimensiones: medidas, años, productos  
  
-   Dos ejes: columna (x, o eje 0) y fila (y o eje 1)  
  
-   eje x: dos dimensiones anidadas, vendedor y Geography  
  
-   eje y: dimensión trimestres  
  
 El eje x tiene dos dimensiones anidadas: vendedor y geografía. Desde la ubicación geográfica, se seleccionan los cuatro miembros: Seattle, Boston, sur de EE. UU. y Japón. De vendedor se seleccionan dos miembros: Valentine y Nash. Esto da como resultado un total de ocho posiciones en este eje (8 = 4 * 2).  
  
 Cada coordenada se representa como una posición con dos miembros: uno de la dimensión vendedor y otro de la dimensión Geography:  
  
```  
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 El eje y sólo tiene una dimensión, que contiene las ocho posiciones siguientes:  
  
```  
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 Conjuntos de celdas, las celdas, ejes y posiciones se representan en ADO MD mediante los objetos correspondientes: [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md), [celda](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md), y [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md).  
  
## <a name="see-also"></a>Vea también  
 [Modelo de objetos ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Información general de esquemas y datos multidimensionales](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programar con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Uso de ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
