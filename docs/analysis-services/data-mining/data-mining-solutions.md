---
title: "Soluciones de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], about data mining
- data mining [Analysis Services], development
ms.assetid: 84f6548d-ebb0-4e10-9b29-66253fa0a04a
caps.latest.revision: "64"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 595282e28a55171ed5a528d28f37500a21f71c0d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="data-mining-solutions"></a>Soluciones de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Una solución de minería de datos es un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solución que contiene uno o varios proyectos de minería de datos.  
  
 En los temas de esta sección se ofrece información acerca del diseño y la implementación de una solución de minería de datos integrada mediante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obtener información general acerca del proceso de diseño de minería de datos y de las herramientas relacionadas, vea [Data Mining Concepts](../../analysis-services/data-mining/data-mining-concepts.md).  
  
 Para más información sobre los tipos adicionales de proyecto que son útiles para la minería de datos, vea [Proyectos relacionados en las soluciones de minería de datos](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md).  
  
 [Soluciones relacionales y. Soluciones multidimensionales](#bkmk_RelMD)  
  
 [Implementar soluciones de minería de datos](#bkmk_Deploy)  
  
 [Tutoriales de la solución](#bkmk_Walkthru)  
  
##  <a name="bkmk_RelMD"></a>Soluciones relacionales y. multidimensionales  
 Una solución de minería de datos se puede basar en datos multidimensionales, es decir, en un cubo existente; o en datos puramente relacionales, como las tablas y las vistas de un almacenamiento de datos; o bien en archivos de texto, libros de Excel u otros orígenes de datos externos.  
  
-   Puede crear objetos de minería de datos en una solución de base de datos multidimensional existente.  
  
     Normalmente, se crearía una solución como esta si ya ha creado un cubo y desearía realizar la minería de datos utilizando el cubo como origen de datos. Al mover y crear copias de seguridad de modelos basados en un cubo, el cubo también debe moverse o copiarse.  
  
-   Puede crear una solución de minería de datos que solo contenga objetos de minería de datos, incluidos los orígenes de datos y vistas del origen de datos que admiten, y que use un origen de datos relacional solamente.  
  
     Este es el método preferido para crear modelos de minería de datos, dado que el procesamiento y la consulta normalmente es más rápido en orígenes de datos relacionales. También puede mover y hacer copia de seguridad fácilmente de los modelos entre servidores copiando los comandos EXPORT e IMPORT.  
  
##  <a name="bkmk_Deploy"></a> Implementar soluciones de minería de datos  
 La instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se implementa la solución debe ejecutarse en un modo que admita objetos multidimensionales y objetos de minería de datos; es decir, no puede implementar objetos de minería de datos en una instancia que hospede modelos tabulares o datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Por consiguiente, al crear una solución de minería de datos en Visual Studio, asegúrese de utilizar la plantilla **Proyecto multidimensional y de minería de datos de Analysis Services**.  
  
 Al implementar la solución, los objetos utilizados para la minería de datos se crean en la instancia especificada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , en una base de datos con el mismo nombre que el archivo de solución.  
  
 Para más información sobre cómo implementar tanto soluciones multidimensionales como relacionales, vea [Implementación de soluciones de minería de datos](../../analysis-services/data-mining/deployment-of-data-mining-solutions.md).  
  
##  <a name="bkmk_Walkthru"></a> Tutorial de la solución  
 Proporciona información general sobre cómo crear soluciones de minería de datos mediante el Asistente para minería de datos.  
  
 [Crear una estructura de minería de datos relacional](../../analysis-services/data-mining/create-a-relational-mining-structure.md)  
 Crear una estructura de minería de datos relacionales, archivos de texto y otros orígenes que se pueden combinar en una vista del origen de datos.  
  
 [Crear una estructura de minería de datos OLAP](../../analysis-services/data-mining/create-an-olap-mining-structure.md)  
 Crear una estructura de minería de datos basada en los datos de un cubo OLAP. Los modelos que se crean a partir de datos OLAP se pueden guardar como una dimensión de minería de datos, o puede guardar el conjunto de datos y sus modelos como un cubo nuevo.  
  
## <a name="in-this-section"></a>En esta sección  
 [Proyectos de minería de datos](../../analysis-services/data-mining/data-mining-projects.md)  
  
 [Procesar objetos de minería de datos](../../analysis-services/data-mining/processing-data-mining-objects.md)  
  
 [Proyectos relacionados en las soluciones de minería de datos](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md)  
  
 [Implementación de soluciones de minería de datos](../../analysis-services/data-mining/deployment-of-data-mining-solutions.md)  
  
## <a name="related-tasks-and-topics"></a>Temas y tareas relacionados  
 Después de crear una solución básica de minería de datos, incluidos los orígenes de datos y su estructura de minería de datos, puede generar la solución agregando nuevos modelos,probando y comparando modelos, creando predicciones, y experimentando con subconjuntos de datos.  
  
 Para obtener más información, vea los siguientes vínculos:  
  
|Tareas|Temas|  
|-----------|------------|  
|Pruebe los modelos que cree, valide la calidad de los datos de entrenamiento y cree gráficos que representen la precisión de los modelos de minería de datos.|[Prueba y validación &#40;minería de datos&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)|  
|Entrene el modelo rellenando la estructura y los modelos relacionados con datos. Actualice y amplía los modelos con nuevos datos.|[Procesar objetos de minería de datos](../../analysis-services/data-mining/processing-data-mining-objects.md)|  
|Personalice un modelo de minería de datos aplicando filtros a los datos de entrenamiento, eligiendo un algoritmo diferente o estableciendo parámetros avanzados para el algoritmo.|[Personalizar la estructura y los modelos de minería de datos](../../analysis-services/data-mining/customize-mining-models-and-structure.md)|  
|Personalice un modelo de minería de datos aplicando filtros a los datos usados en el entrenamiento del modelo.|[Agregar modelos de minería de datos a una estructura &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)|  
|Actualice y administre las soluciones de minería de datos.|Vínculo TBD|  
  
## <a name="see-also"></a>Ver también  
 [Tutoriales de minería de datos &#40;Analysis Services&#41;](../../analysis-services/data-mining-tutorials-analysis-services.md)  
  
  
