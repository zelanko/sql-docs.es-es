---
title: Requisitos y consideraciones de procesamiento (minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], objects
- mining structures [Analysis Services], processing
- mining models [Analysis Services], processing
ms.assetid: f7331261-6f1c-4986-b2c7-740f4b92ca44
author: minewiskan
ms.author: owend
ms.openlocfilehash: 3f0a1dcf4793244a17bb52b38894bba2cb06d219
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84520904"
---
# <a name="processing-requirements-and-considerations-data-mining"></a>Requisitos y consideraciones de procesamiento (minería de datos)
  En este tema se describen algunas consideraciones técnicas que debe tener en cuenta al procesar objetos de minería de datos. Para obtener una explicación general de qué es el procesamiento y cómo se aplica a la minería de datos, vea [Procesar objetos de minería de datos](processing-data-mining-objects.md).  
  
 [Consultas en el almacén relacional](#bkmk_QueryReqs)  
  
 [Procesar estructuras de minería de datos](#bkmk_ProcessStructures)  
  
 [Procesar modelos de minería de datos](#bkmk_ProcessModels)  
  
##  <a name="queries-on-the-relational-store-during-processing"></a><a name="bkmk_QueryReqs"></a> Consultas en el almacén relacional durante el procesamiento  
 En la minería de datos, hay tres fases para el procesamiento: consultar los datos de origen, determinar las estadísticas sin tratar y usar la definición del modelo y el algoritmo para entrenar el modelo de minería de datos.  
  
 El servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] emite consultas a la base de datos que proporciona los datos sin procesar. Esta base de datos puede ser una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o una versión anterior del motor de base de datos de SQL Server. Cuando se procesa una estructura de minería de datos, los datos del origen se transfieren a la estructura de minería de datos y se conservan en el disco en un nuevo formato comprimido. No se procesan todas las columnas del origen de datos sino únicamente aquellas que están incluidas en la estructura de minería de datos, de acuerdo con la definición de los enlaces.  
  
 Con estos datos, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera un índice de todos los datos y columnas de datos discretos, y crea un índice independiente para las columnas continuas. Se emite una consulta por cada tabla anidada para crear el índice y se genera una consulta adicional por cada tabla anidada para procesar las relaciones entre cada par de una tabla anidada y tabla de casos. La razón de crear varias consultas es procesar un almacén interno especial de datos multidimensionales. Puede limitar el número de consultas que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] envía al almacén relacional estableciendo la propiedad del servidor, `DatabaseConnectionPoolMax`. Para más información, consulte [OLAP Properties](../server-properties/olap-properties.md).  
  
 Al procesar el modelo, éste no vuelve a leer directamente los datos del origen de datos, sino que recibe el resumen de los datos de la estructura de minería de datos. Utilizando el cubo que se creó, junto con el índice y los datos del caso almacenados en memoria caché, el servidor crea subprocesos independientes para entrenar los modelos.  
  
 Para obtener más información sobre las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que admiten el procesamiento de modelos en paralelo, vea [características compatibles con las ediciones de SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473) ( https://go.microsoft.com/fwlink/?linkid=232473) .  
  
##  <a name="processing-mining-structures"></a><a name="bkmk_ProcessStructures"></a> Procesar estructuras de minería de datos  
 Una estructura de minería de datos se puede procesar con todos los modelos dependientes, o por separado. Procesar una estructura de minería de datos independientemente de los modelos puede ser útil cuando se prevé que el procesamiento de algunos modelos llevará mucho tiempo y se desee diferir esa operación.  
  
 Para más información, consulte [Process a Mining Structure](process-a-mining-structure.md).  
  
 Si le preocupa el ahorro de espacio en el disco duro, tenga en cuenta que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] conserva localmente las memorias cachés de las estructuras de minería de datos. Es decir, escribe todos los datos de entrenamiento en el disco duro local. Si no desea almacenar en caché los datos, puede cambiar la opción predeterminada estableciendo la propiedad <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> de la estructura de minería de datos en `ClearAfterProcessing`. Esto eliminará la caché una vez procesados los modelos; sin embargo, también deshabilitará la obtención de detalles en la estructura de minería de datos. Para obtener más información, vea [Consultas de obtención de detalles &#40;minería de datos&#41;](drillthrough-queries-data-mining.md).  
  
 Por otra parte, si borra la caché, no podrá utilizar el conjunto de pruebas de exclusión, si definió uno, y se perderá la definición de la partición del conjunto de pruebas. Para más información sobre los conjuntos de pruebas de exclusión, vea [Conjuntos de datos de entrenamiento y de prueba](training-and-testing-data-sets.md).  
  
##  <a name="processing-mining-models"></a><a name="bkmk_ProcessModels"></a> Procesar modelos de minería de datos  
 Puede procesar un modelo de minería de datos independientemente de su estructura de minería de datos asociados, o puede procesar todos los modelos basados en la estructura, junto con la estructura.  
  
 Para más información, vea [Procesar un modelo de minería de datos](process-a-mining-model.md).  
  
 Sin embargo, en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no puede realizar una selección múltiple de modelos de minería de datos para procesar con la estructura. Si necesita controlar cómo se procesan los modelos, deberá seleccionarlos individualmente, o usar XMLA o DMX para procesarlos en serie.  
  
## <a name="when-reprocessing-is-required"></a>Cuándo es necesario un nuevo procesamiento  
 Debe procesar los modelos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que ha definido antes de empezar a trabajar con ellos. También debe volver a procesar los modelos de minería de datos siempre que cambie la estructura del modelo de minería de datos, actualice los datos de aprendizaje, cambie el modelo de minería de datos existente o agregue un nuevo modelo de minería de datos a la estructura.  
  
 Los modelos de minería de datos también se procesan en estos casos:  
  
 **Implementación de un proyecto**: dependiendo de la configuración del proyecto y de su estado actual, los modelos de minería de datos del proyecto normalmente se procesan por completo cuando se implementa el proyecto.  
  
 Cuando se inicia la implementación, el procesamiento se inicia automáticamente, a menos que haya una versión procesada anteriormente en el servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y que no se hayan producido cambios estructurales. Puede implementar un proyecto seleccionando **Implementar solución** en la lista desplegable o presionando la tecla F5. Puede  
  
 Para más información sobre cómo establecer las propiedades de implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que controlan cómo se implementan los modelos de minería de datos, vea [Implementación de soluciones de minería de datos](deployment-of-data-mining-solutions.md).  
  
 **Mover un modelo de minería de datos**: al mover un modelo de minería de datos usando el comando EXPORT, solo se exportará la definición del modelo, lo que incluye el nombre de la estructura de minería de datos que se espera que proporcione datos al modelo.  
  
 Requisitos de nuevo procesamiento en los siguientes escenarios con los comandos EXPORT e IMPORT:  
  
-   La estructura de minería de datos existe en la instancia de destino y la estructura de minería de datos está en un estado sin procesar.  
  
     La estructura y el modelo se deben volver a procesar.  
  
-   La estructura de minería de datos existe en la instancia de destino y se ha procesado la estructura de minería de datos. Solo el modelo de minería de datos se ha exportado.  
  
     El modelo se puede utilizar sin procesar.  
  
-   La definición de la estructura de minería de datos también se exportó utilizando la palabra clave WITH DEENDENCIES.  
  
     La estructura y el modelo se deben volver a procesar.  
  
 Para más información, vea [Exportar e importar objetos de minería de datos](export-and-import-data-mining-objects.md).  
  
## <a name="see-also"></a>Consulte también  
 [Estructuras de minería de datos &#40;Analysis Services:&#41;de minería de datos](mining-structures-analysis-services-data-mining.md)   
 [Estructuras de minería de datos &#40;Analysis Services:&#41;de minería de datos](mining-structures-analysis-services-data-mining.md)   
 [Procesamiento de objetos del modelo multidimensional](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
