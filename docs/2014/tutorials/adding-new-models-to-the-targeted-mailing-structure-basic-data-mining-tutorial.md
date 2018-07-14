---
title: Agregar modelos nuevos a la estructura de distribución de correo directo (Tutorial de minería de datos básicos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 512c6888-60f1-46e4-9639-bc448395b8d7
caps.latest.revision: 45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: db935cec3d17815d0884b1f596e870f6d09d5086
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222615"
---
# <a name="adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>Agregar modelos nuevos a la estructura de correo de destino (tutorial básico de minería de datos)
  En esta tarea, definirá dos modelos adicionales mediante el uso de la **modelos de minería de datos** ficha del Diseñador de minería de datos. Para crear los modelos, se usarán el algoritmo Bayes naive y el algoritmo de clústeres de Microsoft. Estos dos algoritmos se han seleccionado debido a su capacidad de predecir un valor discreto (por ejemplo, la compra de una bicicleta). Para obtener más información acerca de estos algoritmos, vea [Microsoft Clustering Algorithm](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md) y [algoritmo Bayes Naive de Microsoft](../../2014/analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)  
  
### <a name="to-create-a-clustering-mining-model"></a>Para crear un modelo de minería de datos de agrupación en clústeres  
  
1.  Cambie a la **modelos de minería de datos** ficha en el Diseñador de minería de datos en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
     Tenga en cuenta que el diseñador muestra dos columnas, una para la estructura de minería de datos y otra para el `TM_Decision_Tree` modelo de minería de datos, que creó en la lección anterior.  
  
2.  Haga clic en el **estructura** columna y seleccione **nuevo modelo de minería de datos**.  
  
3.  En el **nuevo modelo de minería de datos** cuadro de diálogo **nombre del modelo**, tipo `TM_Clustering`.  
  
4.  En **nombre del algoritmo**, seleccione **Microsoft Clustering**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 El nuevo modelo aparece ahora en el **modelos de minería de datos** ficha del Diseñador de minería de datos. Este modelo, integrado con el [!INCLUDE[msCoName](../includes/msconame-md.md)] clústeres algoritmo, agrupa los clientes con características similares en clústeres y predice la compra de cada clúster de una bicicleta. Aunque puede modificar el uso de las columnas y propiedades para el nuevo modelo, sin cambios en el `TM_Clustering` modelo son necesarios para este tutorial.  
  
### <a name="to-create-a-naive-bayes-mining-model"></a>Para crear un modelo de minería de datos Bayes naive  
  
1.  En el **modelos de minería de datos** ficha del Diseñador de minería de datos,-haga clic derecho **estructura** columna y seleccione **nuevo modelo de minería de datos**.  
  
2.  En el **nuevo modelo de minería de datos** cuadro de diálogo **nombre del modelo**, tipo `TM_NaiveBayes`.  
  
3.  En **nombre del algoritmo**, seleccione **Bayes Naive de Microsoft**, a continuación, haga clic en **Aceptar**.  
  
     Aparece un mensaje que indica que el [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Bayes Naive no admite la **Age** y **Yearly Income** columnas, que son continuas.  
  
4.  Haga clic en **Sí** para confirmar el mensaje y continuar.  
  
 Un nuevo modelo aparece en el **modelos de minería de datos** ficha del Diseñador de minería de datos. Aunque puede modificar el uso de las columnas y propiedades para todos los modelos en esta no pestaña, ningún cambio en el `TM_NaiveBayes` modelo son necesarios para este tutorial.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Procesamiento de modelos en la estructura de distribución de correo directo &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Agregar modelos de minería de datos a una estructura &#40;Analysis Services - minería de datos&#41;](../../2014/analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)   
 [Diseñador de minería de datos](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Mover objetos de minería de datos](../../2014/analysis-services/data-mining/moving-data-mining-objects.md)  
  
  
