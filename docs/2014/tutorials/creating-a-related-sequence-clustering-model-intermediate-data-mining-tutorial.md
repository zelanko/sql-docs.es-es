---
title: Crear un modelo (Tutorial de minería de datos intermedios) de clúster de secuencia relacionado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1fb4f5bc-1756-45ca-9cd7-411a8c5992a9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 71db7ba5246e151bbca8a52972a2ba835b80ddb6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62855878"
---
# <a name="creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Crear un modelo de agrupación en clústeres de secuencia relacionado (tutorial intermedio de minería de datos)
  En el modelo de agrupación en clústeres de secuencia aprendió que otros atributos como Region o Income influyen considerablemente en los modelos; por tanto, para ampliar sus conocimientos sobre las secuencias, creará un modelo de agrupación en clústeres de secuencia relacionado y quitará los atributos relacionados con los datos demográficos de los clientes.  
  
 En esta tarea, creará una copia del modelo de agrupación en clústeres de secuencia de región y, a continuación, quitará del modelo todas las columnas que no estén relacionadas directamente con las secuencias.  
  
 El nuevo modelo contendrá las mismas columnas que el modelo de minería de datos en el que se basa. Sin embargo, no necesita quitar las columnas de la estructura de minería de datos; solo tendrá que especificar que el nuevo modelo de minería omitirá las columnas.  
  
### <a name="to-make-a-copy-of-the-sequence-clustering-model"></a>Para realizar una copia del modelo de agrupación en clústeres de secuencia  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en el Diseñador de minería de datos, haga clic en el **modelos de minería de datos** ficha.  
  
2.  Haga clic en el modelo que desea copiar y seleccione **nuevo modelo de minería de datos**.  
  
3.  En el **nuevo modelo de minería de datos** cuadro de diálogo, escriba un nombre de modelo y seleccione Microsoft `Sequence Clustering`.  
  
     Para este tutorial, escriba el nombre `Sequence Clustering`.  
  
4.  Haga clic en **Aceptar**.  
  
### <a name="to-remove-columns-from-the-mining-model"></a>Para quitar columnas del modelo de minería de datos  
  
1.  En el **Mining Model** ficha, en la columna para el nuevo modelo denominado agrupación en clústeres de secuencia, haga clic en la fila correspondiente a la **Income Group** de atributo y seleccione **omitir**.  
  
2.  Repita este paso para el atributo **región**.  
  
3.  Haga clic en el signo más junto al nombre de tabla, **v Assoc Seq Line Items**, para expandir la tabla y ver las columnas de la tabla anidada.  
  
     El nuevo modelo debe contener solamente las columnas siguientes:  
  
     **Orden NumberKey**  
  
     **Tecla de número de línea**  
  
     **Predicción de modelo**  
  
### <a name="to-process-the-new-sequence-clustering-model"></a>Para procesar el nuevo modelo de agrupación en clústeres de secuencia  
  
1.  En el **Mining Model** pestaña, haga clic en el nuevo modelo denominado `Sequence Clustering`y seleccione **modelo de proceso**.  
  
     Como el nuevo modelo de minería de datos simplificado se basa en una estructura que ya se ha procesado, no es necesario volver a procesar la estructura. Simplemente puede procesar el nuevo modelo de minería de datos.  
  
2.  Haga clic en **Sí** para implementar el proyecto de minería de datos actualizados en el servidor.  
  
3.  En el **modelo de minería de datos de proceso** cuadro de diálogo, haga clic en **ejecutar**.  
  
4.  Haga clic en **cerrar** para cerrar el **progreso del proceso** cuadro de diálogo y, a continuación, haga clic en **cerrar** nuevo en el **modelo de minería de datos de proceso** cuadro de diálogo.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear predicciones en una modelo de clústeres de secuencia &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Requisitos y consideraciones de procesamiento &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
