---
title: Conexiones de Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- sources [Integration Services], connections
- packages [Integration Services], connections
- destinations [Integration Services], connections
- tasks [Integration Services], connections
- connections [Integration Services], about connections
- connections [Integration Services]
- SQL Server Integration Services packages, connections
ms.assetid: 72f5afa3-d636-410b-9e81-2ffa27772a8c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 18575c95602f73baa959d35b176cf16220fc8e64
ms.sourcegitcommit: 59c09dbe29882cbed539229a9bc1de381a5a4471
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/11/2020
ms.locfileid: "79112160"
---
# <a name="integration-services-ssis-connections"></a>Conexiones de Integration Services (SSIS)
  Los paquetes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizan conexiones para realizar diferentes tareas y para implementar características de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:  
  
-   Conectar con almacenes de datos de origen y destino tales como archivos de texto, archivos XML, libros de Excel y bases de datos relacionales para extraer y cargar datos.  
  
-   Conectar con bases de datos relacionales que contienen datos de referencia para realizar búsquedas exactas o aproximadas.  
  
-   Conectar con bases de datos relacionales para ejecutar instrucciones SQL, tales como los comandos SELECT, DELETE e INSERT, así como procedimientos almacenados.  
  
-   Conectar con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para realizar tareas de transferencia y mantenimiento, tales como la realización de copias de seguridad de bases de datos y la transferencia de inicios de sesión.  
  
-   Escribir entradas del registro en archivos XML y de texto, y tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y configuraciones de paquete en tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Conectar con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para crear tablas de trabajo temporales que requieren algunas transformaciones para hacer su trabajo.  
  
-   Conectar con bases de datos y proyectos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para tener acceso a modelos de minería de datos, procesar cubos y dimensiones, y ejecutar el código de DDL.  
  
-   Especificar carpetas y archivos existentes o crear carpetas y archivos nuevos para utilizar en tareas y enumeradores de bucle Foreach.  
  
-   Conectar con colas de mensajes y con servidores de correo, web, Instrumental de administración de Windows (WMI) y objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SMO).  
  
 Para realizar estas conexiones, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utiliza administradores de conexión, descritos en la siguiente sección.  
  
## <a name="connection-managers"></a>Administradores de conexión  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa el administrador de conexiones como una representación lógica de una conexión. En tiempo de diseño, se establecen las propiedades de un administrador de conexiones para que describan la conexión física que crea [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cuando se ejecuta el paquete. Por ejemplo, un administrador de conexiones incluye la propiedad `ConnectionString` que se establece en el tiempo de diseño. En el tiempo de ejecución, se crea una conexión física mediante el valor de la propiedad de la cadena de conexión.  
  
 Un paquete puede usar varias instancias de un tipo de administrador de conexiones y se pueden establecer las propiedades de cada instancia. En el tiempo de ejecución, cada instancia de un tipo de administrador de conexiones crea una conexión que tiene diferentes atributos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona diferentes tipos de administradores de conexión que permiten que los paquetes se conecten a una serie de orígenes de datos y servidores:  
  
-   Se trata de administradores de conexión integrados que el programa de instalación instala al instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   Estos administradores se pueden descargar del sitio web de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
-   Puede crear su propio administrador de conexiones personalizado si los que hay disponibles no satisfacen sus necesidades.  
  
### <a name="built-in-connection-managers"></a>Administradores de conexión integrados  
 En la tabla siguiente se enumeran los tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de administrador de conexiones que proporciona.  
  
|Tipo|Descripción|Tema|  
|----------|-----------------|-----------|  
|ADO|Se conecta a los objetos de Objetos de datos ActiveX (ADO).|[Administrador de conexiones ADO](ado-connection-manager.md)|  
|ADO.NET|Se conecta a un origen de datos mediante un proveedor .NET.|[Administrador de conexiones ADO.NET](ado-net-connection-manager.md)|  
|CACHE|Lee los datos del flujo de datos o de un archivo caché (.caw) y puede guardar los datos en el archivo caché.|[Administrador de conexiones de caché](cache-connection-manager.md)|  
|DQS|Conecta a un servidor de Data Quality Services y una base de datos de Data Quality Services en el servidor.|[Administrador de conexiones de limpieza de DQS](dqs-cleansing-connection-manager.md)|  
|EXCEL|Se conecta a un archivo de libro de Excel.|[Administrador de conexiones de Excel](excel-connection-manager.md)|  
|FILE|Se conecta a un archivo o carpeta.|[administrador de conexiones de archivos](file-connection-manager.md)|  
|FLATFILE|Se conecta a los datos en un solo archivo plano.|[Administrador de conexiones de archivos planos](flat-file-connection-manager.md)|  
|FTP|Se conecta a un servidor FTP.|[FTP, administrador de conexiones](ftp-connection-manager.md)|  
|HTTP|Se conecta a un servidor web.|[HTTP, administrador de conexiones](http-connection-manager.md)|  
|MSMQ|Se conecta a una cola de mensajes.|[MSMQ, administrador de conexiones](msmq-connection-manager.md)|  
|MSOLAP100|Se conecta a una instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] un proyecto de.|[Administrador de conexiones de Analysis Services](analysis-services-connection-manager.md)|  
|MULTIFILE|Se conecta a varios archivos y carpetas.|[administrador de conexiones de varios archivos](multiple-files-connection-manager.md)|  
|MULTIFLATFILE|Se conecta a varios archivos y carpetas de datos.|[administrador de conexiones de varios archivos planos](multiple-flat-files-connection-manager.md)|  
|OLEDB|Se conecta a un origen de datos mediante un proveedor OLE DB.|[OLE DB, administrador de conexiones](ole-db-connection-manager.md)|  
|ODBC|Se conecta a un origen de datos mediante ODBC.|[ODBC, administrador de conexiones](odbc-connection-manager.md)|  
|SMOServer|Se conecta a un servidor de objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SMO).|[SMO, administrador de conexiones](smo-connection-manager.md)|  
|SMTP|Se conecta a un servidor de correo SMTP.|[Administrador de conexiones SMTP](smtp-connection-manager.md)|  
|SQLMOBILE|Se conecta a una base de datos Compact [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Administrador de conexiones con SQL Server Compact Edition](sql-server-compact-edition-connection-manager.md)|  
|WMI|Se conecta a un servidor y especifica el ámbito de la administración del Instrumental de administración de Windows (WMI) en el servidor.|[Administrador de conexiones WMI](wmi-connection-manager.md)|  
  
### <a name="connection-managers-available-for-download"></a>Administradores de conexión disponibles para descarga  
 En la tabla siguiente se indican otros tipos de administradores de conexión que puede descargar del sitio web de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
> [!IMPORTANT]  
>  Los administradores de conexiones incluidos en la tabla siguiente solamente funcionan con [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] y [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)].  
  
|Tipo|Descripción|Tema|  
|----------|-----------------|-----------|  
|ORACLE|Se conecta a un \<servidor de> de información de versión de Oracle.|El administrador de conexiones de Oracle es el componente de administrador de conexiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Oracle de Attunity. 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Oracle de Attunity incluye también un origen y un destino. Para obtener más información, vea la página de descarga de [Conectores de Microsoft para Oracle y Teradata de Attunity](https://go.microsoft.com/fwlink/?LinkId=251526).|  
|SAPBI|Se conecta a un sistema SAP NetWeaver BI versión 7.|El administrador de conexiones de SAP BI es el componente de administrador de conexiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para SAP BI. 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para SAP BI incluye también un origen y un destino. Para obtener más información, vea la página de descarga, [Feature Pack de Microsoft SQL Server 2008](https://www.microsoft.com/download/details.aspx?id=30440).|  
|TERADATA|Se conecta a un \<servidor de> de información de versión de Teradata.|El administrador de conexiones de Teradata es el componente de administrador de conexiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Teradata de Attunity. 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Teradata de Attunity incluye también un origen y un destino. Para obtener más información, vea la página de descarga de [Conectores de Microsoft para Oracle y Teradata de Attunity](https://go.microsoft.com/fwlink/?LinkId=251526).|  
  
### <a name="custom-connection-managers"></a>Administradores de conexión personalizados  
 Puede crear también administradores de conexión personalizados. Para obtener más información, vea [Developing a Custom Connection Manager](../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener detalles sobre cómo agregar o eliminar un administrador de conexiones en un paquete, vea [Agregar, eliminar o compartir un administrador de conexiones en un paquete](../add-delete-or-share-a-connection-manager-in-a-package.md).  
  
 Para obtener detalles sobre cómo establecer las propiedades de un administrador de conexiones en un paquete, vea [Establecer las propiedades de un administrador de conexiones](../set-the-properties-of-a-connection-manager.md).  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Vídeo, [Sacar provecho de Microsoft Attunity Connector for Oracle para mejorar el rendimiento de los paquetes](https://technet.microsoft.com/sqlserver/gg598963.aspx), en technet.microsoft.com  
  
-   Artículos de Wiki, [Conectividad de SSIS](https://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity), en social.technet.microsoft.com  
  
-   Entrada de blog, [Conectar con MySQL desde SSIS](https://go.microsoft.com/fwlink/?LinkId=217669), en blogs.msdn.com.  
  
-   Artículo técnico [Extraer y cargar datos de SharePoint de SQL Server Integration Services](https://go.microsoft.com/fwlink/?LinkId=247826), en msdn.microsoft.com.  
  
-   El artículo técnico [You get "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" error message when using Oracle connection manager in SSIS](https://go.microsoft.com/fwlink/?LinkId=233696) (Aparece el mensaje de error "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" al usar el administrador de conexiones de Oracle en SSIS), en support.microsoft.com.  
  
  
