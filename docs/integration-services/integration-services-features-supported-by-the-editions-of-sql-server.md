---
title: "Caracter&#237;sticas de Integration Services compatibles con las ediciones de SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
caps.latest.revision: 15
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Caracter&#237;sticas de Integration Services compatibles con las ediciones de SQL Server
 En este tema, encontrará información detallada sobre las características de SQL Server Integration Services (SSIS) admitidas por las diversas ediciones de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].  

Para conocer las características admitidas por las ediciones Evaluation y Developer, consulte SQL Server Enterprise Edition. 
  
Para leer las notas de la versión más reciente e información sobre las novedades, vea lo siguiente:
-   [Notas de la versión de SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
-   [Novedades de Integration Services en SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [Novedades de Integration Services en SQL Server vNext](../integration-services/what-s-new-in-integration-services-in-sql-server-vnext.md)
    
**Probar SQL Server 2016**    

La edición de evaluación de SQL Server está disponible durante un período de prueba de 180 días.  
    
> [![Descargar desde el centro de evaluación](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Descargar SQL Server 2016 desde el centro de evaluación](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Máquina virtual de Azure pequeña ](../analysis-services/media/azure-virtual-machine-small.png)**[Poner en marcha una máquina virtual con SQL Server 2016 ya instalado](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    

##  <a name="a-nameisanew-integration-services-features-in-sql-server-vnext"></a><a name="IS"></a>Nuevas características de Integration Services en SQL Server vNext
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express con herramientas|Express|Desarrollador|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Escalar horizontalmente|Sí||||||Sí|
|Compatibilidad con Microsoft Dynamics AX y Microsoft Dynamics CRM en componentes de OData <sup>1</sup>|Sí|Sí|||||Sí|

<sup>1</sup> Esta característica también se admite en SQL Server 2016 con Service Pack 1.

##  <a name="a-nameisa-integration-services"></a><a name="IS"></a> Integration Services  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express con herramientas|Express|Desarrollador|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Conectores de origen de datos integrados|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Tareas y conectores de origen de datos de Azure|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Asistente para importación y exportación de SQL Server|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Conectores y tareas de Hadoop/HDFS|Sí|Sí|Sí||||Sí|  
|Diseñador y tiempo de ejecución de SSIS|Sí|Sí|||||Sí|  
|Tareas y transformaciones integradas|Sí|Sí|||||Sí|  
|Herramientas de generación de perfiles de datos básicos|Sí|Sí|||||Sí|  
|Servicio de captura de datos modificados para Oracle de Attunity|Sí||||||Sí|  
|Diseñador de captura de datos modificados para Oracle de Attunity|Sí||||||Sí| 

##  <a name="a-nameisaaa-integration-services---advanced-adapters"></a><a name="ISAA"></a> Integration Services: adaptadores avanzados  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express con herramientas|Express|Desarrollador|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Destino de Oracle de alto rendimiento|Sí||||||Sí|  
|Destino de teradatos de alto rendimiento|Sí||||||Sí|  
|Origen y destino de SAP BW|Sí||||||Sí|  
|Adaptador de destino de entrenamiento del modelo de minería de datos|Sí||||||Sí|  
|Adaptador de destino de procesamiento de dimensiones|Sí||||||Sí|  
|Adaptador de destino de procesamiento de particiones|Sí||||||Sí|  
|Componentes de Captura de datos modificados de Attunity|Sí||||||Sí|  
|Conector de Conectividad abierta de base de datos (ODBC) de Attunity|Sí||||||Sí|  
  
##  <a name="a-nameisata-integration-services---advanced-transforms"></a><a name="ISAT"></a> Integration Services: transformaciones avanzadas  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express con herramientas|Express|Desarrollador|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Búsquedas persistentes (alto rendimiento)|Sí||||||Sí|  
|Transformación de consulta de minería de datos|Sí||||||Sí|  
|Transformaciones de búsqueda y agrupación aproximada|Sí||||||Sí|  
|Transformaciones de búsqueda y extracción de términos|Sí||||||Sí|  
  