---
title: Cambiar la discretización de una columna en un modelo de minería de datos | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 81b1d0708b8e55ebbfdd06ccb740ca8434a2a837
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="change-the-discretization-of-a-column-in-a-mining-model"></a>Cambiar la discretización de una columna en un modelo de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] discretiza valores automáticamente, es decir, agrupa los datos de las columnas numéricas, en determinadas situaciones. Por ejemplo, si la información contiene datos numéricos continuos y crea un modelo de árbol de decisión, cada columna de datos continuos se discretizará automáticamente según la distribución de los datos. Si desea controlar cómo se discretizan los datos, debe cambiar las propiedades en la columna de la estructura de minería de datos que controlan cómo se usan los datos en el modelo.  
  
 Para más información general sobre cómo configurar las propiedades de un modelo de minería de datos, vea [Columnas del modelo de minería de datos](../../analysis-services/data-mining/mining-model-columns.md).  
  
### <a name="to-display-the-properties-for-a-mining-model-column"></a>Para mostrar las propiedades de una columna de un modelo de minería de datos  
  
1.  En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos, haga clic con el botón derecho en el encabezado de columna que contiene el nombre del modelo de minería de datos o en la fila de la cuadrícula que contiene el nombre del algoritmo de minería de datos y luego seleccione **Propiedades**.  
  
     La ventana **Propiedades** muestra las propiedades que están asociadas al modelo de minería de datos en conjunto.  
  
2.  En la columna **Estructura** situada cerca del lado izquierdo de la pantalla, haga clic en la columna que contiene los datos numéricos continuos que desea discretizar.  
  
     La ventana **Propiedades** cambia para mostrar simplemente las propiedades asociadas a esa columna.  
  
### <a name="to-change-the-discretization-method"></a>Para cambiar el método de discretización  
  
1.  En la ventana **Propiedades de minería de datos** , haga clic en el cuadro de texto situado junto a **Contenido**y seleccione **Discretized** en la lista desplegable.  
  
     La ventana <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> y <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> ya están habilitadas.  
  
2.  En la pestaña **Propiedades** , haga clic en el cuadro de texto situado junto a <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> y seleccione uno de los valores siguientes: **Automatic**, **EqualAreas**o **Cluster**.  
  
    > [!NOTE]  
    >  Si el uso de la columna está establecido en **Ignore**, la ventana **Propiedades** para la columna estará en blanco.  
  
     El nuevo valor tendrá efecto cuando se seleccione otro elemento diferente en el diseñador.  
  
3.  En la pestaña **Propiedades** , haga clic en el cuadro de texto situado junto a <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> y escriba un valor numérico.  
  
    > [!NOTE]  
    >  Si cambia estas propiedades, se debe volver a procesar la estructura, junto con cualquier modelo que desee que use el nuevo valor.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y tareas de modelo de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
