---
title: Agregar nuevos modelos a la estructura de distribución de correo directo (tutorial básico de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 512c6888-60f1-46e4-9639-bc448395b8d7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 285ee82110ffdef521d75fb43343f4889663e981
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62822650"
---
# <a name="adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>Agregar modelos nuevos a la estructura de correo de destino (tutorial básico de minería de datos)
  En esta tarea, definirá dos modelos adicionales mediante la pestaña **modelos de minería** de datos del diseñador de minería de datos. Para crear los modelos, se usarán el algoritmo Bayes naive y el algoritmo de clústeres de Microsoft. Estos dos algoritmos se han seleccionado debido a su capacidad de predecir un valor discreto (por ejemplo, la compra de una bicicleta). Para obtener más información sobre estos algoritmos, vea [algoritmo de clústeres de Microsoft](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md) y [algoritmo Bayes Naive de Microsoft](../../2014/analysis-services/data-mining/microsoft-naive-bayes-algorithm.md) .  
  
### <a name="to-create-a-clustering-mining-model"></a>Para crear un modelo de minería de datos de agrupación en clústeres  
  
1.  Cambie a la pestaña **modelos de minería** de datos del diseñador [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]de minería de datos en.  
  
     Observe que el diseñador muestra dos columnas, una para la estructura de minería de datos y `TM_Decision_Tree` otra para el modelo de minería de datos, que creó en la lección anterior.  
  
2.  Haga clic con el botón secundario en la columna **estructura** y seleccione **nuevo modelo de minería de datos**.  
  
3.  En el cuadro de diálogo **nuevo modelo de minería de datos** , en `TM_Clustering`nombre del **modelo**, escriba.  
  
4.  En **nombre del algoritmo**, seleccione **agrupación en clústeres de Microsoft**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 El nuevo modelo aparece ahora en la pestaña **modelos de minería** de datos del diseñador de minería de datos. Este modelo, creado con el [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de clústeres, agrupa a los clientes con características similares en los clústeres y predice la compra de bicicletas para cada clúster. Aunque puede modificar el uso de las columnas y las propiedades del nuevo modelo, no es necesario `TM_Clustering` realizar ningún cambio en el modelo para este tutorial.  
  
### <a name="to-create-a-naive-bayes-mining-model"></a>Para crear un modelo de minería de datos Bayes naive  
  
1.  En la pestaña **modelos de minería** de datos del diseñador de minería de datos, haga clic con el botón derecho en la columna de **estructura** Clickthe y seleccione **nuevo modelo de minería**de datos.  
  
2.  En el cuadro de diálogo **nuevo modelo de minería de datos** , en `TM_NaiveBayes`nombre del **modelo**, escriba.  
  
3.  En **nombre del algoritmo**, seleccione **Bayes Naive de Microsoft**y, a continuación, haga clic en **Aceptar**.  
  
     Aparece un mensaje que indica que el [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Bayes Naive de no admite las columnas **Age** y **yearly Income** , que son continuas.  
  
4.  Haga clic en **sí** para confirmar el mensaje y continuar.  
  
 Aparece un nuevo modelo en la pestaña **modelos de minería** de datos del diseñador de minería de datos. Aunque puede modificar el uso de las columnas y las propiedades de todos los modelos de esta pestaña, no es `TM_NaiveBayes` necesario realizar ningún cambio en el modelo para este tutorial.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Procesar modelos en la estructura de distribución de correo directo &#40;tutorial básico de minería de datos&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Agregar modelos de minería de datos a una estructura &#40;&#41;de minería de datos Analysis Services](../../2014/analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)   
 [Diseñador de minería de datos](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Mover objetos de minería de datos](../../2014/analysis-services/data-mining/moving-data-mining-objects.md)  
  
  
