---
title: "Procesar datos (SSAS tabular) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d88f2dc9-2933-4be5-9bf3-48ffbc2d0a1a
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 14
---
# Procesar datos (SSAS tabular)
  Cuando se importan datos en un modelo tabular en modo de almacenamiento en caché, se captura una instantánea de esos datos en el momento de la importación. En algunos casos, esos datos nunca cambian y no es necesario actualizarlos en el modelo. Sin embargo, es más probable que los datos que se importan cambien con regularidad, y para que el modelo refleje los datos más recientes de los orígenes de datos, es necesario procesar (actualizar) los datos y recalcular los datos calculados. Para actualizar los datos del modelo, deberá realizar una acción de procesamiento en todas las tablas o en una tabla individual, mediante una partición o mediante una conexión de origen de datos.  
  
 Al crear el proyecto de modelos, las acciones de procesamiento se deben iniciar manualmente en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Una vez implementado el modelo, las operaciones de procesamiento se pueden realizar utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o programar mediante un script. Todas las tareas aquí descritas pertenecen a acciones de procesamiento que puede realizar durante la creación de modelos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para más información sobre las acciones de procesamiento para un modelo implementado, vea [Procesar base de datos, tabla o partición &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md).  
  
## Tareas relacionadas  
  
|Tema|Description|  
|-----------|-----------------|  
|[Procesar manualmente los datos &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/manually-process-data-ssas-tabular.md)|Describe cómo procesar manualmente los datos del área de trabajo del modelo.|  
|[Solucionar problemas del procesamiento de datos &#40;SSAS tabular&#41;](../../analysis-services/troubleshoot-process-data-ssas-tabular.md)|Describe cómo solucionar problemas de operaciones de proceso.|  
  
  