---
title: Administración de información empresarial mediante SSIS, MDS y DQS juntos [Tutorial] Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba09b504-3007-4cb7-8ef8-f01adbf51646
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 29ed5816a3a5fc0af6c5a4ac144557933e3e1a5f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487724"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>Administración de información empresarial mediante SSIS, MDS y DQS [Tutorial]
  La administración de información en una empresa suele implicar la integración de datos procedentes de la empresa y externos, la limpieza de datos, la búsqueda de coincidencias en los datos para quitar duplicados, la normalización de los datos, el enriquecimiento de los datos, hacer que los datos cumplan los requisitos legales y de cumplimiento, y su almacenamiento posterior en una ubicación centralizada con todas las configuraciones de seguridad necesarias.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] proporciona todos los componentes necesarios para lograr una solución eficiente de Administración de información empresarial (EIM) en un único producto. Los componentes clave que ayudan a crear una solución de EIM son los siguientes:  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   SQL Server Master Data Services  
  
 SQL Server Integration Services (SSIS) proporciona una plataforma extensible y eficaz para la integración de datos procedentes de diversos orígenes en una solución completa de extracción, transformación y carga (ETL) que admite flujos de trabajo empresariales, un almacenamiento de datos o administración de datos maestros. Consulte el tema Información general de [Integration ServicesIntegration Services](https://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx) para obtener información general rápida y los usos típicos de SSIS.  
  
 SQL Server Data Quality Services (DQS) permite limpiar, buscar coincidencias, normalizar y enriquecer los datos, de forma que pueda entregar información de confianza para Business Intelligence, un almacenamiento de datos y cargas de trabajo de procesamiento de transacciones. Consulte el tema [Introducción](https://msdn.microsoft.com/library/ff877917.aspx) a Data Quality Services para conocer la necesidad empresarial de DQS y cómo DQS responde a la necesidad.  
  
 SQL Server Master Data Services (MDS) proporciona un concentrador central de datos que garantiza que la integridad de la información y la coherencia de los datos es constante en las diferentes aplicaciones. Consulte el tema Información general de [Master Data ServicesMaster Data Services](../master-data-services/master-data-services-overview-mds.md) para obtener descripciones breves de las características importantes de MDS.  
  
 Consulte Limpieza y coincidencia de datos maestros mediante documentos técnicos de [EIM Technologies](https://msdn.microsoft.com/library/hh403491.aspx) para obtener una guía completa sobre la implementación de una solución EIM mediante estas tecnologías de Microsoft EIM y vea [Enterprise Information Management (EIM): Reunir vídeo sSIS, DQS y MDS](https://go.microsoft.com/fwlink/?LinkId=258672) para obtener una demostración completa de un escenario EIM.  
  
 En este tutorial, aprenderá a usar conjuntamente SSIS, MDS y DQS para implementar una solución de ejemplo de Administración de información empresaria (EIM). Primero usará DQS para crear una base de conocimiento que contenga conocimiento sobre los datos de proveedor (metadatos), limpiar los datos de un archivo de Excel con la base de conocimiento, y buscar coincidencias en los datos para identificar y quitar duplicados en los datos. Después usará el complemento MDS para Excel con el fin de cargar los datos limpios y coincidentes en MDS. A continuación, automatizará todo el proceso mediante una solución de SSIS. La solución SSIS de este tutorial lee los datos de entrada de un archivo de Excel, pero puede ampliarlos para leerlos de varios orígenes, como Oracle, Teradata, DB2 y Azure SQL Database.  
  
## <a name="prerequisites"></a>Prerrequisitos  
  
1.  Microsoft SQL Server 2012 con los siguientes componentes instalados.  
  
    1.  Integration Services (SSIS)  
  
    2.  Master Data Services (MDS)  
  
    3.  Data Quality Services (DQS)  
  
    4.  SQL Server Data Tools  
  
         Consulte la Guía de instalación de [SQL Server 2012](../database-engine/install-windows/installation-for-sql-server.md) para obtener más información sobre la instalación del producto.  
  
2.  [Configure MDS con el Administrador de configuración de Master Data Services.](https://msdn.microsoft.com/library/ee633884.aspx)  
  
     Use el Administrador de configuración para crear y configurar una base de datos de Master Data Services. Después de crear la base de datos MDS, cree una `http://localhost/MDS`aplicación web para MDS en un sitio web (por ejemplo: ) y asocie la base de datos MDS con la aplicación web MDS. Tenga en cuenta que, para crear una aplicación web de MDS, debe tener instalado IIS en el equipo. Consulte Requisitos de [aplicación web (Master Data Services)](https://msdn.microsoft.com/library/ee633744.aspx) y Requisitos de base de datos [(Master Data Services)](https://msdn.microsoft.com/library/ee633767.aspx) para obtener más información sobre los requisitos previos para configurar la base de datos MDS y la aplicación web.  
  
3.  [Instale y configure DQS mediante el Instalador](https://msdn.microsoft.com/library/hh231682.aspx)de servidor de calidad de datosData Quality Server . Haga clic en **Inicio**, Haga clic en **Todos los programas**, Microsoft SQL Server **2014**, Haga clic en Servicios de calidad de **datosData Quality Services**y, a continuación, haga clic en Instalador de servidor de calidad de **datosData Quality Server**.  
  
4.  Microsoft Excel 2010 (preferiblemente de 32 bits).  
  
5.  Instale **el complemento Master Data Services Master Data Services para Excel** (32 bits o 64 bits según la versión de Excel que tenga en su equipo) desde [aquí.](https://www.microsoft.com/download/details.aspx?id=29064) Para encontrar la versión de Excel instalada en el equipo, ejecute **Excel**, haga clic en **Archivo** en la barra de menús y haga clic en **Ayuda** para ver la versión en el panel derecho. Tenga en cuenta que necesita instalar Visual Studio 2010 Tools para Office Runtime antes de instalar el complemento de Excel.  
  
6.  (Opcional) Cree una cuenta con [Azure Marketplace.](https://azuremarketplace.microsoft.com/marketplace/) Una de las tareas del tutorial requiere que tenga una cuenta de **Azure Marketplace** (denominada originalmente **Data Market).** Puede omitir esta tarea si lo desea y continuar con la tarea siguiente.  
  
7.  Descargue el archivo Suppliers.xls desde el Centro de descarga de [Microsoft.](https://www.microsoft.com/download/details.aspx?id=50426)  
  
8.  DQS no le permite exportar los resultados de limpieza o coincidencia a un archivo de Excel si utiliza la **versión de 64 bits de Excel.** Se trata de un problema conocido. Para solucionar temporalmente este problema, haga lo siguiente:  
  
    1.  Ejecute **DQLInstaller.exe -upgrade**. Si instaló la instancia predeterminada de SQL Server, el archivo DQSInstaller.exe está disponible en C:\Archivos de programa\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn. Haga doble clic en el archivo DQSInstaller.exe.  
  
    2.  En Administrador de configuración de **Master Data ServicesMaster Data Services Configuration Manager**, haga clic en Seleccionar base de **datos**, seleccione la base de datos **MDS** existente y, a continuación, haga clic en **Actualizar**.  
  
## <a name="lessons"></a>Lecciones  
  
|Lección|Breve descripción|Tiempo estimado para completarla (en minutos).|  
|------------|-----------------------|------------------------------------------------|  
|[Lección 1: Creación de la base de conocimiento de DQS Proveedores](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|En esta lección, creará una base de conocimiento de DQS denominada **Proveedores**.|60|  
|[Lección 2: Limpieza de datos de proveedor con la base de conocimiento Proveedores](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|En esta lección, creará y ejecutará un proyecto de DQS para limpiar los datos del proveedor en un archivo de Excel mediante la Base de conocimiento **de proveedores** que creó en la primera lección.|45|  
|[Lección 3: Búsqueda de datos coincidentes para quitar duplicados de lista de proveedores](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|En esta lección, creará un proyecto de DQS para realizar la actividad de coincidencia con el fin de identificar y quitar duplicados de la lista limpia de proveedores.|45|  
|[Lección 4: Almacenamiento de datos de proveedor en MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|En esta lección, cargará los datos de proveedor limpiados y coincidentes en Master Data Services (MDS) mediante el **complemento MDS para Excel**.|45|  
|[Lección 5: Automatización de la limpieza y la búsqueda de coincidencias con SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|En esta lección, creará una solución de SSIS que limpia los datos de entrada con DQS, busca coincidencias en los datos limpios para quitar duplicados, y almacena los datos limpios y coincidentes en MDS de forma automatizada.|75|  
  
## <a name="next-steps"></a>Pasos siguientes  
 Para comenzar el tutorial, continúe con la primera lección: Lección 1: Creación de la base de conocimiento de [DQS de proveedores](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md).  
  
  
