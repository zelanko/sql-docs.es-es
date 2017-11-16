---
title: Medidas | Documentos de Microsoft
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27ec8f99-e9ef-44c9-a83f-f7c88e128ad3
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 38b7467cd4ad765d651ea0ebe4ad57c278c987a1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="measures"></a>medidas
  En los modelos tabulares, una medida es un cálculo creado usando una fórmula DAX para usarla en un cliente de informes. Las medidas se evalúan según los campos, filtros y segmentaciones de datos que los usuarios seleccionan en la aplicación cliente de informes.  
  
##  <a name="bkmk_understanding"></a> Ventajas  
 Las medidas pueden estar basadas en funciones de agregación estándar, como AVERAGE, COUNT o SUM, o puede definir su propia fórmula mediante DAX. Además de la fórmula, las medidas tienen propiedades definidas por el tipo de datos de la medida, como el nombre, los detalles de la tabla, el formato y las posiciones decimales.  
  
 Si se definen medidas en un modelo, los usuarios podrán agregarlas a un informe o a una tabla dinámica. Según las perspectivas y los roles, las medidas aparecen en la lista de campos con su tabla asociada y están disponibles para todos los usuarios del modelo. Normalmente, las medidas se crean en tablas de hechos; sin embargo, pueden ser independientes de la tabla con la que están asociadas.  
  
 Es importante comprender las diferencias fundamentales entre una columna calculada y una medida. En una columna calculada, la fórmula se evalúa como un valor para cada fila de la columna. Por ejemplo, en una tabla FactSales, una columna calculada denominada TotalProfit con la fórmula siguiente calcula un valor para el beneficio total de cada fila (una fila por venta) en la tabla FactSales:  
  
```  
=[SalesAmount] - [TotalCost] - [ReturnAmount]  
```  
  
 La columna calculada TotalProfit se puede usar en un cliente de informes como cualquier otra columna.  
  
 Por su parte, una medida se evalúa como un valor basado en una selección del usuario; un contexto de filtro establecido en una tabla dinámica o en un informe. Por ejemplo, en la tabla FactSales se crea una medida con la fórmula siguiente:  
  
```  
Sum of TotalProfit: =SUM([TotalProfit])  
```  
  
 Un analista de ventas, usando Excel, desea conocer el beneficio total de una categoría de productos. Cada categoría de producto consta de varios productos. El analista de ventas selecciona la columna ProductCategoryName y la agrega a la ventana de filtro Etiquetas de fila de una tabla dinámica; de esta forma, se mostrará una fila para cada categoría de producto en la tabla dinámica. A continuación, el usuario selecciona la medida Sum of TotalProfit. Se agregará una medida de forma predeterminada a la ventana de filtro Valores. La medida calcula la suma del beneficio total y muestra los resultados de cada categoría de producto. El analista de ventas puede filtrar aún más la suma del beneficio total para cada categoría de producto mediante una segmentación de datos; por ejemplo, agregando CalendarYear como segmentación para ver la suma del beneficio total anual para cada categoría de producto.  
  
|ProductCategoryName|Sum of TotalProfit|  
|-------------------------|------------------------|  
|Audio|$2,731,061,308.69|  
|Cameras and Camcorders|$620,623,675.75|  
|Computers|$392,999,044.59|  
|Tv and Video|$946,989,702.51|  
|**Total general**|**$4,691,673,731.53**|  
  
##  <a name="bkmk_def_mg"></a> Defining measures by using the measure grid  
 Las medidas se crean en tiempo de diseño mediante la cuadrícula de medidas en el diseñador de modelos. Cada tabla tiene una cuadrícula de medidas. De forma predeterminada, la cuadrícula de medidas aparece debajo de cada tabla en el diseñador de modelos. También puede optar por no ver la cuadrícula de medidas de una determinada tabla. Para alternar entre las visualizaciones de la cuadrícula de medidas de una tabla, haga clic en el menú **Tabla** y, a continuación, en **Mostrar cuadrícula de medidas**.  
  
 En la cuadrícula de medidas, puede crear medidas de las maneras siguientes:  
  
-   Haga clic en una celda vacía de la cuadrícula de medidas y, a continuación, escriba una fórmula de DAX en la barra de fórmulas. Al hacer clic en ENTRAR para completar la fórmula, la medida aparecerá en la celda de la cuadrícula de medidas.  
  
-   Cree una medida mediante una función de agregación estándar; para ello, haga clic en una columna, haga clic en el botón de autosuma (∑) de la barra de herramientas y, por último, haga clic en una función de agregación estándar. Las agregaciones estándar son: Sum, Average, Count, DistinctCount, Max, Min. Las medidas creadas mediante el botón de autosuma siempre aparecerán directamente en la cuadrícula de medidas debajo de la columna.  
  
 De forma predeterminada, cuando se usa la autosuma, el nombre de la medida viene definido por el nombre de la columna asociada seguido de un signo de dos puntos y de la fórmula. Dicho nombre se puede cambiar en la barra de fórmulas o en el valor de la propiedad **Nombre de medida** en la ventana Propiedades. Al crear una medida mediante una fórmula personalizada, puede escribir un nombre en la barra de fórmulas, seguido de un signo de dos puntos y de la fórmula, o puede escribir un nombre en el valor de la propiedad **Nombre de medida** en la ventana Propiedades.  
  
 Es importante para las medidas de nombre con cuidado. El nombre de la medida aparecerá con la tabla asociada en la lista de campos del cliente de informes. También se asignará el nombre a un KPI en función de la medida base. Las medidas no pueden tener el mismo nombre que cualquier columna de cualquier tabla del modelo.  
  
> [!TIP]  
>  Puede agrupar en una tabla medidas de varias tablas si crea una tabla vacía y mueve a esa tabla las medidas o crea nuevas medidas en ella. Tenga en cuenta que quizás necesite incluir los nombres de tabla en las fórmulas DAX al hacer referencia a columnas de otras tablas.  
  
 Si se han definido perspectivas para el modelo, las medidas no se agregarán automáticamente a ninguna de ellas. Deberá agregarlas manualmente mediante el cuadro de diálogo Perspectivas. Para obtener más información, consulte [perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md).  
  
##  <a name="bkmk_properties"></a> Propiedades de medidas  
 Cada medida tiene propiedades que la definen. Las propiedades de las medidas, junto con las propiedades de las columnas asociadas, se pueden modificar en la ventana Propiedades. Las medidas tienen las propiedades siguientes:  
  
|Propiedad|Valor predeterminado|Description|  
|--------------|---------------------|-----------------|  
|**Description**|En blanco|Descripción de la medida. La descripción no aparecerá con la medida en un cliente de informes.|  
|**Formato**|Se determina automáticamente a partir del tipo de datos de la columna a la que se hace referencia en la expresión de la fórmula.|El formato de la medida. Por ejemplo, moneda o porcentaje.|  
|**Fórmula**|La fórmula especificada en la barra de fórmulas al crear la medida.|La fórmula de la medida.|  
|**Nombre de medida**|Si se usa la autosuma, el nombre de la medida estará precedido por el nombre de la columna seguido de un signo de dos puntos. Si se especifica una fórmula personalizada, escriba un nombre seguido de un signo de dos puntos y, a continuación, la fórmula.|El nombre de la medida tal como se muestra en la lista de campos de un cliente de informes.|  
  
##  <a name="bkmk_KPI"></a> Usar una medida en un KPI  
 Un KPI (indicador clave de rendimiento) viene definido por un valor *base* , definido a su vez por una medida, con respecto a un valor de *destino* , también definido por una medida o por un valor absoluto. Los KPI también incluyen un *estado*, un cálculo en el que se evalúa el valor base con respecto al valor de destino entre los umbrales, mostrado en formato gráfico. Los KPI los usan a menudo los profesionales de las empresas para identificar tendencias en métricas empresariales críticas.  
  
 Cualquier medida puede servir como medida base de un KPI. Para crear un KPI, haga clic con el botón derecho en una medida en la cuadrícula de medidas y, después, haga clic en **Crear KPI**. Aparecerá el cuadro de diálogo Indicador clave de rendimiento, donde podrá especificar un valor de destino (definido por una medida o un valor absoluto) y definir umbrales de estado, así como un tipo de gráfico. Para obtener más información, consulte [KPI](../../analysis-services/tabular-models/kpis-ssas-tabular.md).  
  
##  <a name="bkmk_rel_tasks"></a> Tareas relacionadas  
  
|Tema|Description|  
|-----------|-----------------|  
|[Crear y administrar medidas](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md)|Describe cómo crear y administrar medidas mediante la cuadrícula de medidas del diseñador de modelos.|  
  
## <a name="see-also"></a>Vea también  
 [KPI](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [Crear y administrar KPI](../../analysis-services/tabular-models/create-and-manage-kpis-ssas-tabular.md)   
 [Columnas calculadas](../../analysis-services/tabular-models/ssas-calculated-columns.md)  
  
  

