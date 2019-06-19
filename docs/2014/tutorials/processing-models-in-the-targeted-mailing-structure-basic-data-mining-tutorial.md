---
title: Procesamiento de modelos en la estructura de distribución de correo directo (Tutorial de minería de datos básicos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9d8233bb-117e-4563-9302-8a5a8ad1fae2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 605088d405cbd2dcfba92a2da5fa4e07c38d8f0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188231"
---
# <a name="processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>Procesar los modelos de la estructura de distribución de correo directo (Tutorial básico de minería de datos)
  Para poder examinar o trabajar con los modelos de minería de datos que ha creado, se debe implementar el proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y procesar la estructura y los modelos de minería de datos.  
  
-   *Implementar* envía el proyecto a un servidor y crea los objetos en el proyecto en el servidor.  
  
-   *Procesamiento* rellena [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] objetos con datos procedentes de orígenes de datos relacionales.  
  
 Los modelos no se pueden utilizar hasta que se hayan implementado y procesado. Además, cuando se realiza cualquier cambio en el modelo, como agregar datos nuevos, se debe volver a implementar y procesar los modelos.  
  
## <a name="ensuring-consistency-with-holdoutseed"></a>Asegurarse de la coherencia con HoldoutSeed  
 Al implementar un proyecto y procesar la estructura y los modelos, a las filas individuales de la estructura de datos se les asigna el conjunto de entrenamiento o el conjunto de pruebas según un valor de inicialización numérico. De forma predeterminada, el valor de inicialización numérico se calcula en función de los atributos de la estructura de datos. Sin embargo, si alguna vez cambia algunos aspectos del modelo, el valor de inicialización cambiaría, lo que produciría resultados ligeramente diferentes. Por lo tanto, para asegurarse de que los resultados son los mismos que se describe aquí, asignaremos arbitrariamente un fijo *inicialización de exclusión* de `12`. El valor de inicialización de exclusión se utiliza para inicializar el algoritmo de muestreo y garantiza que los datos se reparten aproximadamente de la misma manera para todas las estructuras de minería de datos y sus modelos.  
  
 Este valor no afecta al número de casos del conjunto de entrenamiento; simplemente garantiza que se usará el mismo método de partición siempre que se genere el modelo.  
  
 Para obtener más información sobre el valor de inicialización de exclusión, vea [conjuntos de datos de prueba y entrenamiento](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md).  
  
#### <a name="to-set-the-holdout-seed"></a>Para establecer el valor de inicialización de exclusión  
  
1.  Haga clic en el **Mining Structure** ficha o el **modelos de minería de datos** ficha en el Diseñador de minería de datos en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
     **Destino correo MiningStructure** se muestra en el **propiedades** panel.  
  
2.  Asegúrese de que el **propiedades** panel está abierto presionando **F4**.  
  
3.  Asegúrese de que **CacheMode** está establecido en **KeepTrainingCases**.  
  
4.  Escriba `12` para **HoldoutSeed**.  
  
## <a name="deploying-and-processing-the-models"></a>Implementar y procesar los modelos  
 En el Diseñador de minería de datos, puede decidir qué objetos procesar, según el ámbito de los cambios realizados en el modelo o los datos subyacentes:  
  
 En esta tarea, puesto que los datos y los modelos son nuevos, procesará la estructura y todos los modelos al mismo tiempo.  
  
#### <a name="to-deploy-the-project-and-process-all-the-mining-models"></a>Para implementar el proyecto y procesar todos los modelos de minería de datos  
  
1.  En el **Mining Model** menú, seleccione **procesar estructura de minería de datos y todos los modelos**.  
  
     Si ha realizado cambios en la estructura, se le pedirá que genere e implemente el proyecto antes de procesar los modelos. Haga clic en **Sí**.  
  
2.  Haga clic en **ejecutar** en el **procesamiento Mining Structure - Targeted Mailing** cuadro de diálogo.  
  
     Se abre el cuadro de diálogo **Progreso del proceso** para mostrar los detalles del procesamiento del modelo. El procesamiento del modelo podría tardar algún tiempo, según el equipo.  
  
3.  Haga clic en **Cerrar** en el cuadro de diálogo **Progreso del proceso** cuando el procesamiento de los modelos se haya completado.  
  
4.  Haga clic en **cerrar** en el **procesando estructura de minería de datos - \<estructura >** cuadro de diálogo.  
  
## <a name="previous-task-in-lesson"></a>Tarea anterior de la lección  
 [Agregar modelos nuevos a la estructura de distribución de correo directo &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 4: Explorar los modelos de distribución de correo directo &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Requisitos y consideraciones de procesamiento &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
