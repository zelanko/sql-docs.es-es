---
title: "Crear una base de datos del servidor de informes (Administrador de configuración de SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 05/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], databases
- report server database
- databases [Reporting Services], creating
ms.assetid: 8a3a6ffe-4001-46be-8548-94532550f6a5
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 526abc46fe3b7fc3f923c29f4b4857b06f55a37c
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---

# <a name="create-a-report-server-database"></a>Crear una base de datos del servidor de informes

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**Modo nativo** usa dos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y objetos de metadatos del servidor de informes de bases de datos relacionales para almacenar. Una base de datos se utiliza para el almacenamiento principal y la otra para almacenar datos temporales. Las bases de datos se crean juntas y se enlazan mediante el nombre. Con una instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , las bases de datos tienen los nombres **reportserver** y **reportservertempdb**. Colectivamente, ambas se conocen como "base de datos del servidor de informes" o "catálogo del servidor de informes".

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**El modo de SharePoint** incluye una tercera base de datos que se usa para los metadatos de las alertas de datos. Las tres bases de datos se crean para cada aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y los nombres de base de datos incluyen de manera predeterminada un GUID que representa la aplicación de servicio. A continuación, se indican nombres de ejemplo de las tres bases de datos en modo de SharePoint:

-   ReportingService_90a9f37075544f22953c4a62e4a9f370  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370TempDB  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370_Alerting  
  
> [!IMPORTANT]  
>  No escriba aplicaciones que ejecuten consultas en la base de datos del servidor de informes. La base de datos del servidor de informes no es un esquema público. La estructura de tablas puede cambiar de una versión a la siguiente. Si escribe una aplicación que necesita acceso a la base de datos del servidor de informes, utilice las API de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para obtener acceso.  
>   
>  La excepción son las vistas del registro de ejecución. Para obtener más información, vea [Registro de ejecución del servidor de informes y la vista ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
## <a name="ways-to-create-the-report-server-database"></a>Métodos para crear la base de datos del servidor de informes  
 **Modo nativo:** puede crear la base de datos del servidor de informes de modo nativo de las formas siguientes:  
  
-   Automáticamente: usar el Asistente para la instalación de SQL Server, si elige la opción de instalación de configuración predeterminada. En el Asistente para la instalación de SQL Server, es **Instalar y configurar** en la página Opciones de instalación del servidor de informes. Si elige la opción **Solo instalar** , debe usar el Administrador de configuración de Reporting Services para crear la base de datos.  
  
-   Manualmente: use el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Debe crear la base de datos del servidor de informes manualmente si está usando un [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] remoto para hospedarla. Para obtener más información, vea [Crear una base de datos del servidor de informes de modo nativo &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
 **Modo de SharePoint:** la página Opciones de instalación del servidor de informes solo tiene una opción para el modo de SharePoint, **Solo instalar**. Esta opción instala todos los archivos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y el servicio compartido de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . El paso siguiente consiste en crear al menos una aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de una de las siguientes formas:  
  
-   Use Administración central de SharePoint para crear una aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, vea la sección "Aplicación de servicio" de [Step 3: Create a Reporting Services Service Application](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_create_serrviceapplication).  
  
-   Use cmdlets de PowerShell de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para crear una aplicación de servicio y las bases de datos del servidor de informes. Para obtener más información, vea el ejemplo para crear aplicaciones de servicio en el tema [Cmdlets de PowerShell para el modo de SharePoint de Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
## <a name="database-server-version-requirements"></a>Requisitos de versión del servidor de base de datos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se usa para hospedar las bases de datos del servidor de informes. La instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] puede ser local o remota. A continuación, se indican las versiones admitidas de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que se pueden usar para hospedar las bases de datos del servidor de informes:  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 Para crear la base de datos del servidor de informes en un equipo remoto es preciso que configure la conexión para usar una cuenta de usuario de dominio o una cuenta de servicio que tenga acceso a la red. Si decide utilizar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remota, considere detenidamente qué credenciales debe utilizar el servidor de informes para conectarse a la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
> [!IMPORTANT]  
>  El servidor de informes y la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la base de datos del servidor de informes pueden estar en dominios diferentes. Para la implementación en Internet, la práctica más común es utilizar un servidor que esté detrás de un firewall. Si va a configurar un servidor de informes para el acceso a Internet, utilice las credenciales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que esté detrás del firewall y utilice IPSEC para proteger la conexión.  
  
## <a name="database-server-edition-requirements"></a>Requisitos de edición del servidor de base de datos  
 Cuando cree una base de datos del servidor de informes, tenga en cuenta que no se pueden usar todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hospedarla. Para obtener más información, vea la sección "Requisitos de edición de servidor de la base de datos del servidor de informes" de [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  

## <a name="next-steps"></a>Pasos siguientes

[Administrador de configuración de Reporting Services](http://msdn.microsoft.com/en-us/63519ef4-e68a-42fb-9cf7-31228ea4e434)  

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
