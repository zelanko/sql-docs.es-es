---
title: Soluciones de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], about data mining
- data mining [Analysis Services], development
ms.assetid: 84f6548d-ebb0-4e10-9b29-66253fa0a04a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 50e6eeb4c2f2a8ba5b1ce6430111586e6e3b8207
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722701"
---
# <a name="data-mining-solutions"></a>Soluciones de minería de datos
  Una solución de minería de datos es una solución de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contiene uno o más proyectos de minería de datos.  
  
 En los temas de esta sección se ofrece información acerca del diseño y la implementación de una solución de minería de datos integrada mediante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obtener información general acerca del proceso de diseño de minería de datos y de las herramientas relacionadas, vea [Data Mining Concepts](data-mining-concepts.md).  
  
 Para más información sobre los tipos adicionales de proyecto que son útiles para la minería de datos, vea [Proyectos relacionados en las soluciones de minería de datos](data-mining-solutions.md).  
  
 [Soluciones relacionales y. Soluciones multidimensionales](#bkmk_RelMD)  
  
 [Implementar soluciones de minería de datos](#bkmk_Deploy)  
  
 [Tutoriales de la solución](#bkmk_Walkthru)  
  
##  <a name="bkmk_RelMD"></a> Soluciones relacionales y. multidimensionales  
 Puede ser una solución de minería de datos basado en datos multidimensionales: es decir, un cubo existente- o en datos puramente relacionales, como las tablas y vistas en un almacén de datos o en archivos de texto, libros de Excel u otros orígenes de datos externos.  
  
-   Puede crear objetos de minería de datos en una solución de base de datos multidimensional existente.  
  
     Normalmente, se crearía una solución como esta si ya ha creado un cubo y desearía realizar la minería de datos utilizando el cubo como origen de datos. Al mover y crear copias de seguridad de modelos basados en un cubo, el cubo también debe moverse o copiarse.  
  
-   Puede crear una solución de minería de datos que solo contenga objetos de minería de datos, incluidos los orígenes de datos y vistas del origen de datos que admiten, y que use un origen de datos relacional solamente.  
  
     Este es el método preferido para crear modelos de minería de datos, dado que el procesamiento y la consulta normalmente es más rápido en orígenes de datos relacionales. También puede mover y hacer copia de seguridad fácilmente de los modelos entre servidores copiando los comandos EXPORT e IMPORT.  
  
##  <a name="bkmk_Deploy"></a> Implementar soluciones de minería de datos  
 La instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se implementa la solución debe ejecutarse en un modo que admita objetos multidimensionales y objetos de minería de datos; es decir, no puede implementar objetos de minería de datos en una instancia que hospede modelos tabulares o datos de PowerPivot.  
  
 Por consiguiente, al crear una solución de minería de datos en Visual Studio, asegúrese de utilizar la plantilla **Proyecto multidimensional y de minería de datos de Analysis Services**.  
  
 Al implementar la solución, los objetos utilizados para la minería de datos se crean en la instancia especificada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , en una base de datos con el mismo nombre que el archivo de solución.  
  
 Para más información sobre cómo implementar tanto soluciones multidimensionales como relacionales, vea [Implementación de soluciones de minería de datos](deployment-of-data-mining-solutions.md).  
  
##  <a name="bkmk_Walkthru"></a> Tutorial de la solución  
 Proporciona información general sobre cómo crear soluciones de minería de datos mediante el Asistente para minería de datos.  
  
 [Crear una estructura de minería de datos relacional](create-a-relational-mining-structure.md)  
 Crear una estructura de minería de datos relacionales, archivos de texto y otros orígenes que se pueden combinar en una vista del origen de datos.  
  
 [Crear una estructura de minería de datos OLAP](create-an-olap-mining-structure.md)  
 Crear una estructura de minería de datos basada en los datos de un cubo OLAP. Los modelos que se crean a partir de datos OLAP se pueden guardar como una dimensión de minería de datos, o puede guardar el conjunto de datos y sus modelos como un cubo nuevo.  
  
## <a name="in-this-section"></a>En esta sección  
 [Proyectos de minería de datos](data-mining-projects.md)  
  
 [Procesar objetos de minería de datos](processing-data-mining-objects.md)  
  
 [Proyectos relacionados en las soluciones de minería de datos](data-mining-solutions.md)  
  
 [Implementación de soluciones de minería de datos](deployment-of-data-mining-solutions.md)  
  
## <a name="related-tasks-and-topics"></a>Temas y tareas relacionados  
 Después de crear una solución básica de minería de datos, incluidos los orígenes de datos y su estructura de minería de datos, puede generar la solución agregando nuevos modelos,probando y comparando modelos, creando predicciones, y experimentando con subconjuntos de datos.  
  
 Para obtener más información, vea los siguientes vínculos:  
  
|Tareas|Temas|  
|-----------|------------|  
|Pruebe los modelos que cree, valide la calidad de los datos de entrenamiento y cree gráficos que representen la precisión de los modelos de minería de datos.|[Prueba y validación &#40;minería de datos&#41;](testing-and-validation-data-mining.md)|  
|Entrene el modelo rellenando la estructura y los modelos relacionados con datos. Actualice y amplía los modelos con nuevos datos.|[Procesar objetos de minería de datos](processing-data-mining-objects.md)|  
|Personalice un modelo de minería de datos aplicando filtros a los datos de entrenamiento, eligiendo un algoritmo diferente o estableciendo parámetros avanzados para el algoritmo.|[Personalizar la estructura y los modelos de minería de datos](customize-mining-models-and-structure.md)|  
|Personalice un modelo de minería de datos aplicando filtros a los datos usados en el entrenamiento del modelo.|[Agregar modelos de minería de datos a una estructura &#40;Analysis Services - Minería de datos&#41;](add-mining-models-to-a-structure-analysis-services-data-mining.md)|  
|Actualice y administre las soluciones de minería de datos.|Vínculo TBD|  
  
## <a name="see-also"></a>Vea también  
 [Tutoriales de minería de datos &#40;Analysis Services&#41;](../data-mining-tutorials-analysis-services.md)  
  
  
