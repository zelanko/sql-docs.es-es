---
title: Cambiar la discretización de una columna en un modelo de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- discretization [Analysis Services]
- mining structures [Analysis Services], how-to topics
- discretized columns [data mining]
- bucketing problems [Analysis Services]
ms.assetid: 3c49862b-595d-4fa4-b890-e2e1bde1d74f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d2296eadc16d5ca1745fe940d1f5e7582ef30db6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085894"
---
# <a name="change-the-discretization-of-a-column-in-a-mining-model"></a>Cambiar la discretización de una columna en un modelo de minería de datos
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] discretiza valores automáticamente: es decir, agrupa los datos de numérico columna en determinados escenarios. Por ejemplo, si la información contiene datos numéricos continuos y crea un modelo de árbol de decisión, cada columna de datos continuos se discretizará automáticamente según la distribución de los datos. Si desea controlar cómo se discretizan los datos, debe cambiar las propiedades en la columna de la estructura de minería de datos que controlan cómo se usan los datos en el modelo.  
  
 Para más información general sobre cómo configurar las propiedades de un modelo de minería de datos, vea [Columnas del modelo de minería de datos](mining-model-columns.md).  
  
### <a name="to-display-the-properties-for-a-mining-model-column"></a>Para mostrar las propiedades de una columna de un modelo de minería de datos  
  
1.  En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos, haga clic con el botón derecho en el encabezado de columna que contiene el nombre del modelo de minería de datos o en la fila de la cuadrícula que contiene el nombre del algoritmo de minería de datos y luego seleccione **Propiedades**.  
  
     La ventana **Propiedades** muestra las propiedades que están asociadas al modelo de minería de datos en conjunto.  
  
2.  En la columna **Estructura** situada cerca del lado izquierdo de la pantalla, haga clic en la columna que contiene los datos numéricos continuos que desea discretizar.  
  
     La ventana **Propiedades** cambia para mostrar simplemente las propiedades asociadas a esa columna.  
  
### <a name="to-change-the-discretization-method"></a>Para cambiar el método de discretización  
  
1.  En el **propiedades de minería de datos** ventana, haga clic en el cuadro de texto situado junto a **contenido**y seleccione `Discretized` en la lista desplegable.  
  
     La ventana <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> y <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> ya están habilitadas.  
  
2.  En el **propiedades** ventana, haga clic en el cuadro de texto situado junto a <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> y seleccione uno de los siguientes valores: `Automatic`, `EqualAreas`, o `Cluster`.  
  
    > [!NOTE]  
    >  Si el uso de la columna se establece en `Ignore`, **propiedades** ventana para la columna está en blanco.  
  
     El nuevo valor tendrá efecto cuando se seleccione otro elemento diferente en el diseñador.  
  
3.  En la pestaña **Propiedades** , haga clic en el cuadro de texto situado junto a <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> y escriba un valor numérico.  
  
    > [!NOTE]  
    >  Si cambia estas propiedades, se debe volver a procesar la estructura, junto con cualquier modelo que desee que use el nuevo valor.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de los modelos de minería de datos](mining-model-tasks-and-how-tos.md)  
  
  
