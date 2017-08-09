---
title: "Documentación técnica de SQL Server | Microsoft Docs"
ms.date: 06/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.portal.f1
helpviewer_keywords:
- documentation [SQL Server], home page
- Help [SQL Server]
- SQL Server, documentation
- home page [SQL Server]
- Help [SQL Server], documentation home page
- Books Online [SQL Server], home page
- portal page [SQL Server]
ms.assetid: 674933a8-e423-4d44-a39b-2a997e2c2333
caps.latest.revision: 106
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: aad94f116c1a8b668c9a218b32372424897a8b4a
ms.openlocfilehash: 334c3d130a1d0c8371c1a7810d82d443e1fbecc8
ms.contentlocale: es-es
ms.lasthandoff: 07/31/2017

---
# <a name="sql-server-technical-documentation"></a>Documentación técnica de SQL Server
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 > Para obtener contenido relacionado con versiones anteriores de SQL Server, vea [Instalación de SQL Server 2014](https://msdn.microsoft.com/en-US/library/bb500469(SQL.120).aspx).

 Documentación que le ayuda a instalar, configurar y usar SQL Server. El contenido incluye ejemplos descentralizados, ejemplos de código y vídeos. Para temas sobre el lenguaje [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] , consulte [Referencia del lenguaje](../t-sql/language-reference.md).

También puede ver la documentación de SQL Server sin conexión mediante el Visor de Ayuda. Para más información, vea [Visor de Ayuda y contenido sin conexión para SQL Server](../release-notes/sql-server-help-installation.md).

**SQL Server 2017**

- [Notas de la versión de SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)
- [Novedades de SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)
 
**SQL Server 2016:**
 
- [Notas de la versión de SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
- [Novedades de SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)
    
 **Probar SQL Server**    
 - [**Descargar SQL Server 2016 desde el Centro de evaluación**](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) 
 - **[Poner en marcha una máquina virtual con SQL Server 2016 ya instalado](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)**    
 - **[Descargar la versión más reciente de SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)**   
      
## <a name="sql-server-technologies"></a>Tecnologías de SQL Server    
    
|||    
|-|-|    
|![Motor de base de datos de SQL](../sql-server/media/sql-database-engine.png "Motor de base de datos de SQL")|**[Motor de base de datos](../database-engine/configure-windows/sql-server-database-engine.md)**<br /><br /> El Motor de base de datos es el servicio principal para almacenar, procesar y proteger datos. El Motor de base de datos proporciona acceso controlado y procesamiento rápido de transacciones para cumplir los requisitos de las aplicaciones consumidoras de datos más exigentes de su empresa. El Motor de base de datos también proporciona una completa compatibilidad para mantener una gran disponibilidad.|    
|![R Server](../sql-server/media/r-server.png "R Server")|**[R Services](../advanced-analytics/r-services/r-services.md)**<br /><br /> Microsoft R Services proporciona varias maneras de incorporar el popular lenguaje R en los flujos de trabajo de la empresa.<br /><br /> [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] integra el lenguaje R con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], facilitando así la compilación, el reciclaje y los modelos de puntuación llamando a los procedimientos almacenados de [!INCLUDE[tsql](../includes/tsql-md.md)] .<br /><br /> Microsoft R Server proporciona compatibilidad multiplataforma y escalable para R en la empresa y admite orígenes de datos como Hadoop y Teradata.|    
|![Data Quality Services](../sql-server/media/data-quality-services.png "Data Quality Services")|**[Data Quality Services](../data-quality-services/data-quality-services.md)**<br /><br /> SQL Server Data Quality Services (DQS) proporciona una solución de limpieza de datos controlada por conocimiento. DQS permite generar una base de conocimiento y usarla para realizar tareas de corrección de datos y eliminación de datos duplicados, usando medios asistidos por ordenador e interactivos. Puede usar servicios de consulta de datos basados en la nube y puede generar una solución de administración de datos que integra DQS con SQL Server Integration Services y Master Data Services.|    
|![Integration Services](../sql-server/media/integration-services.png "Integration Services")|**[Integration Services](../integration-services/sql-server-integration-services.md)**<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] es una plataforma para generar soluciones de integración de datos de alto rendimiento, lo que incluye paquetes que proporcionan procesamiento de extracción, transformación y carga (ETL) para almacenamiento de datos.|    
|![Master Data Services](../sql-server/media/master-data-services.png)|**[Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md)**<br /><br /> [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] es la solución de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para la administración de datos maestros. Una solución basada en [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ayuda a asegurarse de que los informes y los análisis se basan en la información correcta. Con [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], se crea un repositorio central de los datos maestros y se mantiene un registro auditable y protegible de los mismos a medida que van cambiando con el tiempo.|    
|![Analysis Services](../sql-server/media/analysis-services.png "Analysis Services")|**[Analysis Services](../analysis-services/analysis-services.md)**<br /><br /> [!INCLUDE[ssASnoversion_md](../includes/ssasnoversion-md.md)] es una plataforma y un conjunto de herramientas de datos analíticos para Business Intelligence en un entorno personal, de equipo o empresa. Los servidores y los diseñadores de cliente admiten soluciones OLAP tradicionales, nuevas soluciones de modelado tabular y análisis y colaboración de autoservicio mediante [!INCLUDE[ssGemini](../includes/ssgemini-md.md)], Excel y un entorno de SharePoint Server. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] también incluye minería de datos para permitir descubrir las relaciones y los patrones ocultos en grandes volúmenes de datos.|    
|![Servicios de replicación](../sql-server/media/replication-services.png "Servicios de replicación")|**[Replicación](../relational-databases/replication/sql-server-replication.md)**<br /><br /> La replicación es un conjunto de tecnologías destinadas a la copia y distribución de datos y objetos de base de datos de una base de datos a otra, para luego sincronizar ambas bases de datos con el fin de mantener su coherencia. La replicación permite distribuir datos a diferentes ubicaciones y a usuarios remotos o móviles mediante redes de área local y de área extensa, conexiones de acceso telefónico, conexiones inalámbricas e Internet.|    
|![Reporting Services](../sql-server/media/reporting-services.png "Reporting Services")|**[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)**<br /><br /> Reporting Services ofrece funcionalidad empresarial de informes habilitados para web con el fin de poder crear informes que extraigan contenido a partir de diversos orígenes de datos, publicar informes con distintos formatos y administrar la seguridad y las suscripciones de forma centralizada.|    

    
## <a name="earlier-sql-server-versions"></a>Versiones anteriores de SQL Server
- [Libros en pantalla de SQL Server 2014](https://msdn.microsoft.com/library/ms130214(v=sql.120).aspx)
- [Instalar SQL Server 2014 Express y otras versiones anteriores de SQL Server](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx). (**Gracias a [Scott Hanselman](http://www.hanselman.com/) por recopilar todos los vínculos de paquetes del instalador en un solo lugar**)  
- [Documentación técnica de SQL Server 2012](https://technet.microsoft.com/library/bb418433(v=sql.10).aspx)  
- [Documentación del producto SQL Server 2008 R2](https://msdn.microsoft.com/library/hh278298(v=sql.10).aspx)  
- [Documentación técnica de SQL Server 2008](https://msdn.microsoft.com/library/hh994727(v=sql.10).aspx) 
- [Documentación archivada de SQL Server 2005](https://msdn.microsoft.com/library/hh278313(v=sql.10).aspx)    

**Bases de datos de ejemplo**  
- [Base de datos de ejemplo de Wide World Importers](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx)  
- [Bases de datos de ejemplo y scripts de AdventureWorks para SQL Server 2016](https://www.microsoft.com/en-us/download/details.aspx?id=49502) 
- [Ejemplos de SQL Server en GitHub](https://github.com/Microsoft/sql-server-samples) 
   
 ## <a name="more-information"></a>Más información   
+ [Administrador de configuración de SQL Server](../relational-databases/sql-server-configuration-manager.md)
+ Vínculos e información del[Centro de actualizaciones de SQL Server](https://msdn.microsoft.com/library/ff803383.aspx) sobre todas las versiones compatibles 
+ [Instalar el motor de base de datos de SQL Server](../database-engine/install-windows/install-sql-server-database-engine.md) 
+ [Instalar las Herramientas de administración de SQL Server con SSMS](https://msdn.microsoft.com/library/bb500441.aspx) 
+ [Herramientas de datos de SQL Server en Visual Studio 2015](https://msdn.microsoft.com/mt186501.aspx)
+ [Vídeos, ejemplos y recursos de la comunidad](https://msdn.microsoft.com/library/dn237258.aspx)
  
[!INCLUDE[feedback_stackoverflow_msdn_connect-md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

