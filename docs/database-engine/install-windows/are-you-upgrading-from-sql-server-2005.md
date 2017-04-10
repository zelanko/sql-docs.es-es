---
title: "&#191;Desea actualizar desde SQL Server 2005? | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad40e66f-71fe-4ee6-9ce3-17127e7b1d7a
caps.latest.revision: 21
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 21
---
# &#191;Desea actualizar desde SQL Server 2005?
  Como el soporte extendido de SQL Server 2005 llega a su fin, es un buen momento para actualizar a una versión más reciente de SQL Server y a Base de datos SQL de Azure. La actualización permite mantener la seguridad y el cumplimiento, lograr un rendimiento excepcional y optimizar la infraestructura de su plataforma de datos.  
  
 Para obtener más información, orientación y herramientas para planear y automatizar la actualización o migración, consulte [Finalización del soporte de SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
## ¿Por qué es recomendable actualizar?  
  
> [!IMPORTANT]  
>  El soporte extendido de SQL Server 2005 finaliza el 12 de abril de 2016. Si sigue ejecutando SQL Server 2005 después del 12 de abril de 2016, ya no recibirá actualizaciones de seguridad.  
  
 Para obtener la hoja de datos en formato PDF en la que se explican las ventajas de actualizar desde SQL Server 2005, [haga clic aquí](https://info.microsoft.com/rs/157-GQE-382/images/EN-CNTNT-Infographic-UpgradeSQL2005Datasheet.pdf) (no en la imagen en miniatura que aparece aquí).  
  
 ![Data sheet about upgrading from SQL Server 2005](../../database-engine/install-windows/media/sqlserver2005eos.png "Data sheet about upgrading from SQL Server 2005")  
  
## Elija la opción de actualización  
 Si va a actualizar bases de datos relacionales de SQL Server 2005, estas son las opciones de almacenamiento relacional en la plataforma de Microsoft.  
  
 Para ver un análisis más exhaustivo de estas opciones, [haga clic aquí](http://sql05upgrade.azurewebsites.net/).  
  
|Opción de almacenamiento relacional|Ventajas|Otros factores a tener en cuenta|  
|-------------------------------|--------------|-------------------------------|  
|**SQL Server local**<br /><br /> Tenga en cuenta esta opción para las aplicaciones de bases de datos de cualquier tipo, desde sistemas transaccionales a almacenes de datos.|Tendrá el máximo control sobre las características y la escalabilidad, ya que administra el hardware y software.<br /><br /> Si está actualizando desde SQL Server 2005, este es el entorno más parecido.|Debe realizar la mayor inversión inicial y proporcionar la administración más continua, porque tiene que comprar, mantener y administrar su propio hardware y software.<br /><br /> Para más información, consulte [SQL Server 2016](https://www.microsoft.com/EN-US/server-cloud/products/sql-server-2016/).|  
|**SQL Server hospedado en máquinas virtuales de Azure**<br /><br /> Tenga en cuenta esta opción si desea lo siguiente:<br /><br /> Ventajas de migrar a un entorno hospedado.<br /><br /> Control sobre el entorno operativo.<br /><br /> Conjunto de características conocidas de SQL Server.|Puede implementar rápidamente desde una biblioteca de imágenes de máquina virtual.<br /><br /> Obtenga el conjunto completo de características de SQL Server.<br /><br /> Ahórrese el costo de hardware y software de servidor. Solo paga por el uso por horas.|Debe configurar y administrar el servidor SQL Server y el software del sistema operativo.<br /><br /> <br /><br /> Para más información, consulte [Información general sobre SQL Server en máquinas virtuales de Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/).<br /><br /> Para obtener información acerca de la migración, consulte [Migrar una base de datos a SQL Server en una máquina virtual de Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-migrate-onpremises-database/).|  
|**Servicio de base de datos hospedado en la base de datos SQL de Azure**<br /><br /> Tenga en cuenta esta opción si desea una solución de bajo costo con menos mantenimiento.<br /><br /> Esta opción es especialmente adecuada para aplicaciones que no requieren la misma capacidad en todo momento o que tiene que proporcionar acceso externo.|Puede implementar rápidamente y escalar fácilmente.<br /><br /> Solo paga por el uso por horas.<br /><br /> El costo del servicio incluye no solo el almacenamiento, sino también copias de seguridad automatizadas y de alta disponibilidad.|La base de datos SQL de Azure carece de algunas características de SQL Server que no son aplicables en un entorno de nube hospedada. Para obtener más información, vea la [información de Transact-SQL de la base de datos SQL de Azure](https://azure.microsoft.com/documentation/articles/sql-database-transact-sql-information/).<br /><br /> La base de datos SQL de Azure también tiene un tamaño máximo de base de datos de 500 GB, en comparación con los 524 PB de SQL Server.<br /><br /> Para más información, consulte [Base de datos SQL](https://azure.microsoft.com/services/sql-database/).<br /><br /> Para obtener información sobre la migración, vea [Migración de una base de datos de SQL Server a una Base de datos SQL de Azure](https://azure.microsoft.com/documentation/articles/sql-database-cloud-migrate/).|  
  
 También debe considerar soluciones NoSQL o no relacionales para determinados datos y aplicaciones.  
  
|Solución no relacional|Ventajas|  
|------------------------------|--------------|  
|**Azure DocumentDB**<br /><br /> Considere esta opción para aplicaciones web, móviles, modernas y escalables que usan datos JSON y requieren una combinación de consultas sólidas y procesamiento de datos transaccionales.<br /><br /> Para obtener más información, consulte [DocumentDB](https://azure.microsoft.com/en-us/services/documentdb/).<br /><br /> Para obtener información sobre cómo importar datos, vea [Importación de datos en DocumentDB](https://azure.microsoft.com/documentation/articles/documentdb-import-data/).|Los documentos se indizan y se puede usar la conocida sintaxis SQL para consultarlos.<br /><br /> La base de datos no tiene esquema.<br /><br /> Puede agregar propiedades a los documentos sin tener que volver a generar índices.<br /><br /> Obtiene compatibilidad con JSON y JavaScript directamente del motor de la base de datos.<br /><br /> Obtiene soporte nativo para datos geoespaciales e integración con otros servicios de Azure, incluidas la Búsqueda de Azure, HDInsight y la Factoría de datos.<br /><br /> Obtenga una latencia baja, almacenamiento de alto rendimiento con niveles de rendimiento reservados.|  
|**Almacenamiento de tablas de Azure**<br /><br /> Tenga en cuenta esta opción para almacenar petabytes de datos semiestructurados en una solución rentable.<br /><br /> Para obtener más información, consulte [Almacenamiento de tablas](https://azure.microsoft.com/services/storage/tables/).|Pueden desarrollar las aplicaciones y el esquema de tabla sin tener que desconectar los datos.<br /><br /> Puede escalar sin tener que realizar un particionamiento del conjunto de datos.<br /><br /> Obtiene almacenamiento con redundancia geográfica que replica los datos en varias regiones.|  
  
 Para descargar el informe "Migración desde SQL Server 2005" de Indicaciones en Microsoft, [haga clic aquí](https://info.microsoft.com/CO-SQL-CNTNT-FY16-09Sep-14-ModernizationDirOnMFST-Register.html) (no en la imagen en miniatura que aparece aquí).  
  
 ![Report about migrating from SQL Server 2005](../../database-engine/install-windows/media/sqlserver2005migratingdoc.png "Report about migrating from SQL Server 2005")  
  
## Planee su actualización  
  
-   Lea la siguiente serie de publicaciones de blog del equipo de SQL Server sobre cómo planear su actualización.  
  
    -   [Planear una actualización eficaz de SQL Server 2005: paso 1 de 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/10/planning-an-efficient-upgrade-from-sql-server-2005-step-1-of-3.aspx)  
  
    -   [Planear una actualización eficaz de SQL Server 2005: paso 2 de 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/15/planning-an-efficient-upgrade-from-sql-server-2005-step-2-of-3.aspx)  
  
    -   [Planear una actualización eficaz de SQL Server 2005: paso 3 de 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/17/planning-an-efficient-upgrade-from-sql-server-2005-step-3-of-3.aspx)  
  
-   Revise los requisitos y las consideraciones en [Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md), incluidos los [Hardware and Software Requirements for Installing SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md).  
  
-   Lea cómo llevar a cabo la actualización.  
  
    -   Revise los métodos de actualización disponibles y aprenda a planear y realizar pruebas en el tema [Upgrade Database Engine](../../database-engine/install-windows/upgrade-database-engine.md).  
  
        > [!IMPORTANT]  
        >  No puede actualizar un servidor SQL Server 2005 a SQL Server 2016 in situ. Debe instalar SQL Server 2016 y después migrar las bases de datos de SQL Server 2005 a la nueva instalación. Para más información, vea la sección "New Installation Upgrade" (Nueva actualización de la instalación) en el tema [Choose a Database Engine Upgrade Method](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
  
    -   Para obtener la guía de actualización técnica más detallada en formato PDF, [haga clic aquí](http://download.microsoft.com/download/7/1/5/715BDFA7-51B6-4D7B-AF17-61E78C7E538F/SQL_Server_2014_Upgrade_technical_guide.pdf).  
  
        > [!NOTE]  
        >  Actualmente, esta es la versión de SQL Server 2014 de la "Guía de actualización técnica". La versión de SQL Server 2016 de la guía no está disponible todavía.  
  
-   Para obtener más información, orientación y herramientas para planear y automatizar la actualización o migración, consulte [Finalización del soporte de SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
## Obtener SQL Server 2016  
 Para descargar una copia de evaluación de SQL Server 2016, [haga clic aquí](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016/?wt.mc_id=upgrade2005).  
  
## Vea también  
 [SQL Server 2016](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2016/default.aspx)   
 [Finalización del soporte de SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)   
 [Actualización de SQL Server 2005 a SQL Server 2014](https://msdn.microsoft.com/en-us/library/mt170591\(v=sql.120\).aspx)  
  
  