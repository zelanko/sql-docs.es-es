---
description: Trabajo con datos multidimensionales
title: Trabajar con datos multidimensionales | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
author: rothja
ms.author: jroth
ms.openlocfilehash: 7c37f18f8bcaa3d0c1f78b3ddb8d0c6413fe7277
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452397"
---
# <a name="working-with-multidimensional-data"></a>Trabajo con datos multidimensionales
Un conjunto de *celdas* es el resultado de una consulta en datos multidimensionales. Consta de una colección de ejes, normalmente no más de cuatro ejes y, normalmente, solo dos o tres. Un *eje* es una colección de miembros de una o más dimensiones, que se utiliza para buscar o filtrar valores específicos de un cubo.  
  
 Una *posición* es un punto a lo largo de un eje. En el caso de un eje que conste de una sola dimensión, estas posiciones son un subconjunto de los miembros de la dimensión. Si un eje se compone de más de una dimensión, cada posición es una entidad compuesta, que tiene *n* partes, donde *n* es el número de dimensiones orientadas a lo largo de ese eje. Cada parte de la posición es un miembro de una dimensión constitutiva.  
  
 Por ejemplo, si las dimensiones geografía y producto de un cubo que contiene datos de ventas se orientan a lo largo del eje x de un objeto Cellset, una posición a lo largo de este eje puede contener los miembros "EE. UU." y "equipos". En este ejemplo, la determinación de una posición a lo largo del eje x requiere que los miembros de cada dimensión estén orientados a lo largo del eje.  
  
 Una *celda* es un objeto situado en la intersección de coordenadas del eje. Cada celda tiene varias partes de información asociadas, incluidos los propios datos, una cadena con formato (la forma que se pueda mostrar de los datos de la celda) y el valor ordinal de la celda. (Cada celda es un valor ordinal único en el Cellset. El valor ordinal de la primera celda del Cellset es cero, mientras que la celda situada más a la izquierda de la segunda fila de un Cellset con ocho columnas tendría un valor ordinal de ocho.  
  
 Por ejemplo, un cubo tiene las seis dimensiones siguientes (tenga en cuenta que este esquema de cubo difiere ligeramente del ejemplo dado en [información general de esquemas y datos multidimensionales](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)):  
  
-   SalesPerson  
  
-   Geografía (jerarquía natural): continentes, países, Estados, etc.  
  
-   Trimestres-trimestres, meses, días  
  
-   Years  
  
-   Measures-sales, PercentChange, BudgetedSales  
  
-   Productos  
  
 El siguiente Cellset representa las ventas de 1991 para todos los productos:  
  
> [!NOTE]
>  Los valores de celda del ejemplo se pueden ver como pares ordenados de los ordinales de posición del eje, donde el primer dígito representa la posición del eje x y el segundo dígito de la posición del eje y.  
  
 Las características de este Cellset son las siguientes:  
  
-   Dimensiones del eje: trimestres, vendedor, geografía  
  
-   Dimensiones de filtro: medidas, años, productos  
  
-   Dos ejes: columna (x, o eje 0) y fila (y o eje 1)  
  
-   eje x: dos dimensiones anidadas, vendedor y geografía  
  
-   eje y: dimensión Quarters  
  
 El eje x tiene dos dimensiones anidadas: vendedor y geografía. Desde la geografía, se seleccionan cuatro miembros: Seattle, Boston, EE. UU., sur y Japón. Se seleccionan dos miembros de vendedor: San Valentín y Nash. Esto produce un total de ocho posiciones en este eje (8 = 4 * 2).  
  
 Cada coordenada se representa como una posición con dos miembros: uno de la dimensión Salesperson y otro de la dimensión Geography:  
  
```console
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 El eje y solo tiene una dimensión, que contiene las ocho posiciones siguientes:  
  
```console
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 Celdas, celdas, ejes y posiciones se representan en ADO MD por los objetos correspondientes: [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md), [Cell](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [AXIS](../../../ado/reference/ado-md-api/axis-object-ado-md.md)y [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md).  
  
## <a name="see-also"></a>Consulte también  
 [Modelo de objetos de ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Información general de los esquemas y datos multidimensionales](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programar con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Uso de ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
