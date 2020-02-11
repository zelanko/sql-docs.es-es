---
title: Agregar un modelo de regresión logística a la estructura del centro de llamadas (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 97abb77a-346c-44fa-8959-688dee1af6a8
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 32e66a84dea20964c11c7de0aa568530aa8c28c5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62823282"
---
# <a name="adding-a-logistic-regression-model-to-the-call-center-structure-intermediate-data-mining-tutorial"></a>Agregar un modelo de regresión logística a la estructura de centro de llamadas (Tutorial intermedio de minería de datos)
  Además de analizar los factores que pueden influir en las operaciones del centro de llamadas, se le pidió que proporcionara recomendaciones concretas sobre la manera en que el personal puede mejorar la calidad de servicio. En esta tarea usará la misma estructura de minería de datos con la que creó el modelo de exploración y agregará un modelo de minería de datos que después se usará para crear predicciones.  
  
 En [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], un modelo de regresión logística se basa en el algoritmo de redes neuronales, lo que ofrece la misma flexibilidad y eficacia que un modelo de red neuronal. Sin embargo, la regresión logística es especialmente adecuada para predecir resultados binarios.  
  
 En este escenario, usará la misma estructura de minería de datos que utilizó para el modelo de red neuronal. Sin embargo, personalizará el nuevo modelo para abordar las cuestiones empresariales. Le interesa la mejora de la calidad de servicio y determinar cuántos operadores experimentados necesita; para ello, configurará el modelo para predecir esos valores.  
  
 Para asegurarse de que todos los modelos basados en los datos del centro de llamadas se parecen lo más posible, usará el mismo valor de inicialización que antes. Al establecer el parámetro de inicialización se garantiza que el modelo procesa los datos a partir del mismo punto inicial, y se minimizan las variaciones causadas por las anomalías en los datos.  
  
### <a name="to-add-a-new-mining-model-to-the-call-center-mining-structure"></a>Para agregar un nuevo modelo de minería de datos a la estructura de minería de datos del centro de llamadas  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en explorador de soluciones, haga clic con el botón secundario en la estructura de minería de datos **Call Center Discretizan**y seleccione **abrir diseñador**.  
  
2.  En el diseñador de minería de datos, haga clic en la pestaña **modelos de minería** de datos.  
  
3.  Haga clic en **crear un modelo de minería de datos relacionado**.  
  
4.  En el cuadro de diálogo **nuevo modelo de minería de datos** , en `Call Center - LR`nombre del **modelo**, escriba.  En **nombre del algoritmo**, seleccione **regresión logística de Microsoft**.  
  
5.  Haga clic en **OK**.  
  
     El nuevo modelo de minería de datos se muestra en la pestaña **modelos de minería de datos** .  
  
### <a name="to-customize-the-logistic-regression-model"></a>Para personalizar el modelo de regresión logística  
  
1.  En la columna del nuevo modelo `Call Center - LR`de minería de datos, deje Fact callcenter ID como la clave.  
  
2.  Cambie el valor de ServiceGrade y el nivel dos operadores a **PREDICT**.  
  
     Ambas columnas se usarán como entrada y para la predicción. Básicamente, crea dos modelos independientes en los mismos datos: uno que predice el número de operadores y otro que predice la calificación del servicio.  
  
3.  Cambie todas las demás columnas a **Input**.  
  
### <a name="to-specify-the-seed-and-process-the-models"></a>Para especificar el valor de inicialización y procesar los modelos  
  
1.  En la pestaña **modelo de minería de datos** , haga clic con el botón secundario en la columna del modelo denominado Call Center-LR y seleccione **establecer parámetros de algoritmo**.  
  
2.  En la fila del parámetro HOLDOUT_SEED, haga clic en la celda vacía **** situada debajo de valor `1`y escriba. Haga clic en **OK**.  
  
    > [!NOTE]  
    >  El valor de inicialización que elija no es importante siempre y cuando use el mismo para todos los modelos relacionados.  
  
3.  En el menú **modelos de minería de datos** , seleccione **procesar estructura de minería de datos y todos los modelos**. Haga clic en **sí** para implementar el proyecto de minería de datos actualizado en el servidor.  
  
4.  En el cuadro de diálogo **procesar modelo de minería de datos** , haga clic en **Ejecutar**.  
  
5.  Haga clic en **cerrar** para cerrar el cuadro de diálogo **progreso del proceso** y, a continuación, haga clic de nuevo en **cerrar** en el cuadro de diálogo **procesar modelo de minería de datos** .  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear predicciones para los modelos del centro de llamadas &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Requisitos y consideraciones de procesamiento &#40;la minería de datos&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
