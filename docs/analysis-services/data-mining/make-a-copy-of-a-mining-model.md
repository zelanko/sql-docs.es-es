---
title: "Realizar una copia de un modelo de miner&#237;a de datos | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modelos de minería de datos [Analysis Services], copiar"
  - "modelos de minería de datos [Analysis Services], crear"
  - "modelos de minería de datos [Analysis Services], temas de procedimientos"
  - "copiar modelos de minería de datos"
ms.assetid: 7975bb02-f188-49a0-b7de-5b9b216254ad
caps.latest.revision: 12
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 12
---
# Realizar una copia de un modelo de miner&#237;a de datos
  La creación de una copia de un modelo de minería de datos resulta útil para crear rápidamente varios modelos de minería de datos basados en los mismos datos. Una vez copiado el modelo, puede modificar la nueva copia de este si cambia los parámetros o agrega un filtro.  
  
 Por ejemplo, si tiene una tabla Customers que está vinculada a una tabla de compras, puede crear copias para generar modelos de minería de datos independientes para cada dato demográfico de los clientes, filtrando por atributos como la edad o la región.  
  
 Para más información sobre cómo copiar el contenido del modelo (como la representación gráfica o los patrones del modelo) en el Portapapeles para usarlo en otros programas, vea [Copiar una vista de un modelo de minería de datos](../../analysis-services/data-mining/copy-a-view-of-a-mining-model.md).  
  
### Para crear un modelo de minería relacionado  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en el Explorador de soluciones, haga clic en la estructura de minería de datos que contiene el modelo de minería.  
  
2.  Haga clic en la pestaña **Modelos de minería de datos** .  
  
3.  Seleccione el modelo y haga clic con el botón secundario del mouse para abrir el menú contextual.  
  
     O bien  
  
     Seleccione el modelo. En el menú **Modelo de minería de datos** , seleccione **Nuevo modelo de minería de datos**.  
  
4.  Escriba un nombre para el nuevo modelo de minería de datos y seleccione un algoritmo. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### Para modificar el filtro en el modelo de minería de datos copiado  
  
1.  Seleccione el modelo de minería de datos.  
  
2.  En la ventana **Propiedades**, haga clic en el cuadro de texto de la propiedad **Filter** y luego haga clic en el botón de generación **(…)**.  
  
3.  Cambiar las condiciones de los filtros.  
  
     Para más información sobre cómo usar los cuadros de diálogo del editor de filtros, vea [Aplicar un filtro a un modelo de minería de datos](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md).  
  
4.  En la ventana **Propiedades**, en el cuadro de texto **AlgorithmParameters**, haga clic en **Establecer parámetros de algoritmo** y cambie los parámetros del algoritmo si eso es lo que quiere.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Vea también  
 [Filtros para modelos de minería &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)   
 [Tareas y procedimientos de los modelos de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Eliminar un filtro de un modelo de minería de datos](../../analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)  
  
  