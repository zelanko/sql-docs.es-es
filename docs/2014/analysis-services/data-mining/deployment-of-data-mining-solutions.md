---
title: Implementación de soluciones de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], deploying
- deploying [Analysis Services], production environments
- deploying [Analysis Services - data mining]
- solutions [Analysis Services], deploying
- models [Analysis Services], data mining
ms.assetid: d83effc7-437d-42e9-8ac3-b65f79e27043
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 50cd0b4e2336b20ab12b8c5e6fda6615af03abd5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087645"
---
# <a name="deployment-of-data-mining-solutions"></a>Implementación de soluciones de minería de datos
  El último paso del proceso de minería de datos consiste en implementar los modelos en un entorno de producción. La implementación es importante porque hace que los modelos estén a disposición de los usuarios para que pueda realizar cualquiera de las siguientes tareas:  
  
-   Utilice los modelos para crear predicciones y tomar decisiones empresariales. Para obtener información acerca de las herramientas que puede usar para crear consultas, vea [Interfaces de consultas de minería de datos](data-mining-query-tools.md).  
  
-   Incrustar la funcionalidad de minería de datos directamente en una aplicación. Puede incluir Objetos de administración de análisis (AMO) o un ensamblado que contenga un conjunto de objetos que la aplicación pueda utilizar para crear, cambiar, procesar y eliminar estructuras y modelos de minería de datos.  
  
-   Crear informes que permiten a los usuarios solicitar predicciones, ver tendencias o comparar modelos.  
  
 En esta sección se proporciona información detallada sobre las opciones de implementación.  
  
 [Requisitos para la implementación de las soluciones de minería de datos](#bkmk_Reqs)  
  
 [Implementar una solución relacional](#bkmk_RelationalSltn)  
  
 [Implementar una solución multidimensional](#bkmk_MDSltn)  
  
 [Recursos relacionados](#bkmk_Resources)  
  
## <a name="in-this-section"></a>En esta sección  
 [Implementar soluciones de minería de datos para versiones anteriores de SQL Server](deploy-a-data-mining-solution-to-previous-versions-of-sql-server.md)  
  
 [Exportar e importar objetos de minería de datos](export-and-import-data-mining-objects.md)  
  
##  <a name="bkmk_Reqs"></a> Requisitos para la implementación de las soluciones de minería de datos  
 La instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se implementa la solución debe ejecutarse en un modo que admita objetos multidimensionales y objetos de minería de datos; es decir, no puede implementar objetos de minería de datos en una instancia que hospede modelos tabulares o datos de PowerPivot.  
  
 Por consiguiente, al crear una solución de minería de datos en Visual Studio, asegúrese de utilizar la plantilla **Proyecto multidimensional y de minería de datos de Analysis Services**.  
  
 Al implementar la solución, los objetos utilizados para la minería de datos se crean en la instancia especificada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , en una base de datos con el mismo nombre que el archivo de solución.  
  
###  <a name="bkmk_RelationalSltn"></a> Implementar una solución relacional  
 Al implementar una solución relacional de minería de datos, los objetos necesarios de minería de datos se crean dentro de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y los objetos se procesan de forma predeterminada. Puede cambiar las opciones de procesamiento con la propiedad de configuración **Opción de procesamiento**. Para más información, vea [Configurar las propiedades de un proyecto de Analysis Services &#40;SSDT&#41;](../multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
 De forma predeterminada, solo los cambios incrementales se implementan cada vez. En otras palabras, puede modificar un modelo de minería de datos y, cuando vuelva a implementar el proyecto, solo el modelo de minería de datos se actualizaría. Sin embargo, si tiene varios clientes que modifican la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , esto puede provocar errores. Para cambiar el modo de implementación predeterminado para actualizar la base de datos completa al implementar la solución, cambie la propiedad **Modo de implementación**  
  
 En una solución relacional de minería de datos, los únicos objetos que deben implementarse son la definición del origen de datos, cualquier vista del origen de datos que se usara, las estructuras de minería de datos y todos los modelos de minería de datos dependientes.  
  
###  <a name="bkmk_MDSltn"></a> Implementar una solución multidimensional  
 Al implementar una solución de minería de datos multidimensional, esta solución crea los objetos de minería de datos en la misma base de datos que el cubo de origen.  
  
 Cuando se procesa la estructura o el modelo de minería de datos, debe procesar también el cubo de origen. Por esta razón, al implementar una solución que utiliza los modelos de minería de datos OLAP puede tardarse más que en las soluciones que relacionales de minería de datos.  
  
 Los objetos de minería de datos normalmente usan los mismos orígenes de datos y vistas del origen de datos que se utilizan para el cubo. Sin embargo, puede agregar orígenes de datos y vistas del origen de datos que estén destinadas específicamente a la minería de datos. Por ejemplo, un cubo normalmente no contendría datos sobre los posibles clientes o datos externos que no se usen en los objetos multidimensionales.  
  
##  <a name="bkmk_Resources"></a> Recursos relacionados  
 [Mover objetos de minería de datos](moving-data-mining-objects.md)  
  
 Si el modelo se basa solo en datos relacionales, exportar e importar objetos mediante DMX es la forma más sencilla de mover los modelos.  
  
 [Mover una base de datos de Analysis Services](../multidimensional-models/move-an-analysis-services-database.md)  
  
 Cuando los modelos utilizan un cubo como origen de datos, consulte este tema para obtener más información sobre cómo mover los modelos y sus datos de cubo correspondientes.  
  
 [Implementar proyectos de Analysis Services &#40;SSDT&#41;](../multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
 Proporciona información general sobre la implementación de los proyectos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y describe las propiedades que puede establecer como parte de la configuración del proyecto.  
  
## <a name="see-also"></a>Vea también  
 [Procesamiento de objetos de modelo multidimensional](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Interfaces de consultas de minería de datos](data-mining-query-tools.md)   
 [Requisitos y consideraciones de procesamiento &#40;minería de datos&#41;](processing-requirements-and-considerations-data-mining.md)  
  
  
