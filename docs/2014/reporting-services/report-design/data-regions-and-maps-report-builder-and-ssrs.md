---
title: Regiones de datos y mapas (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data regions
ms.assetid: 3afb8874-b36c-4e44-a0d8-80d2f7135fb1
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a130b04ab18fc22bf1a028cea38d093e4b48f24c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37206645"
---
# <a name="data-regions-and-maps-report-builder-and-ssrs"></a>Regiones de datos y mapas (Generador de informes y SSRS)
  Una región de datos es un objeto de un informe que muestra los datos de un conjunto de datos de informe. Los datos de informe se pueden mostrar como números y texto en una tabla, matriz o lista, gráficamente en un gráfico o medidor, y sobre un fondo geográfico en un mapa. Las tablas, las matrices y las listas están basadas en la región de datos *Tablix* , que se expande cuando es necesario para mostrar todos los datos del conjunto de datos. Una región de datos Tablix admite varios grupos de filas y columnas, tanto estáticas como dinámicas. En un gráfico se representan diversas series y grupos de categorías en una variedad de formatos de gráfico. Un medidor muestra un valor único o un valor agregado para un conjunto de datos. Un mapa muestra datos espaciales como elementos de mapa cuya apariencia puede variar según los datos agregados de un conjunto de datos.  
  
 Puede guardar una región de datos o asignarla como un elemento de informe. [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="table"></a>Table  
 Una tabla es una región de datos que muestra los datos fila por fila. La columnas de tabla son estáticas: el número de columnas del informe se define al diseñarlo. Las filas de tabla son dinámicas: se expanden hacia abajo para incluir los datos. Se pueden agregar grupos a las tablas, que organizan los datos por campos o expresiones seleccionados. Para obtener información sobre cómo agregar una tabla a un informe, vea [Tablas &#40;Generador de informes y SSRS&#41;](tables-report-builder-and-ssrs.md).  
  
## <a name="matrix"></a>Matriz  
 Las matrices también se denominan tablas de referencias cruzadas. Una región de datos de matriz contiene columnas y filas dinámicas: se expanden para dar cabida a los datos. Una matriz puede tener columnas y filas dinámicas y estáticas. Las columnas o las filas pueden contener otras columnas o filas, y se pueden usar para agrupar datos. Para obtener información acerca de cómo agregar una matriz a un informe, vea [Matrices &#40;generador de informes y SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)  
  
## <a name="list"></a>Lista  
 Una lista es una región de datos que muestra los datos organizados con un formato libre. Los elementos de informe se pueden organizar para crear un formulario con cuadros de texto, imágenes y otras regiones de datos colocadas en cualquier lugar de la lista. Para obtener información acerca de cómo agregar una lista a un informe, vea [enumera &#40;generador de informes y SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
## <a name="chart"></a>Gráfico  
 Un gráfico muestra los datos de forma gráfica. Los gráficos de barras, circulares y de líneas son algunos ejemplos, pero se admiten muchos más estilos. Para obtener información acerca de cómo agregar un gráfico a un informe, vea [gráficos &#40;generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
## <a name="gauge"></a>Medidor  
 Un medidor presenta los datos como un intervalo con un indicador que señala a un valor concreto dentro del intervalo. Los medidores se utilizan para mostrar indicadores clave de rendimiento (KPI) y otras métricas. Los medidores pueden ser lineales y circulares. Para obtener más información acerca de cómo agregar un medidor a un informe, vea [medidores &#40;generador de informes y SSRS&#41;](gauges-report-builder-and-ssrs.md).  
  
## <a name="map"></a>Mapa  
 Con los mapas podrá presentar datos comparándolos con un entorno geográfico. Los datos del mapa pueden ser datos espaciales de una consulta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , un archivo de forma ESRI o mosaicos Bing Map de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Los datos espaciales están formados por conjuntos de coordenadas que definen polígonos que representan formas o áreas, líneas que representan rutas o rutas de acceso, y puntos representados por marcadores. Puede asociar los datos agregados a elementos de asignación para modificar automáticamente su color y tamaño. Por ejemplo, puede cambiar el tipo de marcador para una tienda según la cantidad de ventas o el color de una carretera según el límite de velocidad. Para obtener más información, vea [Mapas &#40;Generador de informes y SSRS&#41;](maps-report-builder-and-ssrs.md).  
  
## <a name="data-regions-in-the-report-layout"></a>Regiones de datos del diseño del informe  
 Es posible agregar varias regiones de datos a un informe. Las regiones de datos crecen para alojar los datos del conjunto de datos de informe al que están vinculadas. Por ejemplo, una matriz que muestra las ventas anuales de cada producto tiene un grupo de filas basado en los nombres del producto y un grupo de columnas basado en los años. Al ejecutar el informe, la matriz se expande hacia abajo en la página para cada producto y hacia los lados para cada año. Un gráfico que se coloque junto a la matriz en la superficie de diseño del informe se mostrará junto a la matriz expandida en el informe representado. La manera de representar las regiones de datos en una página sigue un conjunto de reglas basadas en el formato de salida de un informe. Por ejemplo, para ayudar a controlar el modo en que un gráfico y una matriz se representan en una página, puede usar un rectángulo como contenedor o anidar ambas regiones de datos en una lista. Para obtener más información, consulte [representación y diseño de página &#40;generador de informes y SSRS&#41;](page-layout-and-rendering-report-builder-and-ssrs.md).  
  
## <a name="nested-data-regions"></a>Regiones de datos anidadas  
 Se pueden anidar regiones de datos en otras regiones de datos. Por ejemplo, si desea crear un registro de ventas para cada vendedor de una base de datos, puede crear una lista con cuadros de texto y una imagen que muestre información acerca del empleado y, a continuación, agregar regiones de datos tabulares y gráficas a la lista para mostrar el registro de ventas del empleado. Para obtener más información, vea [Anidar regiones de datos &#40;Generador de informes y SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md).  
  
## <a name="multiple-data-regions-linked-to-the-same-dataset"></a>Varias regiones de datos vinculadas al mismo conjunto de datos  
 Puede vincular más de una región de datos al mismo conjunto de datos para proporcionar vistas diferentes de los mismos datos. Por ejemplo, puede mostrar los mismos datos en una tabla y en un gráfico. Puede crear el informe para que proporcione botones de ordenación interactivos en la tabla. De ese modo, al ordenar la tabla, el gráfico también se ordenará automáticamente. Para obtener más información, consulte [vincular varias regiones de datos al mismo conjunto de datos &#40;generador de informes y SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md).  
  
## <a name="data-for-a-data-region"></a>Datos para una región de datos  
 Cada Tablix, gráfico y medidor están diseñados para mostrar los datos de un solo conjunto de datos. Un mapa muestra los datos espaciales y los datos analíticos de los mismos conjuntos de datos o de conjuntos de datos distintos. También puede incluir valores de conjuntos de datos que no están vinculados a la región de datos de las maneras siguientes:  
  
-   Valores agregados que no dependen de un criterio de ordenación o agrupación cuyo ámbito está definido para un conjunto de datos diferente.  
  
-   Valores de búsqueda de pares de nombre/valor en un conjunto de datos diferente.  
  
 Para más información, vea [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Conceptos de creación de informes &#40;generador de informes y SSRS&#41;](report-authoring-concepts-report-builder-and-ssrs.md)   
 [Los informes, elementos de informe y definiciones de informe &#40;generador de informes y SSRS&#41;](reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Representación y diseño de páginas &#40;Generador de informes y SSRS&#41;](page-layout-and-rendering-report-builder-and-ssrs.md)   
 [Tutoriales &#40;generador de informes&#41;](../report-builder-tutorials.md)   
 [Tutoriales de Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  
  
  
