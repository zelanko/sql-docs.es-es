---
title: Región de datos Tablix (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 99f83b32-4b86-4d40-973c-9a328d23ac8b
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0d5360091fbf0ece381b8b7444fdd8e225238563
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33028882"
---
# <a name="tablix-data-region-report-builder-and-ssrs"></a>Región de datos Tablix (Generador de informes y SSRS)
  En [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)], la región de datos Tablix es un elemento de informe de diseño generalizado que muestra los datos del informe paginado en celdas organizadas en filas y columnas. Los datos del informe pueden ser datos detallados tal y como se recuperan del origen de datos, o datos detallados agregados organizados en grupos previamente especificados. Cada celda de Tablix puede contener cualquier elemento de informe, como un cuadro de texto o una imagen, o bien otra región de datos, como una región de Tablix, un gráfico o un medidor. Para agregar varios elementos de informe a una celda, agregue primero un rectángulo que actúe como contenedor. Después, agregue los elementos de informe al rectángulo.  
  
 Las regiones de datos de tabla, matriz y lista se representan en la cinta de opciones mediante plantillas para la región de datos Tablix subyacente. Al agregar una de estas plantillas a un informe, en realidad se está agregando una región de datos Tablix que está optimizada para un diseño de datos concreto. De forma predeterminada, una plantilla de tabla muestra datos detallados en un diseño de cuadrícula, una matriz muestra datos de grupo en un diseño de cuadrícula y una lista muestra datos detallados en un diseño de forma libre.  
  
 De forma predeterminada, cada celda de Tablix de una tabla o matriz contiene un cuadro de texto. La celda de una lista contiene un rectángulo. Puede reemplazar un elemento de informe predeterminado por un elemento de informe diferente, como una imagen.  
  
 Cuando se definen grupos para una tabla, una matriz o una lista, el Generador de informes y el Diseñador de informes agregan filas y columnas a la región de datos Tablix en que se van a mostrar los datos agrupados.  
  
 Para entender la región de datos Tablix, debe entender primero lo siguiente:  
  
*   La diferencia que existe entre datos detallados y datos agrupados.  
  
*   Los grupos, que se organizan como miembros de jerarquías de grupo, en el eje horizontal como grupos de filas y en el eje vertical como grupos de columnas.  
  
*  El propósito de las celdas de Tablix en las cuatro áreas de una región de datos Tablix: el cuerpo, los encabezados de grupo de filas, los encabezados de grupo de columnas y la esquina.  
  
*  Las filas y columnas estáticas y dinámicas, y cómo se relacionan con los grupos.  
  
 En este artículo se detallan estos conceptos para explicar la estructura que el Generador de informes y el Diseñador de informes agregan automáticamente al agregar plantillas y crear grupos para que pueda modificar dicha estructura de acuerdo a sus propias necesidades. El Generador de informes y el Diseñador de informes proporcionan varios indicadores visuales que le ayudan a reconocer la estructura de la región de datos Tablix. Para más información, vea [Celdas, filas y columnas de la región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-detail-and-grouped-data"></a>Descripción de los datos detallados y los datos agrupados  
 Los datos detallados son todos los datos de un conjunto de datos de informe tal y como se recuperan del origen de datos. Los datos detallados son básicamente lo que se ve en el panel de resultados del diseñador de consultas al ejecutar una consulta de conjunto de datos. Los datos detallados reales incluyen campos calculados creados por el usuario, y están restringidos por filtros establecidos en el conjunto de datos, la región de datos y el grupo de detalles. Para mostrar datos detallados en una fila de detalles, use una expresión simple como [Quantity]. Cuando se ejecuta el informe, la fila de detalles se repite una vez en tiempo de ejecución para cada fila de los resultados de la consulta.  
  
 Los datos agrupados son datos detallados que se organizan por un valor especificado en la definición de grupo, como [SalesOrder]. Para mostrar datos agrupados en filas y columnas de grupo, use expresiones simples que agreguen los datos agrupados, como [Sum(Quantity)]. Para obtener más información, vea [Descripción de los grupos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
## <a name="understanding-group-hierarchies"></a>Descripción de las jerarquías de grupo  
 Los grupos se organizan como miembros de jerarquías de grupos. Las jerarquías de grupos de filas y de columnas son estructuras idénticas en ejes diferentes. Piense en los grupos de columnas como elementos que se expanden a lo ancho de la página y en los grupos de filas como elementos que se expanden hacia abajo.  
  
 Una estructura de árbol representa grupos de filas y de columnas anidados que tienen una relación de elementos primarios y secundarios como, por ejemplo, una categoría con subcategorías. El grupo primario es la raíz del árbol y los grupos secundarios son sus bifurcaciones. Los grupos también pueden tener una relación adyacente independiente, como por ejemplo ventas por territorio y ventas por año. Varias jerarquías de árbol no relacionadas reciben el nombre de bosque. En una región de datos Tablix, los grupos de filas y los grupos de columnas se representan como bosques independientes. Para obtener más información, vea [Descripción de los grupos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
## <a name="understanding-tablix-data-region-areas"></a>Descripción de las áreas de la región de datos Tablix  
 Una región de datos Tablix tiene cuatro áreas posibles para las celdas: la esquina de Tablix, la jerarquía de grupos de filas de Tablix, la jerarquía de grupos de columnas de Tablix y el cuerpo de Tablix. El cuerpo de Tablix siempre existe. Las demás áreas son opcionales.  
  
 Las celdas del área del cuerpo de Tablix muestran datos detallados y de grupo.  
  
 Las celdas del área de grupos de filas se crean automáticamente al crear un grupo de filas. Éstas son celdas de encabezado de grupo de filas y muestran valores de instancia de grupo de filas de forma predeterminada. Por ejemplo, al agrupar por [SalesOrder], los valores de instancia de grupo son los pedidos de venta individuales por los que se está realizando la agrupación.  
  
 Las celdas del área de grupos de columnas se crean automáticamente al crear un grupo de columnas. Son celdas de encabezado de grupo de columnas y muestran valores de instancia de grupo de columnas de forma predeterminada. Por ejemplo, al agrupar por [Year], los valores de instancia de grupo son los años individuales por los que realiza la agrupación.  
  
 Las celdas del área de esquina de Tablix se crean automáticamente al definir los grupos de filas y de columnas. Las celdas de esta área pueden mostrar etiquetas, o puede combinar las celdas y crear un título.  
  
 Para obtener más información, vea [Describir las áreas de la región de datos Tablix &#40;Generador de informes y SSRS&#41](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md).  
  
## <a name="understanding-static-and-dynamic-rows-and-columns"></a>Descripción de las filas y columnas estáticas y dinámicas  
 Una región de datos Tablix organiza las celdas en filas y columnas que están asociadas a grupos. Las estructuras de grupo para los grupos de filas y las columnas son idénticas. Este ejemplo utiliza los grupos de filas, pero puede aplicar los mismos conceptos a grupos de columna.  
  
 Una fila puede ser estática o dinámica. Una fila estática no está asociada con un grupo. Cuando se ejecuta el informe, una fila estática se representa una vez. Los encabezados y pies de tabla son filas estáticas. Las filas estáticas muestran etiquetas y totales. El ámbito de las celdas de una fila estática es la región de datos.  
  
 Una fila dinámica está asociada con uno o más grupos. Una fila dinámica se representa una vez para cada valor de grupo único en el grupo más interno. El ámbito de las celdas de una fila dinámica es el grupo de filas y el grupo de columnas más interno a los que pertenece la celda.  
  
 Las filas de detalles dinámicas están asociadas al grupo de detalles que se crea automáticamente al agregar una tabla o lista a la superficie de diseño. Por definición, el grupo de detalles es el grupo más interno de una región de datos Tablix. Las celdas de las filas de detalles muestran datos detallados.  
  
 Las filas de grupo dinámicas se crean al agregar un grupo de filas o un grupo de columnas a una región de datos Tablix existente. Las celdas de las filas de grupo dinámicas muestran valores agregados para el ámbito predeterminado.  
  
 La característica Agregar total crea automáticamente una fila fuera del grupo actual en la que mostrar valores cuyo ámbito es el grupo. También puede agregar filas estáticas y dinámicas manualmente. Los indicadores visuales le ayudan a entender qué filas son estáticas y qué filas son dinámicas. Para más información, vea [Celdas, filas y columnas de la región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Ver también  
 [Vincular varias regiones de datos al mismo conjunto de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Controlar la presentación de la región de datos Tablix en una página de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)   
 [Explorar la flexibilidad de una región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)   
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
