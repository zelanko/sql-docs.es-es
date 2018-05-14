---
title: Conexiones de Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.asvs.connectionmanager.f1
- sql13.dts.designer.adddtsconnection.f1
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
caps.latest.revision: 92
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c6ece524c8ee7565b692902b5f8d1e7dbcbd5db6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="integration-services-ssis-connections"></a>Conexiones de Integration Services (SSIS)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizan conexiones para realizar diferentes tareas y para implementar características de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
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
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa el administrador de conexiones como una representación lógica de una conexión. En tiempo de diseño, se establecen las propiedades de un administrador de conexiones para que describan la conexión física que crea [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cuando se ejecuta el paquete. Por ejemplo, un administrador de conexiones incluye la propiedad **ConnectionString** que se establece en el tiempo de diseño. En el tiempo de ejecución, se crea una conexión física mediante el valor de la propiedad de la cadena de conexión.  
  
 Un paquete puede usar varias instancias de un tipo de administrador de conexiones y se pueden establecer las propiedades de cada instancia. En el tiempo de ejecución, cada instancia de un tipo de administrador de conexiones crea una conexión que tiene diferentes atributos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona diferentes tipos de administradores de conexión que permiten que los paquetes se conecten a una serie de orígenes de datos y servidores:  
  
-   Se trata de administradores de conexión integrados que el programa de instalación instala al instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   Estos administradores se pueden descargar del sitio web de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
-   Puede crear su propio administrador de conexiones personalizado si los que hay disponibles no satisfacen sus necesidades.  

### <a name="package-level-and-project-level-connection-managers"></a>Administradores de conexiones de nivel de paquete y de nivel de proyecto
Se puede crear un administrador de conexiones en el nivel de paquete o en el nivel de proyecto. El administrador de conexiones creado en el nivel de proyecto está disponible para todos los paquetes del proyecto. En tanto que el administrador de conexiones creado en el nivel de paquete está disponible para ese paquete específico.  
  
 Utilice los administradores de conexiones que se crean en el nivel de proyecto en lugar de orígenes de datos, para compartir conexiones a orígenes. Para agregar un administrador de conexiones en el nivel de proyecto, el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] debe utilizar el modelo de implementación del proyecto. Cuando se configura un proyecto de usar este modelo, la carpeta **Administradores de conexiones** aparece en el **Explorador de soluciones**y la carpeta **Orígenes de datos** se quita del **Explorador de soluciones**.  
  
> [!NOTE]  
>  Si desea utilizar orígenes de datos en el paquete, debe convertir el proyecto en el modelo de implementación de paquetes.  
>   
>  Para obtener más información sobre los dos modelos y sobre cómo convertir un proyecto en un modelo de implementación de proyectos, vea [Implementación de proyectos y paquetes de Integration Services (SSIS)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).

### <a name="built-in-connection-managers"></a>Administradores de conexión integrados  
 En la tabla siguiente se indican los tipos de administradores de conexión proporcionados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
|Tipo|Description|Tema|  
|----------|-----------------|-----------|  
|ADO|Se conecta a los objetos de Objetos de datos ActiveX (ADO).|[Administrador de conexiones ADO](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|Se conecta a un origen de datos mediante un proveedor .NET.|[Administrador de conexiones ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|CACHE|Lee los datos del flujo de datos o de un archivo caché (.caw) y puede guardar los datos en el archivo caché.|[Administrador de conexiones de caché](../../integration-services/connection-manager/cache-connection-manager.md)|  
|DQS|Conecta a un servidor de Data Quality Services y una base de datos de Data Quality Services en el servidor.|[Administrador de conexiones de Limpieza de DQS](../../integration-services/connection-manager/dqs-cleansing-connection-manager.md)|  
|EXCEL|Se conecta a un archivo de libro de Excel.|[Administrador de conexiones con Excel](../../integration-services/connection-manager/excel-connection-manager.md)|  
|FILE|Se conecta a un archivo o carpeta.|[Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md)|  
|FLATFILE|Se conecta a los datos en un solo archivo plano.|[Administrador de conexiones de archivos planos](../../integration-services/connection-manager/flat-file-connection-manager.md)|  
|FTP|Se conecta a un servidor FTP.|[Administrador de conexiones FTP](../../integration-services/connection-manager/ftp-connection-manager.md)|  
|HTTP|Se conecta a un servidor web.|[Administrador de conexiones HTTP](../../integration-services/connection-manager/http-connection-manager.md)|  
|MSMQ|Se conecta a una cola de mensajes.|[Administrador de conexiones MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md)|  
|MSOLAP100|Se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|[Administrador de conexiones de Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)|  
|MULTIFILE|Se conecta a varios archivos y carpetas.|[Administrador de conexiones de varios archivos](../../integration-services/connection-manager/multiple-files-connection-manager.md)|  
|MULTIFLATFILE|Se conecta a varios archivos y carpetas de datos.|[Administrador de conexiones de varios archivos planos](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|  
|OLEDB|Se conecta a un origen de datos mediante un proveedor OLE DB.|[Administrador de conexiones OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|Se conecta a un origen de datos mediante ODBC.|[Administrador de conexiones ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|SMOServer|Se conecta a un servidor de objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SMO).|[Administrador de conexiones SMO](../../integration-services/connection-manager/smo-connection-manager.md)|  
|SMTP|Se conecta a un servidor de correo SMTP.|[Administrador de conexiones SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)|  
|SQLMOBILE|Se conecta a una base de datos Compact [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Administrador de conexiones con SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
|WMI|Se conecta a un servidor y especifica el ámbito de la administración del Instrumental de administración de Windows (WMI) en el servidor.|[Administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager.md)|  
  
### <a name="connection-managers-available-for-download"></a>Administradores de conexión disponibles para descarga  
 En la tabla siguiente se indican otros tipos de administradores de conexión que puede descargar del sitio web de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
> [!IMPORTANT]  
>  Los administradores de conexiones incluidos en la tabla siguiente solamente funcionan con [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] y [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)].  
  
|Tipo|Description|Tema|  
|----------|-----------------|-----------|  
|ORACLE|Se conecta a un servidor de Oracle \<información de versión\>.|El administrador de conexiones de Oracle es el componente de administrador de conexiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Oracle de Attunity. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Oracle de Attunity incluye también un origen y un destino. Para obtener más información, vea la página de descarga de [Conectores de Microsoft para Oracle y Teradata de Attunity](http://go.microsoft.com/fwlink/?LinkId=251526).|  
|SAPBI|Se conecta a un sistema SAP NetWeaver BI versión 7.|El administrador de conexiones de SAP BI es el componente de administrador de conexiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para SAP BI. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para SAP BI incluye también un origen y un destino. Para obtener más información, vea la página de descarga, [Feature Pack de Microsoft SQL Server 2008](http://go.microsoft.com/fwlink/?LinkId=262016).|  
|TERADATA|Se conecta a un servidor de Teradata \<información de versión\>.|El administrador de conexiones de Teradata es el componente de administrador de conexiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Teradata de Attunity. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector para Teradata de Attunity incluye también un origen y un destino. Para obtener más información, vea la página de descarga de [Conectores de Microsoft para Oracle y Teradata de Attunity](http://go.microsoft.com/fwlink/?LinkId=251526).|  
  
### <a name="custom-connection-managers"></a>Administradores de conexión personalizados  
 Puede crear también administradores de conexión personalizados. Para obtener más información, vea [Developing a Custom Connection Manager](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md).  
  
## <a name="create-connection-managers"></a>Crear administradores de conexiones
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye una serie de administradores de conexión adaptados a las necesidades de las tareas que se conectan a diferentes tipos de servidores y orígenes de datos. Los administradores de conexión son utilizados por los componentes de flujo de datos, que extraen y cargan datos en diferentes tipos de almacenes de datos, y por los proveedores de registro que escriben registros en un servidor, tabla o archivo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por ejemplo, un paquete con una tarea Enviar correo usa un tipo de administrador de conexiones SMTP para conectarse a un servidor de Protocolo simple de transferencia de correo (SMTP). Un paquete con una tarea Ejecutar SQL puede usar un administrador de conexiones OLE DB para conectarse a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para más información, vea [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 Para crear y configurar automáticamente los administradores de conexiones al crear un paquete nuevo, puede utilizar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este asistente también ayuda a crear y configurar los orígenes y destinos que utilizan los administradores de conexiones. Para más información, consulte [Create Packages in SQL Server Data Tools](../../integration-services/create-packages-in-sql-server-data-tools.md).  
  
 Para crear manualmente un nuevo administrador de conexiones y agregarlo a un paquete existente, se usa el área **Administradores de conexiones** que aparece en las pestañas **Flujo de control**, **Flujo de datos**y **Controladores de eventos** del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Desde el área **Administrador de conexiones** , se elige el tipo de administrador de conexiones que se desea crear y luego se establecen las propiedades del administrador de conexiones mediante un cuadro de diálogo proporcionado por el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Para obtener más información, vea la sección "Usar el área Administradores de conexiones" más adelante en este tema.  
  
 Una vez agregado el administrador de conexiones a un paquete, puede usarlo en tareas, contenedores de bucles Foreach, orígenes, transformaciones y destinos. Para obtener más información, vea [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md), [Contenedor Foreach Loop](../../integration-services/control-flow/foreach-loop-container.md) y [Flujo de datos](../../integration-services/data-flow/data-flow.md).  
  
### <a name="using-the-connection-managers-area"></a>Uso del área Administradores de conexión  
 Puede crear administradores de conexión mientras las pestañas **Flujo de control**, **Flujo de datos**o **Controladores de eventos** del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] están activas.  
  
 El siguiente diagrama muestra el área **Administradores de conexión** en la pestaña **Flujo de control** del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 ![Captura de pantalla del diseñador de flujo de control con paquete](../../integration-services/connection-manager/media/samplecontrolflow.gif "Screenshot of control flow designer with package")    
  
### <a name="32-bit-and-64-bit-providers-for-connection-managers"></a>Proveedores de 32 y 64 bits para administradores de conexión  
 Muchos de los proveedores que utilizan los administradores de conexión están disponibles en versiones de 32 y 64 bits. El entorno de diseño de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es un entorno de 32 bits; solamente verá proveedores de 32 bits al diseñar un paquete. Por lo tanto, solo se puede configurar un administrador de conexiones para que utilice un proveedor de 64 bits específico si también está instalada la versión de 32 bits del mismo proveedor.  
  
 En tiempo de ejecución, se utiliza la versión correcta, independientemente de que haya especificado la versión de 32 bits del proveedor en tiempo de diseño. Se puede ejecutar la versión de 64 bits del proveedor aun cuando el paquete se ejecuta en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
  Las dos versiones del proveedor tienen el mismo identificador. Para especificar si el tiempo de ejecución de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa una versión de 64 bits disponible del proveedor, establezca la propiedad Run64BitRuntime del proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Si la propiedad Run64BitRuntime se establece en **true**, el tiempo de ejecución busca y usa el proveedor de 64 bits; si Run64BitRuntime se establece en **false**, el tiempo de ejecución busca y usa el proveedor de 32 bits. Para más información sobre las propiedades que se pueden establecer en proyectos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Entornos de Studio e Integration Services (SSIS)](https://msdn.microsoft.com/library/ms140028.aspx).   

## <a name="add-a-connection-manager"></a>Agregar un administrador de conexiones
###  <a name="wizard"></a> Agregar un administrador de conexiones al crear un paquete  
  
-   Use el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Además de crear y configurar un administrador de conexiones, el asistente también ayuda a crear y configurar los orígenes y destinos que utilizan el administrador de conexiones. Para más información, consulte [Create Packages in SQL Server Data Tools](../../integration-services/create-packages-in-sql-server-data-tools.md).  
  
###  <a name="package"></a> Agregar un administrador de conexiones a un paquete existente  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en la pestaña **Flujo de control** , **Flujo de datos** o **Controlador de eventos** para que esté disponible el área **Administradores de conexiones** .  
  
4.  Haga clic con el botón derecho en cualquier lugar del área **Administradores de conexiones** y, después, siga uno de estos procedimientos:  
  
    -   Haga clic en el tipo de administrador de conexiones que desee agregar al paquete.  
  
         O bien  
  
    -   Si no aparece el tipo que desea agregar, haga clic en **Nueva conexión** para abrir el cuadro de diálogo **Agregar administrador de conexiones SSIS** , seleccione un tipo de administrador de conexiones y haga clic en **Aceptar**.  
  
     Se abrirá el cuadro de diálogo personalizado para el tipo de administrador de conexiones seleccionado. Para obtener más información acerca de los tipos de administradores de conexiones y las opciones disponibles, vea la siguiente tabla de opciones.  
  
    |Administrador de conexiones|Opciones|  
    |------------------------|-------------|  
    |[Administrador de conexiones ADO](../../integration-services/connection-manager/ado-connection-manager.md)|[Configurar el administrador de conexiones OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Administrador de conexiones ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|[Configurar el administrador de conexiones ADO.NET](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Administrador de conexiones de Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones con Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Administrador de conexiones de Excel](../../integration-services/connection-manager/excel-connection-manager.md)|[Editor del administrador de conexiones con Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md)|[Editor del administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[Administrador de conexiones de varios archivos](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones de archivos](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Administrador de conexiones de archivos planos](../../integration-services/connection-manager/flat-file-connection-manager.md)|[Editor del administrador de conexiones de archivos planos &#40;página General&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Columnas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Avanzadas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Vista previa&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[Administrador de conexiones de varios archivos planos](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[Editor del administrador de conexiones de varios archivos planos &#40;página General&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Columnas&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Avanzadas&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Vista previa&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Administrador de conexiones FTP](../../integration-services/connection-manager/ftp-connection-manager.md)|[Editor del administrador de conexiones FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[Administrador de conexiones HTTP](../../integration-services/connection-manager/http-connection-manager.md)|[Editor del administrador de conexiones HTTP &#40;página Servidor&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [Editor del administrador de conexiones HTTP &#40;página Proxy&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[Administrador de conexiones MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md)|[Editor del administrador de conexiones MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[Administrador de conexiones ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|[Referencia de la interfaz de usuario del administrador de conexiones ODBC](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[Administrador de conexiones OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|[Configurar el administrador de conexiones OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Administrador de conexiones SMO](../../integration-services/connection-manager/smo-connection-manager.md)|[Editor del administrador de conexiones SMO](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[Administrador de conexiones SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)|[Editor del administrador de conexiones SMTP](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[Administrador de conexiones con SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor del administrador de conexiones con SQL Server Compact Edition &#40;página Conexión&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor del administrador de conexiones con SQL Server Compact Edition &#40;página Todo&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager.md)|[Editor del administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
     En el área **Administradores de conexiones** se muestra el administrador de conexiones agregado.  
  
5.  Opcionalmente, puede hacer clic con el botón derecho en el administrador de conexiones, hacer clic en **Cambiar nombre**y, después, modificar el nombre predeterminado del administrador de conexiones.  
  
6.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** en el menú **Archivo** .  
  
###  <a name="project"></a> Agregar un administrador de conexiones en el nivel de proyecto  
  
1.  Abra el proyecto de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Administradores de conexiones**y, después, en **Nuevo administrador de conexiones**.  
  
3.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS** , seleccione el tipo de administrador de conexiones y, a continuación, haga clic en **Agregar**.  
  
     Se abrirá el cuadro de diálogo personalizado para el tipo de administrador de conexiones seleccionado. Para obtener más información acerca de los tipos de administradores de conexiones y las opciones disponibles, vea la siguiente tabla de opciones.  
  
    |Administrador de conexiones|Opciones|  
    |------------------------|-------------|  
    |[Administrador de conexiones ADO](../../integration-services/connection-manager/ado-connection-manager.md)|[Configurar el administrador de conexiones OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Administrador de conexiones ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|[Configurar el administrador de conexiones ADO.NET](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Administrador de conexiones de Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones con Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Administrador de conexiones de Excel](../../integration-services/connection-manager/excel-connection-manager.md)|[Editor del administrador de conexiones con Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md)|[Editor del administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[Administrador de conexiones de varios archivos](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones de archivos](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Administrador de conexiones de archivos planos](../../integration-services/connection-manager/flat-file-connection-manager.md)|[Editor del administrador de conexiones de archivos planos &#40;página General&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Columnas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Avanzadas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Vista previa&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[Administrador de conexiones de varios archivos planos](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[Editor del administrador de conexiones de varios archivos planos &#40;página General&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Columnas&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Avanzadas&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Vista previa&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Administrador de conexiones FTP](../../integration-services/connection-manager/ftp-connection-manager.md)|[Editor del administrador de conexiones FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[Administrador de conexiones HTTP](../../integration-services/connection-manager/http-connection-manager.md)|[Editor del administrador de conexiones HTTP &#40;página Servidor&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [Editor del administrador de conexiones HTTP &#40;página Proxy&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[Administrador de conexiones MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md)|[Editor del administrador de conexiones MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[Administrador de conexiones ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|[Referencia de la interfaz de usuario del administrador de conexiones ODBC](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[Administrador de conexiones OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|[Configurar el administrador de conexiones OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Administrador de conexiones SMO](../../integration-services/connection-manager/smo-connection-manager.md)|[Editor del administrador de conexiones SMO](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[Administrador de conexiones SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)|[Editor del administrador de conexiones SMTP](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[Administrador de conexiones con SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor del administrador de conexiones con SQL Server Compact Edition &#40;página Conexión&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor del administrador de conexiones con SQL Server Compact Edition &#40;página Todo&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager.md)|[Editor del administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
     El administrador de conexiones que agregó aparecerá en el nodo de **Administradores de conexiones** en el **Explorador de soluciones**. También aparecerá en la pestaña **Administradores de conexiones** de la ventana **Diseñador SSIS** para todos los paquetes del proyecto. El nombre del administrador de conexiones de esta pestaña tendrá el prefijo **(proyecto)** para distinguir este administrador de conexiones de nivel de proyecto de los administradores de conexiones de nivel de paquete.  
  
4.  Si quiere, haga clic con el botón derecho en el administrador de conexiones de la ventana **Explorador de soluciones** en el nodo **Administradores de conexiones** o en la pestaña **Administradores de conexiones** de la ventana **Diseñador SSIS** , haga clic en **Cambiar nombre**y, después, modifique el nombre predeterminado del administrador de conexiones.  
  
    > [!NOTE]  
    >  En la pestaña **Administradores de conexiones** de la ventana **Diseñador SSIS** , no podrá sobrescribir el prefijo **(proyecto)** del nombre del administrador de conexiones. es así por diseño.  

### <a name="add-ssis-connection-manager-dialog-box"></a>Cuadro de diálogo Agregar administrador de conexiones SSIS
Utilice el cuadro de diálogo **Agregar administrador de conexiones SSIS** para seleccionar el tipo de conexión que se va a agregar a un paquete.  
  
 Para obtener más información sobre los administradores de conexión, vea [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
#### <a name="options"></a>Opciones  
 **Tipo de administrador de conexiones**  
 Seleccione un tipo de conexión y haga clic en **Agregar**, o bien haga doble clic en un tipo de conexión para especificar las propiedades de conexión con el editor para cada tipo de conexión.  
  
 **Agregar**  
 Especifique las propiedades de conexión mediante el editor para cada tipo de conexión.  
   
##  <a name="parameter"></a> Crear un parámetro para una propiedad de administrador de conexiones  
  
1.  En el área de **Administradores de conexiones** , haga clic con el botón derecho en el administrador de conexiones para el que quiere crear un parámetro y haga clic en **Parametrizar**.  
  
2.  Configure los valores de parámetro en el cuadro de diálogo **Parametrizar** . Para más información, consulte [Parameterize Dialog Box](http://msdn.microsoft.com/library/fac02b6d-d247-447a-8940-e8700c7ac350).  

## <a name="delete-a-connection-manager"></a>Eliminar un administrador de conexiones 
###  <a name="DeletePackageLevel"></a> Eliminar un administrador de conexiones de un paquete  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en la pestaña **Flujo de control** , **Flujo de datos** o **Controlador de eventos** para que esté disponible el área **Administradores de conexiones** .  
  
4.  Haga clic con el botón derecho en el administrador de conexiones que quiera eliminar y haga clic en **Eliminar**.  
  
     Si elimina un administrador de conexiones que use un elemento de paquete, como una tarea Ejecutar SQL o un origen de OLE DB, experimentará los resultados siguientes:  
  
    -   Un icono de error aparece en el elemento de paquete que usaba el administrador de conexiones eliminado.  
  
    -   El paquete no puede validarse.  
  
    -   El paquete no se puede ejecutar.  
  
5.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
###  <a name="DeleteProjectLevel"></a> Eliminar un administrador de conexiones compartido (administrador de conexiones de nivel de proyecto)  
  
1.  Para eliminar un administrador de conexiones de nivel de proyecto, haga clic con el botón derecho en el administrador de conexiones en el nodo **Administradores de conexiones** de la ventana del **Explorador de soluciones** y haga clic en **Eliminar**. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] muestra el siguiente mensaje de advertencia:  
  
    > [!WARNING]  
    >  Si elimina un administrador de conexiones del proyecto, los paquetes que utilizan el administrador de conexiones no pueden ejecutarse. No es posible deshacer esta acción. ¿Desea eliminar el administrador de conexiones?  
  
2.  Haga clic en Aceptar para eliminar el administrador de conexiones o en Cancelar para mantenerlo.  
  
    > [!NOTE]  
    >  También puede eliminar un administrador de conexiones de nivel de proyecto en la pestaña **Administrador de conexiones** de la ventana **Diseñador SSIS** abierta para los paquetes del proyecto. Para ello, haga clic con el botón derecho en el administrador de conexiones en la pestaña y después haga clic en **Eliminar**. 
    
## <a name="set-the-properties-of-a-connection-manager"></a>Establecer las propiedades de un administrador de conexiones
Todos los administradores de conexión se pueden configurar en la ventana **Propiedades** .  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] también proporciona cuadros de diálogo personalizados para modificar los distintos tipos de administradores de conexiones en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. El cuadro de diálogo tiene un conjunto de opciones diferente para cada tipo de administrador de conexiones.  
  
### <a name="modify-a-connection-manager-using-the-properties-window"></a>Modificar un administrador de conexiones mediante la ventana Propiedades  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador SSIS, haga clic en la pestaña **Flujo de control** , **Flujo de datos** o **Controlador de eventos** para que esté disponible el área **Administradores de conexión** .  
  
4.  Haga clic con el botón derecho en el administrador de conexiones y haga clic en **Propiedades**.  
  
5.  En la ventana **Propiedades** , modifique los valores de las propiedades. La ventana **Propiedades** proporciona acceso a algunas propiedades que no se pueden configurar en el editor estándar para un administrador de conexiones.  
  
6.  Haga clic en **Aceptar**.  
  
7.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
### <a name="modify-a-connection-manager-using-a-connection-manager-dialog-box"></a>Modificar un administrador de conexiones mediante el cuadro de diálogo Administrador de conexiones  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en la pestaña **Flujo de control** , **Flujo de datos** o **Controlador de eventos** para que esté disponible el área **Administradores de conexiones** .  
  
4.  En el área **Administradores de conexiones** , haga doble clic en el administrador de conexiones para abrir el cuadro de diálogo **Administrador de conexiones** . Para obtener información acerca de tipos específicos de administradores de conexión y de las opciones disponibles para cada tipo, vea la tabla siguiente.  
  
    |Administrador de conexiones|Opciones|  
    |------------------------|-------------|  
    |[Administrador de conexiones ADO](../../integration-services/connection-manager/ado-connection-manager.md)|[Configurar el administrador de conexiones OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Administrador de conexiones ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|[Configurar el administrador de conexiones ADO.NET](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Administrador de conexiones de Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones con Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Administrador de conexiones de Excel](../../integration-services/connection-manager/excel-connection-manager.md)|[Editor del administrador de conexiones con Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md)|[Editor del administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[Administrador de conexiones de varios archivos](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones de archivos](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Administrador de conexiones de archivos planos](../../integration-services/connection-manager/flat-file-connection-manager.md)|[Editor del administrador de conexiones de archivos planos &#40;página General&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Columnas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Avanzadas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Vista previa&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[Administrador de conexiones de varios archivos planos](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[Editor del administrador de conexiones de varios archivos planos &#40;página General&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Columnas&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Avanzadas&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Vista previa&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Administrador de conexiones FTP](../../integration-services/connection-manager/ftp-connection-manager.md)|[Editor del administrador de conexiones FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[Administrador de conexiones HTTP](../../integration-services/connection-manager/http-connection-manager.md)|[Editor del administrador de conexiones HTTP &#40;página Servidor&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [Editor del administrador de conexiones HTTP &#40;página Proxy&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[Administrador de conexiones MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md)|[Editor del administrador de conexiones MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[Administrador de conexiones ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|[Referencia de la interfaz de usuario del administrador de conexiones ODBC](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[Administrador de conexiones OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|[Configurar el administrador de conexiones OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Administrador de conexiones SMO](../../integration-services/connection-manager/smo-connection-manager.md)|[Editor del administrador de conexiones SMO](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[Administrador de conexiones SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)|[Editor del administrador de conexiones SMTP](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[Administrador de conexiones con SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor del administrador de conexiones con SQL Server Compact Edition &#40;página Conexión&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor del administrador de conexiones con SQL Server Compact Edition &#40;página Todo&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager.md)|[Editor del administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
5.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  

## <a name="related-content"></a>Contenido relacionado  
  
-   Vídeo, [Sacar provecho de Microsoft Attunity Connector for Oracle para mejorar el rendimiento de los paquetes](http://technet.microsoft.com/sqlserver/gg598963.aspx), en technet.microsoft.com  
  
-   Artículos de Wiki, [Conectividad de SSIS](http://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity), en social.technet.microsoft.com  
  
-   Entrada de blog, [Conectar con MySQL desde SSIS](http://go.microsoft.com/fwlink/?LinkId=217669), en blogs.msdn.com.  
  
-   Artículo técnico [Extraer y cargar datos de SharePoint de SQL Server Integration Services](http://go.microsoft.com/fwlink/?LinkId=247826), en msdn.microsoft.com.  
  
-   El artículo técnico [You get "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" error message when using Oracle connection manager in SSIS](http://go.microsoft.com/fwlink/?LinkId=233696)(Aparece el mensaje de error "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" al usar el administrador de conexiones de Oracle en SSIS), en support.microsoft.com.  
  
  
