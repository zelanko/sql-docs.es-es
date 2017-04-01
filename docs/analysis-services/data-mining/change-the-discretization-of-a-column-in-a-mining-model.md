---
title: "Cambiar la discretizaci&#243;n de una columna en un modelo de miner&#237;a de datos | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "discretización [Analysis Services]"
  - "estructuras de minería [Analysis Services], temas de procedimientos"
  - "columnas de datos discretos [minería de datos]"
  - "problemas de creación de depósitos [Analysis Services]"
ms.assetid: 3c49862b-595d-4fa4-b890-e2e1bde1d74f
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 14
---
# Cambiar la discretizaci&#243;n de una columna en un modelo de miner&#237;a de datos
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] discretiza valores automáticamente, es decir, agrupa los datos de las columnas numéricas, en determinadas situaciones. Por ejemplo, si la información contiene datos numéricos continuos y crea un modelo de árbol de decisión, cada columna de datos continuos se discretizará automáticamente según la distribución de los datos. Si desea controlar cómo se discretizan los datos, debe cambiar las propiedades en la columna de la estructura de minería de datos que controlan cómo se usan los datos en el modelo.  
  
 Para más información general sobre cómo configurar las propiedades de un modelo de minería de datos, vea [Columnas del modelo de minería de datos](../../analysis-services/data-mining/mining-model-columns.md).  
  
### Para mostrar las propiedades de una columna de un modelo de minería de datos  
  
1.  En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos, haga clic con el botón derecho en el encabezado de columna que contiene el nombre del modelo de minería de datos o en la fila de la cuadrícula que contiene el nombre del algoritmo de minería de datos y luego seleccione **Propiedades**.  
  
     La ventana **Propiedades** muestra las propiedades que están asociadas al modelo de minería de datos en conjunto.  
  
2.  En la columna **Estructura** situada cerca del lado izquierdo de la pantalla, haga clic en la columna que contiene los datos numéricos continuos que desea discretizar.  
  
     La ventana **Propiedades** cambia para mostrar simplemente las propiedades asociadas a esa columna.  
  
### Para cambiar el método de discretización  
  
1.  En la ventana **Propiedades de minería de datos** , haga clic en el cuadro de texto situado junto a **Contenido** y seleccione **Discretized** en la lista desplegable.  
  
     Las propiedades <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> y <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> ya están habilitadas.  
  
2.  En la ventana **Propiedades**, haga clic en el cuadro de texto situado al lado de <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> y seleccione uno de los valores siguientes: **Automatic**, **EqualAreas** o **Cluster**.  
  
    > [!NOTE]  
    >  Si el uso de la columna está establecido en **Ignore**, la ventana **Propiedades** para la columna estará en blanco.  
  
     El nuevo valor tendrá efecto cuando se seleccione otro elemento diferente en el diseñador.  
  
3.  En la ventana **Propiedades**, haga clic en el cuadro de texto situado al lado de <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> y escriba un valor numérico.  
  
    > [!NOTE]  
    >  Si cambia estas propiedades, se debe volver a procesar la estructura, junto con cualquier modelo que desee que use el nuevo valor.  
  
## Vea también  
 [Tareas y procedimientos de los modelos de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  