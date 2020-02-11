---
title: Administración de objetos y soluciones de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], managing
- managing mining models
ms.assetid: 06fc61dd-925c-4347-8677-7046ee5d2f6f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 15574819cf0f0fec0d95fa2353c187cc55091e56
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084202"
---
# <a name="management-of-data-mining-solutions-and-objects"></a>Administración de las soluciones y los objetos de minería de datos
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]proporciona herramientas de cliente que puede utilizar para administrar estructuras y modelos de minería de datos existentes. Esta sección describe las operaciones de administración que puede realizar con cada entorno.  
  
 Además de estas herramientas, puede administrar los objetos de minería de datos mediante programación con AMO, o utilizar otros clientes que puedan conectarse con una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como, por ejemplo, los complementos de minería de datos para [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007.  
  
## <a name="in-this-section"></a>En esta sección  
 [Mover objetos de minería de datos](moving-data-mining-objects.md)  
  
 [Requisitos y consideraciones de procesamiento &#40;la minería de datos&#41;](processing-requirements-and-considerations-data-mining.md)  
  
 [Usar SQL Server Profiler para supervisar la minería de datos &#40;Analysis Services de minería de datos&#41;](using-sql-server-profiler-to-monitor-data-mining-analysis-services-data-mining.md)  
  
## <a name="location-of-data-mining-objects"></a>Ubicación de los objetos de minería de datos  
 Las estructuras y los modelos de minería de datos que se han procesado se almacenan en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Si crea una conexión a una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos `Immediate` de en modo al desarrollar los objetos de minería de datos, los objetos que cree se agregarán inmediatamente al servidor mientras trabaja. Sin embargo, si diseña los objetos de minería de datos en modo **Sin conexión** , que es el predeterminado cuando se trabaja en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], los objetos de minería que cree solo serán contenedores de metadatos, hasta que los implemente en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Por lo tanto, siempre que realice un cambio en un objeto, deberá volver a implementarlo en el servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para más información sobre la arquitectura de minería de datos, vea [Arquitectura física &#40;Analysis Services - Minería de datos&#41;](physical-architecture-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Algunos clientes, como los complementos de minería de datos para [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007, también permiten crear modelos de minería de datos y estructuras de minería de datos de sesión que usan una conexión a una instancia, aunque solo almacenan la estructura y los modelos de minería de datos en el servidor durante el transcurso de la sesión. Aun así, podrá administrar estos modelos a través del cliente, al igual que si las estructuras y los modelos estuvieran almacenados en una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Sin embargo, los objetos no se conservarán después de que se desconecte de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="managing-data-mining-objects-in-sql-server-data-tools"></a>Administrar objetos de minería de datos en herramientas de datos de SQL Server  
 
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] proporciona características que facilitan la creación, exploración y edición de los objetos de minería de datos.  
  
 Los vínculos siguientes proporcionan información sobre cómo puede modificar objetos de minería de datos utilizando [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]:  
  
-   [Modifique la vista del origen de datos utilizada para una estructura de minería de datos](edit-the-data-source-view-used-for-a-mining-structure.md)  
  
-   [Cambiar las propiedades de una estructura de minería de datos](change-the-properties-of-a-mining-structure.md)  
  
-   [Cambiar las propiedades de un modelo de minería de datos](change-the-properties-of-a-mining-model.md)  
  
-   [Ver o cambiar las marcas de modelado &#40;minería de datos&#41;](modeling-flags-data-mining.md)  
  
-   [Ver o cambiar parámetros del algoritmo](view-or-change-algorithm-parameters.md)  
  
 Normalmente, utilizará [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] como herramienta para desarrollar nuevos proyectos y agregarlos a proyectos existentes, y, a continuación, administrará los proyectos y los objetos que se han implementado con herramientas como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Sin embargo, puede modificar directamente los objetos que ya se han implementado en una instancia de ssASnoversion mediante la opción de `Immediate` y conectándose al servidor en modo en línea. Para obtener más información, vea [Connect in Online Mode to an Analysis Services Database](../multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md).  
  
> [!WARNING]  
>  Todos los cambios realizados en una estructura o modelo de minería de datos, incluso los cambios realizados en los metadatos, como un nombre o una descripción, requieren que se vuelva a procesar la estructura o modelo.  
  
 Si no tiene el archivo de solución que se usó para crear el proyecto o los objetos de minería de datos, puede importar el proyecto existente del servidor mediante el asistente para la importación de Analysis Services, realizar modificaciones en los objetos y, a continuación, volver a implementarlo con la opción `Incremental`. Para obtener más información, vea [Importar un proyecto de minería de datos mediante el Asistente para la importación de Analysis Services](import-a-data-mining-project-using-the-analysis-services-import-wizard.md).  
  
## <a name="managing-data-mining-objects-in-sql-server-management-studio"></a>Administrar objetos de minería de datos en SQL Server Management Studio  
 En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puede crear scripts, procesar o eliminar estructuras y modelos de minería de datos. Solo podrá visualizar un conjunto limitado de propiedades utilizando el Explorador de objetos; sin embargo, puede ver metadatos adicionales relativos a los modelos de minería de datos abriendo una ventana de **consultas DMX** y seleccionando una estructura de minería de datos.  
  
-   [Crear una consulta DMX en SQL Server Management Studio](create-a-dmx-query-in-sql-server-management-studio.md)  
  
## <a name="managing-data-mining-objects-programmatically"></a>Administrar objetos de minería de datos mediante programación  
 Puede crear, modificar, procesar y eliminar objetos de minería de datos utilizando los lenguajes de programación siguientes. Cada lenguaje está diseñado para desempeñar tareas diferentes, por lo que podría haber restricciones en cuanto al tipo de operaciones que puede llevar a cabo. Por ejemplo, algunas propiedades de los objetos de minería de datos no se pueden cambiar usando Extensiones de minería de datos (DMX); deberá usar XMLA o AMO.  
  
### <a name="analysis-management-objects-amo"></a>Objetos de administración de análisis (AMO)  
 Objetos de administración de análisis (AMO) es un modelo de objetos basado en XMLA que le proporciona un control total sobre los objetos de minería de datos. AMO le permite crear, implementar y supervisar estructuras y modelos de minería de datos.  
  
-   [Modelo de objetos y conceptos de AMO](https://docs.microsoft.com/bi-reference/amo/amo-concepts-and-object-model)  
  
-   <xref:Microsoft.AnalysisServices>  
  
 **Restricciones:** Ninguna.  
  
### <a name="data-mining-extensions-dmx"></a>Extensiones de minería de datos (DMX)  
 Las extensiones de minería de datos (DMX) se pueden utilizar con otras interfaces de comandos, como [!INCLUDE[vstecado](../../includes/vstecado-md.md)] o ADOMD.Net para crear, eliminar y consultar estructuras y modelos de minería de datos.  
  
-   [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](/sql/dmx/dmx-statements-data-definition)  
  
 **Restricciones:** Algunas propiedades no se pueden cambiar mediante DMX.  
  
### <a name="xml-for-analysis-xmla"></a>XML for Analysis (XMLA)  
 XML for Analysis (XMLA) es el lenguaje de definición de datos para todos los Analysis Services. XMLA proporciona control sobre la mayoría de los objetos de minería de datos y las operaciones del servidor. Todas las operaciones de administración entre el cliente y el servidor se pueden realizar usando XMLA. Para su comodidad, puede usar el lenguaje de scripting de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ASSL) para encapsular el XML.  
  
 **Restricciones:** [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] genera algunas instrucciones XMLA que solo se admiten para uso interno y que no se pueden usar en scripts DDL XML.  
  
## <a name="see-also"></a>Consulte también  
 [Guía del desarrollador &#40;Analysis Services&#41;](../analysis-services-developer-documentation.md)  
  
  
