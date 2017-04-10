---
title: "Procedimientos almacenados de miner&#237;a de datos (Analysis Services - Miner&#237;a de datos) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "procedimientos almacenados [Analysis Services], minería de datos"
ms.assetid: a751856d-33bd-4788-9593-317b2826132d
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 26
---
# Procedimientos almacenados de miner&#237;a de datos (Analysis Services - Miner&#237;a de datos)
  A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite procedimientos almacenados escritos en cualquier lenguaje administrado. Entre los lenguajes administrados admitidos se incluyen [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET, C# y C++ administrado. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puede llamar a los procedimientos almacenados directamente mediante la instrucción **CALL** o como parte de una consulta DMX (Extensiones de minería de datos).  
  
 Para obtener más información sobre cómo llamar a procedimientos almacenados de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Llamar a procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md).  
  
 Para obtener información general sobre la programación de [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)], vea [Programación de minería de datos](../../analysis-services/data-mining-programming.md).  
  
 Para obtener información adicional sobre cómo programar objetos de minería de datos, vea el artículo relativo a la[programabilidad de la minería de datos de SQL Server](http://go.microsoft.com/fwlink/?LinkId=93735)" en MSDN Library.  
  
> [!NOTE]  
>  Al consultar modelos de minería de datos y, sobre todo, al probar nuevas soluciones de minería de datos, puede ser útil llamar a los procedimientos almacenados del sistema utilizados internamente por el motor de minería de datos. Para ver los nombres de estos procedimientos almacenados del sistema, utilice [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para crear un seguimiento en el servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y, a continuación, cree, examine y consulte los modelos de minería de datos. Sin embargo, [!INCLUDE[msCoName](../../includes/msconame-md.md)] no garantiza la compatibilidad de los procedimientos almacenados del sistema entre distintas versiones y nunca debe utilizar las llamadas a este tipo de procedimientos en un sistema de producción. En su lugar, para obtener compatibilidad, debe crear sus propias consultas con DMX o XML/A.  
  
## En esta sección  
  
-   [SystemGetCrossValidationResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterCrossValidationResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetAccuracyResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterAccuracyResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
## Referencia  
 [Crear scripts para tareas administrativas en Analysis Services](../../analysis-services/instances/script-administrative-tasks-in-analysis-services.md)  
  
## Vea también  
 [Validación cruzada &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)   
 [Pestaña Validación cruzada &#40;vista Gráfico de precisión de minería de datos&#41;](../Topic/Cross-Validation%20Tab%20\(Mining%20Accuracy%20Chart%20View\).md)   
 [Llamar a un procedimiento almacenado](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
  
  