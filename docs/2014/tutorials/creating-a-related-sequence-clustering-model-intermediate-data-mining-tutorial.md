---
title: Crear un modelo de agrupación en clústeres de secuencia relacionado (tutorial intermedio de minería de datos) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62855878"
---
# <a name="creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Crear un modelo de agrupación en clústeres de secuencia relacionado (tutorial intermedio de minería de datos)
  En el modelo de agrupación en clústeres de secuencia aprendió que otros atributos como Region o Income influyen considerablemente en los modelos; por tanto, para ampliar sus conocimientos sobre las secuencias, creará un modelo de agrupación en clústeres de secuencia relacionado y quitará los atributos relacionados con los datos demográficos de los clientes.  
  
 En esta tarea, creará una copia del modelo de agrupación en clústeres de secuencia de región y, a continuación, quitará del modelo todas las columnas que no estén relacionadas directamente con las secuencias.  
  
 El nuevo modelo contendrá las mismas columnas que el modelo de minería de datos en el que se basa. Sin embargo, no necesita quitar las columnas de la estructura de minería de datos; solo tendrá que especificar que el nuevo modelo de minería omitirá las columnas.  
  
### <a name="to-make-a-copy-of-the-sequence-clustering-model"></a>Para realizar una copia del modelo de agrupación en clústeres de secuencia  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en el diseñador de minería de datos, haga clic en la pestaña **modelos de minería** de datos.  
  
2.  Haga clic con el botón secundario en el modelo que desea copiar y seleccione **nuevo modelo de minería de datos**.  
  
3.  En el cuadro de diálogo **nuevo modelo de minería de datos** , escriba un nombre de `Sequence Clustering`modelo y seleccione Microsoft.  
  
     Para este tutorial, escriba el nombre `Sequence Clustering`.  
  
4.  Haga clic en **OK**.  
  
### <a name="to-remove-columns-from-the-mining-model"></a>Para quitar columnas del modelo de minería de datos  
  
1.  En la pestaña **modelo de minería de datos** , en la columna del nuevo modelo denominado agrupación en clústeres de secuencia, haga clic en la fila del atributo de grupo de **ingresos** y seleccione **omitir**.  
  
2.  Repita este paso para la **región**de atributo.  
  
3.  Haga clic en el signo más situado junto al nombre de la tabla, **v Assoc SEQ line items**, para expandir la tabla y ver las columnas de la tabla anidada.  
  
     El nuevo modelo debe contener solamente las columnas siguientes:  
  
     **Orden NumberKey**  
  
     **Clave de número de línea**  
  
     **Predicción de modelo**  
  
### <a name="to-process-the-new-sequence-clustering-model"></a>Para procesar el nuevo modelo de agrupación en clústeres de secuencia  
  
1.  En la pestaña **modelo de minería de datos** , haga clic con el `Sequence Clustering`botón secundario en el nuevo modelo denominado y seleccione **procesar modelo**.  
  
     Como el nuevo modelo de minería de datos simplificado se basa en una estructura que ya se ha procesado, no es necesario volver a procesar la estructura. Simplemente puede procesar el nuevo modelo de minería de datos.  
  
2.  Haga clic en **sí** para implementar el proyecto de minería de datos actualizado en el servidor.  
  
3.  En el cuadro de diálogo **procesar modelo de minería de datos** , haga clic en **Ejecutar**.  
  
4.  Haga clic en **cerrar** para cerrar el cuadro de diálogo **progreso del proceso** y, a continuación, haga clic de nuevo en **cerrar** en el cuadro de diálogo **procesar modelo de minería de datos** .  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear predicciones en un modelo de agrupación en clústeres de secuencia &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Requisitos y consideraciones de procesamiento &#40;la minería de datos&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
