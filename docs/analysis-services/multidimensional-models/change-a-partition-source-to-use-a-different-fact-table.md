---
title: "Cambiar el origen de una partici&#243;n para usar una tabla de hechos diferente | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "tablas de hechos [Analysis Services]"
  - "particiones [Analysis Services], tablas de hechos"
ms.assetid: 5508312f-8e46-4802-9362-6688ca03d098
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 29
---
# Cambiar el origen de una partici&#243;n para usar una tabla de hechos diferente
  Cuando se crea una partición para un cubo, se puede usar una tabla de hechos diferente. Las tablas diferentes pueden proceder de una única vista del origen de datos, de diferentes vistas del origen de datos o de diferentes orígenes de datos. Una vista del origen de datos también puede contener tablas diferentes de más de un origen de datos.  
  
 Todas las tablas de hechos y dimensiones correspondientes a las particiones de un cubo deben tener la misma estructura que la tabla de hechos y las dimensiones del cubo. Por ejemplo, varias tablas de hechos pueden tener la misma estructura pero contener datos de años distintos o de líneas de productos diferentes.  
  
 La tabla de hechos se especifica en la página **Especificar información de origen** del Asistente para particiones. En esta página, en el grupo Origen de la partición que hay al lado de **Buscar en**, especifique un origen de datos o una vista del origen de datos en la que se debe buscar. A continuación, haga clic en **Buscar tablas**y, a continuación, en **Tablas disponibles**, seleccione la tabla que desea usar.  
  
 Cuando utilice tablas de hechos diferentes, asegúrese de que no hay datos duplicados en las distintas particiones. Por ejemplo, si una tabla de hechos contiene únicamente transacciones del año 2012 y otra solo contiene transacciones correspondientes a 2013, ambas contienen datos independientes. Igualmente son independientes las tablas de hechos correspondientes a líneas de productos o a áreas geográficas distintas.  
  
 Es posible, pero no se recomienda, utilizar diferentes tablas de hechos que contengan datos duplicados. En este caso, debe utilizar filtros en las particiones para asegurarse de que los datos empleados por una partición no serán utilizados por ninguna otra. Para más información, vea [Crear y administrar una partición local &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md).  
  
## Vea también  
 [Crear y administrar una partición local &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)  
  
  