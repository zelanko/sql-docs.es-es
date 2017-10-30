---
title: "Características compatibles con las ediciones de SQL Server Integration Services | Documentos de Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 8cc1fcfdeae8742a93916dfb08c9db1215f88721
ms.openlocfilehash: e9d1b8851f113fa44264230a79d0e496007ed96b
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="integration-services-features-supported-by-the-editions-of-sql-server"></a>Características de Integration Services compatibles con las ediciones de SQL Server
 En este tema, encontrará información detallada sobre las características de SQL Server Integration Services (SSIS) admitidas por las diversas ediciones de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].  

Para características compatibles con las ediciones Evaluation y Developer, vea las características descritas en Enterprise Edition en las tablas siguientes.
  
Para obtener las notas de la versión más recientes y ¿qué es información nueva, vea los siguientes artículos:
-   [Notas de la versión de SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
-   [Novedades de Integration Services en SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [Novedades de Integration Services en SQL Server 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)
    
**Pruebe SQL Server 2016.**    

La edición de evaluación de SQL Server está disponible durante un período de prueba de 180 días.  
    
> [![Descargar desde el centro de evaluación](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Descargar SQL Server 2016 desde el centro de evaluación](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
## <a name="ISNew"></a>Nuevas características de Integration Services en SQL Server 2017
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Escalado horizontal Master|Sí|||||
|Escalado del trabajo|Sí|Sí <sup>1</sup>|TBD|TBD|TBD|
|Soporte para Microsoft Dynamics AX y Microsoft Dynamics CRM en componentes de OData <sup>2</sup>|Sí|Sí||||

<sup>1</sup> si ejecuta paquetes que requieren características solo Enterprise en horizontalmente, también debe ejecutar los trabajos de salida de escala en las instancias de SQL Server Enterprise.

<sup>2</sup> esta característica también se admite en SQL Server 2016 con Service Pack 1.

## <a name="IEWiz"></a>Importación de SQL Server y el Asistente para exportación

|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Asistente para importación y exportación de SQL Server|Sí|Sí|Sí|Sí|Sí|  

## <a name="IS"></a> Integration Services  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Conectores de origen de datos integrados|Sí|Sí|||| 
|Tareas y transformaciones integradas|Sí|Sí||||  
|Origen ODBC y destino de Attunity|Sí|Sí|||| 
|Tareas y conectores de origen de datos de Azure|Sí|Sí||||  
|Tareas y conectores de Hadoop y HDFS|Sí|Sí||||  
|Herramientas de generación de perfiles de datos básicos|Sí|Sí|||| 

## <a name="ISAA"></a>Integration Services - avanzadas orígenes y destinos  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Origen de Oracle de alto rendimiento y de destino de Attunity|Sí|||||  
|Origen de Teradata de alto rendimiento y de destino de Attunity|Sí|||||  
|Origen y destino de SAP BW|Sí|||||  
|Destino de entrenamiento del modelo de minería de datos|Sí|||||  
|Destino de procesamiento de dimensiones|Sí|||||  
|Destino de procesamiento de particiones|Sí|||||  
  
## <a name="ISAT"></a>Integration Services - avanzadas tareas y transformaciones  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Cambiar los componentes de la captura de datos de Attunity <sup>1</sup>|Sí|||||  
|Transformación de consulta de minería de datos|Sí|||||  
|Transformaciones de búsqueda aproximada y agrupación aproximada|Sí|||||  
|Extracción de términos y las transformaciones de búsqueda de términos|Sí|||||  

<sup>1</sup> componentes de la captura de datos modificados de Attunity requieren Enterprise edition. Change Data Capture Service y Change Data Capture Designer, sin embargo, no requieren Enterprise edition. Puede usar el diseñador y el servicio en un equipo donde SSIS no está instalado.

