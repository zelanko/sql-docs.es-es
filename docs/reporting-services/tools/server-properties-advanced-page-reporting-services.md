---
title: "Propiedades del servidor (página de opciones avanzadas) - Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.reportserver.serverproperties.advanced.f1
ms.assetid: 07b78a84-a6aa-4502-861d-349720ef790e
caps.latest.revision: "18"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 80f962efa995f8f6a5d422f8b470826acddbab58
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="server-properties-advanced-page---reporting-services"></a>Propiedades del servidor (página de opciones avanzadas) - Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Use esta página para establecer las propiedades del sistema en el servidor de informes. Hay varias maneras de establecer las propiedades del sistema. Esta herramienta proporciona una interfaz de usuario gráfica para que pueda establecer propiedades sin tener que escribir código.

Para abrir esta página, inicie SQL Server Management Studio, conéctese a una instancia del servidor de informes, haga clic con el botón derecho en el nombre del servidor de informes y seleccione **Propiedades**. Seleccione **Opciones avanzadas** para abrir esta página.

## <a name="options"></a>Opciones

**EnableMyReports**  
Indica si la característica Mis informes está habilitada. El valor **true** indica que la característica está habilitada.  

**MyReportsRole**  
El nombre del rol que se usa al crear directivas de seguridad en las carpetas Mis informes del usuario. El valor predeterminado es **My Reports Role**.  

**EnableClientPrinting**  
Determina si el control ActiveX RSClientPrint está disponible para descargarlo del servidor de informes. Los valores válidos son **true** y **false**. El valor predeterminado es **true**. Para más información sobre opciones de configuración adicionales necesarias para este control, vea [Habilitar y deshabilitar la impresión del lado cliente para Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  

**EnableExecutionLogging**  
Indica si el registro de ejecución de informes está habilitado. El valor predeterminado es **true**. Para más información sobre el registro de ejecución del servidor de informes, vea [Registro de ejecución del servidor de informes y la vista ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  

**ExecutionLogDaysKept**  
Número de días que mantener la información de ejecución de informes en el registro de ejecución. Entre los valores válidos de esta propiedad están el rango **-1** - **2**,**147**,**483**y**647**. Si el valor es **1** , no se eliminan las entradas de la tabla del registro de ejecución. El valor predeterminado es **60**.  

> [!NOTE] 
> Si establece un valor de **0**, se *eliminarán* todas las entradas del registro de ejecución. Un valor de **-1** conservará las entradas del registro de ejecución y no se eliminarán.

**SessionTimeout**  
El período, en segundos, que una sesión permanece activa. El valor predeterminado es **600**.  

**SharePointIntegratedMode**  
Ésta es una propiedad de solo lectura que indica el modo de servidor. Si este valor es False, el servidor de informes se ejecuta en modo nativo.  

**SiteName**  
El nombre del sitio del servidor de informes mostrado en el título de la página del portal web. El valor predeterminado es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Esta propiedad puede ser una cadena vacía. La longitud máxima es de 8000 caracteres.  

**StoredParametersLifetime**  
Especifica el número máximo de días que un parámetro almacenado puede estar almacenado. Los valores válidos **-1**y de **+1** a **2 147 483 647**. El valor predeterminado es **180** días.  

**StoredParametersThreshold**  
Especifica el número máximo de valores de parámetro que se pueden almacenar por el servidor de informes. Los valores válidos **-1**y de **+1** a **2 147 483 647**. El valor predeterminado es **1500**.  

**UseSessionCookies**  
Indica si el servidor de informes debería usar cookies de sesión al comunicarse con exploradores cliente. El valor predeterminado es **true**.  

**ExternalImagesTimeout**  
Determina el período de tiempo dentro del cual se debe recuperar un archivo de imagen externo antes de que se agote el tiempo de espera de la conexión. El valor predeterminado es **600** segundos.  

**SnapshotCompression**  
Define la manera en la que se comprimen las instantáneas. El valor predeterminado es **SQL**. Los valores válidos son los siguientes:

|Valores|Description|
|---------|---------|
|**SQL**|Las instantáneas se comprimen cuando se almacenan en la base de datos del servidor de informes. Éste es el comportamiento actual.|
|**Ninguno**|Las instantáneas no se comprimen.|
|**Todos**|Las instantáneas se comprimen para todas las opciones de almacenamiento, lo que incluye la base de datos del servidor de informes o el sistema de archivos.|

**SystemReportTimeout**  
El valor de tiempo de espera de procesamiento de informes predeterminado, en segundos, para todos los informes administrados en el espacio de nombres del servidor de informes. Este valor se puede invalidar en el nivel de informe. Si se establece esta propiedad, el servidor de informes intenta detener el procesamiento de un informe cuando ha expirado el tiempo especificado. Los valores válidos para esta propiedad van desde **-1** a **2** **147** **483** **647**. Si el valor es **-1**, no se agota el tiempo de espera de los informes del espacio de nombres durante el procesamiento. El valor predeterminado es **1800**.  

**SystemSnapshotLimit**  
Número máximo de instantáneas almacenadas para un informe. Los valores válidos para esta propiedad van desde **-1** a **2** **147** **483** **647**. Si el valor es **-1**, no hay ningún límite de instantáneas.  

**EnableIntegratedSecurity**  
Determina si se admite la seguridad integrada de Windows para las conexiones de origen de datos del informe. El valor predeterminado es **True**. Los valores válidos son los siguientes:

|Valores|Description|
|---------|---------|
|**True**|La seguridad integrada de Windows está habilitada.|
|**False**|La seguridad integrada de Windows no está habilitada. No se ejecutarán los orígenes de datos de informes que se configuran para usar la seguridad integrada de Windows.|

**EnableLoadReportDefinition**  
Seleccione esta opción para especificar si los usuarios pueden realizar la ejecución de notificaciones ad hoc desde un informe del Generador de informes. Al establecer esta opción, se determina el valor de la propiedad **EnableLoadReportDefinition** en el servidor de informes.  

Si desactiva esta opción, la propiedad se establecerá en False y el servidor de informes no generará informes click-through para los informes que usan un modelo de informe como origen de datos. Se bloquearán las llamadas al método LoadReportDefinition.  

Al desactivar esta opción, se mitiga una amenaza en la que un usuario malintencionado inicia un ataque por denegación de servicio sobrecargando el servidor de informes con solicitudes LoadReportDefinition.  

**EnableRemoteErrors**  
Incluye información de errores externa (por ejemplo, sobre los orígenes de datos de informe) con los mensajes de error que se devuelven para los usuarios que solicitan informes de los equipos remotos. Los valores válidos son **true** y **false**. El valor predeterminado es **false**. Para más información, vea [Habilitar errores remotos &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md).  

**EnableReportDesignClientDownload**  
Especifica si el paquete de instalación del Generador de informes se puede descargar del servidor de informes. Si borra este valor, la dirección URL al Generador de informes no funcionará. Para más información, vea [Configurar el acceso al Generador de informes](../../reporting-services/report-server/configure-report-builder-access.md).  

**EditSessionCacheLimit**  
Especifica el número de entradas de datos en memoria caché que pueden estar activas en una sesión de edición de informes. El número predeterminado es 5.  

**EditSessionTimeout**  
Especifica el número de segundos tras los cuales se agotará el tiempo de espera para una sesión de edición de informes. El valor predeterminado es de 7200 segundos (2 horas).  

**EnableCustomVisuals** ***(solo Power BI Report Server)***  
Si Power BI Report Server debe habilitar la visualización de objetos visuales personalizados de Power BI. Los valores son True o False.  El valor predeterminado es True.  

**EnablePowerBIReportExportData** ***(solo Power BI Report Server)***  
Si Power BI Report Server debe habilitar la exportación de datos desde objetos visuales de Power BI. Los valores son True o False.  El valor predeterminado es True.  

**ScheduleRefreshTimeoutMinutes** ***(solo Power BI Report Server)***  
Tiempo de espera de actualización de datos en minutos para la actualización programada en informes de Power BI con modelos de AS incrustados. El valor predeterminado es 120 minutos.

**EnableTestConnectionDetailedErrors**  
Indica si se han enviado al equipo cliente los mensajes de error detallados cuando los usuarios prueban las conexiones a orígenes de datos mediante el servidor de informes. El valor predeterminado es **true**. Si la opción se establece en **false**, solo se enviarán mensajes de error genéricos.

**AccessControlAllowCredentials**  
Indica si la respuesta a la solicitud del cliente puede exponerse cuando la marca 'credentials' está establecida en true. El valor predeterminado es **false**.

**AccessControlAllowHeaders** Lista separada por comas de encabezados que el servidor permite cuando un cliente realiza una solicitud. Esta propiedad puede ser una cadena vacía; si se especifica *, se permiten todos los encabezados.

**AccessControlAllowMethods** Lista separada por comas de métodos HTTP que el servidor permite cuando un cliente realiza una solicitud. Los valores predeterminados son (GET, PUT, POST, PATCH, DELETE); si se especifica *, se permiten todos los métodos.

**AccessControlAllowOrigin** Lista separada por comas de orígenes que el servidor permite cuando un cliente realiza una solicitud. El valor predeterminado es en blanco, lo que evita todas las solicitudes; si se especifica *, se permiten todos los orígenes siempre que no haya credenciales establecidas; si hay credenciales especificadas, se debe especificar una lista explícita de orígenes.

**AccessControlExposeHeaders** Lista separada por comas de encabezados que el servidor va a exponer a los clientes. Está en blanco de forma predeterminada.

**AccessControlMaxAge** Especifica el número de segundos durante los que se pueden almacenar en caché los resultados de la solicitud preparatoria. El valor predeterminado es 600 (10 minutos).

## <a name="see-also"></a>Vea también

[Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Conectar con un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Propiedades de Reporting Services](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Servidor de informes en Management Studio ayuda F1](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[Propiedades del sistema del servidor de informes](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[Script para tareas administrativas y de implementación](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[Habilitar y deshabilitar Mis informes](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
