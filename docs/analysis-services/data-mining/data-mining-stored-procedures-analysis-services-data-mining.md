---
title: 'Procedimientos almacenados de minería de datos (Analysis Services: minería de datos) | Documentos de Microsoft'
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 86de302df302ae12ca83216dff998b4c7b39333b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="data-mining-stored-procedures-analysis-services---data-mining"></a>Procedimientos almacenados de minería de datos (Analysis Services - Minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite procedimientos almacenados escritos en cualquier lenguaje administrado. Entre los lenguajes administrados admitidos se incluyen [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET, C# y C++ administrado. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puede llamar a los procedimientos almacenados directamente mediante la instrucción **CALL** o como parte de una consulta DMX (Extensiones de minería de datos).  
  
 Para obtener más información sobre cómo llamar a procedimientos almacenados de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , vea [Llamar a procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md).  
  
 Para obtener información general acerca de la programación, vea [programación de minería de datos](../../analysis-services/data-mining-programming.md).  
  
 Para obtener información adicional sobre cómo programar objetos de minería de datos, vea el artículo relativo a la[programabilidad de la minería de datos de SQL Server](http://go.microsoft.com/fwlink/?LinkId=93735)" en MSDN Library.  
  
> [!NOTE]  
>  Al consultar modelos de minería de datos y, sobre todo, al probar nuevas soluciones de minería de datos, puede ser útil llamar a los procedimientos almacenados del sistema utilizados internamente por el motor de minería de datos. Para ver los nombres de estos procedimientos almacenados del sistema, utilice [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para crear un seguimiento en el servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y, a continuación, cree, examine y consulte los modelos de minería de datos. Sin embargo, [!INCLUDE[msCoName](../../includes/msconame-md.md)] no garantiza la compatibilidad de los procedimientos almacenados del sistema entre distintas versiones y nunca debe utilizar las llamadas a este tipo de procedimientos en un sistema de producción. En su lugar, para obtener compatibilidad, debe crear sus propias consultas con DMX o XML/A.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [SystemGetCrossValidationResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterCrossValidationResults & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetAccuracyResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterAccuracyResults & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
## <a name="see-also"></a>Vea también  
 [Validación cruzada &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)   
 [Pestaña validación cruzada &#40;vista Gráfico de precisión de minería de datos&#41;](http://msdn.microsoft.com/library/bd215a68-1ad7-4046-9c44-ec8e2be13a64)   
 [Llamar a un procedimiento almacenado](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
  
  
