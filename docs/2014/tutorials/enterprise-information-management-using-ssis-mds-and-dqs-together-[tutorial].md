---
title: Administración de información empresarial mediante SSIS, MDS y DQS [Tutorial] | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ba09b504-3007-4cb7-8ef8-f01adbf51646
caps.latest.revision: 11
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bf4106c531dbb1f386f8c1b6745f773bbe3c0f4b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189662"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>Administración de información empresarial mediante SSIS, MDS y DQS [Tutorial]
  La administración de información en una empresa suele implicar la integración de datos procedentes de la empresa y externos, la limpieza de datos, la búsqueda de coincidencias en los datos para quitar duplicados, la normalización de los datos, el enriquecimiento de los datos, hacer que los datos cumplan los requisitos legales y de cumplimiento, y su almacenamiento posterior en una ubicación centralizada con todas las configuraciones de seguridad necesarias.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] proporciona todos los componentes necesarios para lograr una solución eficiente de Administración de información empresarial (EIM) en un único producto. Los componentes clave que ayudan a crear una solución de EIM son los siguientes:  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   SQL Server Master Data Services  
  
 SQL Server Integration Services (SSIS) proporciona una plataforma extensible y eficaz para la integración de datos procedentes de diversos orígenes en una solución completa de extracción, transformación y carga (ETL) que admite flujos de trabajo empresariales, un almacenamiento de datos o administración de datos maestros. Consulte [información general de servicios de integración](http://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx) usa el tema para obtener una introducción rápida y típicos de SSIS.  
  
 SQL Server Data Quality Services (DQS) permite limpiar, buscar coincidencias, normalizar y enriquecer los datos, de forma que pueda entregar información de confianza para Business Intelligence, un almacenamiento de datos y cargas de trabajo de procesamiento de transacciones. Consulte [Introducción a Data Quality Services](http://msdn.microsoft.com/library/ff877917.aspx) tema de la necesidad empresarial de DQS y cómo responde DQS a la necesidad.  
  
 SQL Server Master Data Services (MDS) proporciona un concentrador central de datos que garantiza que la integridad de la información y la coherencia de los datos es constante en las diferentes aplicaciones. Consulte [Master Data Services Overview](http://msdn.microsoft.com/library/ff487003.aspx) tema para ver descripciones breves de características importantes de MDS.  
  
 Consulte [limpieza y coincidencia de patrón de datos con las tecnologías EIM](http://msdn.microsoft.com/library/hh403491.aspx) notas del producto para obtener instrucciones completas sobre cómo implementar una solución EIM utilizando conjuntamente estas tecnologías EIM de Microsoft y la inspección [Enterprise Administración de información (EIM): Reunir SSIS, DQS y MDS](http://go.microsoft.com/fwlink/?LinkId=258672) vídeo para ver una buen demostración de un escenario EIM.  
  
 En este tutorial, aprenderá a usar conjuntamente SSIS, MDS y DQS para implementar una solución de ejemplo de Administración de información empresaria (EIM). Primero usará DQS para crear una base de conocimiento que contenga conocimiento sobre los datos de proveedor (metadatos), limpiar los datos de un archivo de Excel con la base de conocimiento, y buscar coincidencias en los datos para identificar y quitar duplicados en los datos. Después usará el complemento MDS para Excel con el fin de cargar los datos limpios y coincidentes en MDS. A continuación, automatizará todo el proceso mediante una solución de SSIS. La solución de SSIS de este tutorial lee los datos de entrada de un archivo de Excel, pero puede ampliarla para que lea de diversos orígenes como Oracle, Teradata, DB2 y SQL Database de Microsoft Azure.  
  
## <a name="prerequisites"></a>Requisitos previos  
  
1.  Microsoft SQL Server 2012 con los siguientes componentes instalados.  
  
    1.  Integration Services (SSIS)  
  
    2.  Master Data Services (MDS)  
  
    3.  Data Quality Services (DQS)  
  
    4.  Herramientas de datos de SQL Server  
  
         Consulte [Guía de instalación de SQL Server 2012](http://msdn.microsoft.com/library/bb500469.aspx) para obtener más información acerca de cómo instalar el producto.  
  
2.  [Configure MDS con el Administrador de configuración de Master Data Services](http://msdn.microsoft.com/library/ee633884.aspx)  
  
     Use el Administrador de configuración para crear y configurar una base de datos de Master Data Services. Después de crear la base de datos MDS, cree una aplicación web para MDS en un sitio web (por ejemplo: [ http://localhost/MDS ](http://localhost/MDS)) y asociar la base de datos MDS a la aplicación web MDS. Tenga en cuenta que, para crear una aplicación web de MDS, debe tener instalado IIS en el equipo. Consulte [requisitos de la aplicación Web (Master Data Services)](http://msdn.microsoft.com/library/ee633744.aspx) y [requisitos de la base de datos (Master Data Services)](http://msdn.microsoft.com/library/ee633767.aspx) para obtener más información sobre los requisitos previos para configurar la aplicación web y base de datos MDS.  
  
3.  [Instale y Configure DQS mediante el instalador de Data Quality Server](http://msdn.microsoft.com/library/hh231682.aspx). Haga clic en **iniciar**, haga clic en **todos los programas**, haga clic en **Microsoft SQL Server 2014**, haga clic en **Data Quality Services**y, a continuación, haga clic en **Instalador de data Quality Server**.  
  
4.  Microsoft Excel 2010 (preferiblemente de 32 bits).  
  
5.  Instalar **complemento Master Data Services para Excel** (32 bits o 64 bits basado en la versión de Excel que tiene en su equipo) desde [aquí](http://www.microsoft.com/download/details.aspx?id=29064). Para averiguar la versión de Excel instalado en el equipo, ejecute **Excel**, haga clic en **archivo** en la barra de menús y haga clic en **ayuda** para ver la versión en el panel derecho. Tenga en cuenta que deberá instalar Visual Studio 2010 Tools para Office Runtime antes de instalar el complemento de Excel.  
  
6.  (Opcional) Cree una cuenta con [Windows Azure Marketplace](https://datamarket.azure.com/). Una de las tareas del tutorial requiere que tenga un **Azure Marketplace** (denominado originalmente **Data Market**) cuenta. Puede omitir esta tarea si lo desea y continuar con la tarea siguiente.  
  
7.  Descargue el archivo Suppliers.xls desde [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=271504).  
  
8.  DQS no permite exportar la limpieza o coincidencia de los resultados a un archivo de Excel si está utilizando **versión de 64 bits de Excel**. Se trata de un problema conocido. Para solucionar temporalmente este problema, haga lo siguiente:  
  
    1.  Ejecute **DQLInstaller.exe – upgrade**. Si instaló la instancia predeterminada de SQL Server, el archivo DQSInstaller.exe está disponible en C:\Archivos de programa\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn. Haga doble clic en el archivo DQSInstaller.exe.  
  
    2.  En **Administrador de configuración de Master Data Services**, haga clic en **Seleccionar base de datos**, seleccione existente **MDS** de base de datos y, a continuación, haga clic en **actualizar**.  
  
## <a name="lessons"></a>Lecciones  
  
|Lección|Descripción breve|Tiempo estimado para completarla (en minutos).|  
|------------|-----------------------|------------------------------------------------|  
|[Lección 1: Crear la base de conocimiento de DQS Proveedores](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|En esta lección, creará una base de conocimiento DQS denominada **proveedores**.|60|  
|[Lección 2: Limpiar datos de proveedor con la base de conocimiento Proveedores](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|En esta lección, puede crear y ejecutar un proyecto de DQS para limpiar los datos de proveedor en un archivo de Excel mediante el **proveedores** Base de conocimiento que creó en la primera lección.|45|  
|[Lección 3: Buscar datos coincidentes para quitar duplicados de lista de proveedores](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|En esta lección, creará un proyecto de DQS para realizar la actividad de coincidencia con el fin de identificar y quitar duplicados de la lista limpia de proveedores.|45|  
|[Lección 4: Almacenar datos de proveedor en MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|En esta lección, cargará los datos de proveedor limpios y coincidentes a Master Data Services (MDS) mediante el uso de la **complemento MDS para Excel**.|45|  
|[Lección 5: Automatizar la limpieza y la búsqueda de coincidencias con SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|En esta lección, creará una solución de SSIS que limpia los datos de entrada con DQS, busca coincidencias en los datos limpios para quitar duplicados, y almacena los datos limpios y coincidentes en MDS de forma automatizada.|75|  
  
## <a name="next-steps"></a>Pasos siguientes  
 Para comenzar el tutorial, vaya a la primera lección: [lección 1: crear la Base de conocimiento de DQS proveedores](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md).  
  
  
