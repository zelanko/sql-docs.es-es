---
title: Propiedades del servidor (página de opciones avanzadas) - Reporting Services | Microsoft Docs
author: markingmyname
ms.author: maghan
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.date: 08/16/2018
ms.openlocfilehash: f897c332130ece43357869972ff406ea79a6c21d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47725030"
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
Número de días que mantener la información de ejecución de informes en el registro de ejecución. Entre los valores válidos de esta propiedad están el rango **-1** - **2**,**147**,**483**y**647**. Si el valor es **-1**, no se eliminan las entradas de la tabla del registro de ejecución. El valor predeterminado es **60**.  

> [!NOTE]
> Si establece un valor de **0**, se *eliminan* todas las entradas del registro de ejecución. Un valor de **-1** mantiene las entradas del registro de ejecución y no las elimina.

**RDLXReportTimetout** El valor de tiempo de espera de procesamiento del informe RDLX *(informes de Power View en SharePoint Server)*, en segundos, para todos los informes administrados en el espacio de nombres del servidor de informes. Este valor se puede invalidar en el nivel de informe. Si se establece esta propiedad, el servidor de informes intenta detener el procesamiento de un informe cuando ha expirado el tiempo especificado. Los valores válidos para esta propiedad van desde **-1** a **2** **147** **483** **647**. Si el valor es **-1**, no se agota el tiempo de espera de los informes del espacio de nombres durante el procesamiento. El valor predeterminado es **1800**.

**SessionTimeout** La cantidad de tiempo, en segundos, que una sesión permanece activa. El valor predeterminado es **600**.  

**SharePointIntegratedMode**  
Esta propiedad de solo lectura indica el modo de servidor. Si este valor es False, el servidor de informes se ejecuta en modo nativo.  

**SiteName**  
El nombre del sitio del servidor de informes mostrado en el título de la página del portal web. El valor predeterminado es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Esta propiedad puede ser una cadena vacía. La longitud máxima es de 8000 caracteres.  

**StoredParametersLifetime** Especifica el número máximo de días que se puede almacenar un parámetro almacenado. Los valores válidos **-1**y de **+1** a **2 147 483 647**. El valor predeterminado es **180** días.  

**StoredParametersThreshold**  
Especifica el número máximo de valores de parámetro que se pueden almacenar por el servidor de informes. Los valores válidos **-1**y de **+1** a **2 147 483 647**. El valor predeterminado es **1500**.  

**UseSessionCookies**  
Indica si el servidor de informes debería usar cookies de sesión al comunicarse con exploradores cliente. El valor predeterminado es **true**.  

**ExternalImagesTimeout**  
Determina el período de tiempo dentro del cual se debe recuperar un archivo de imagen externo antes de que se agote el tiempo de espera de la conexión. El valor predeterminado es **600** segundos.  

**SnapshotCompression** una instantánea del servidor de informes en ese momento.

**SnapshotCompression**  
Define la manera en la que se comprimen las instantáneas. El valor predeterminado es **SQL**. Los valores válidos son los siguientes:

|Valores|Descripción|
|---------|---------|
|**SQL**|Las instantáneas se comprimen cuando se almacenan en la base de datos del servidor de informes. Esta compresión es el comportamiento actual.|
|**Ninguno**|Las instantáneas no se comprimen.|
|**Todos**|Las instantáneas se comprimen para todas las opciones de almacenamiento, lo que incluye la base de datos del servidor de informes o el sistema de archivos.|

**SystemReportTimeout**  
El valor de tiempo de espera de procesamiento de informes predeterminado, en segundos, para todos los informes administrados en el espacio de nombres del servidor de informes. Este valor se puede invalidar en el nivel de informe. Si se establece esta propiedad, el servidor de informes intenta detener el procesamiento de un informe cuando ha expirado el tiempo especificado. Los valores válidos para esta propiedad van desde **-1** a **2** **147** **483** **647**. Si el valor es **-1**, no se agota el tiempo de espera de los informes del espacio de nombres durante el procesamiento. El valor predeterminado es **1800**.  

**SystemSnapshotLimit**  
Número máximo de instantáneas almacenadas para un informe. Los valores válidos para esta propiedad van desde **-1** a **2** **147** **483** **647**. Si el valor es **-1**, no hay ningún límite de instantáneas.  

**EnableIntegratedSecurity**  
Determina si se admite la seguridad integrada de Windows para las conexiones de origen de datos de informes. El valor predeterminado es **True**. Los valores válidos son los siguientes:

|Valores|Descripción|
|---------|---------|
|**True**|La seguridad integrada de Windows está habilitada.|
|**False**|La seguridad integrada de Windows no está habilitada. No se ejecutarán los orígenes de datos de informes configurados para usar la seguridad integrada de Windows.|

**EnableLoadReportDefinition**  
Seleccione esta opción para especificar si los usuarios pueden realizar una ejecución de informes no planeada desde un informe del Generador de informes. Al establecer esta opción, se determina el valor de la propiedad **EnableLoadReportDefinition** en el servidor de informes.  

Si se desactiva esta opción, la propiedad se establece en False. El servidor de informes no generará informes click-through para los informes en los que se use un modelo de informe como origen de datos. Se bloquean todas las llamadas al método LoadReportDefinition.  

Al desactivar esta opción, se mitiga una amenaza en la que un usuario malintencionado inicia un ataque por denegación de servicio sobrecargando el servidor de informes con solicitudes LoadReportDefinition.  

**EnableRemoteErrors**  
Incluye información de errores externa (por ejemplo, sobre los orígenes de datos de informe) con los mensajes de error que se devuelven para los usuarios que solicitan informes de los equipos remotos. Los valores válidos son **true** y **false**. El valor predeterminado es **false**. Para más información, vea [Habilitar errores remotos &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md).  

**AccessControlAllowCredentials**  
Indica si la respuesta a la solicitud del cliente puede exponerse cuando la marca 'credentials' está establecida en true. El valor predeterminado es **false**.

**AccessControlAllowHeaders** Lista separada por comas de encabezados que el servidor permitirá cuando un cliente realice una solicitud. Esta propiedad puede ser una cadena vacía; si se especifica *, se permiten todos los encabezados.

**AccessControlAllowMethods** Lista separada por comas de métodos HTTP que el servidor permitirá cuando un cliente realice una solicitud. Los valores predeterminados son (GET, PUT, POST, PATCH, DELETE); si se especifica *, se permiten todos los métodos.

**AccessControlAllowOrigin** Lista separada por comas de los orígenes que el servidor permitirá cuando un cliente realice una solicitud. El valor predeterminado es en blanco, lo que evita todas las solicitudes; si se especifica *, se permiten todos los orígenes siempre que no haya credenciales establecidas; si hay credenciales especificadas, se debe especificar una lista explícita de orígenes.

**AccessControlExposeHeaders** Lista separada por comas de encabezados que el servidor va a exponer a los clientes. Está en blanco de forma predeterminada.

**AccessControlMaxAge** Especifica el número de segundos durante los que se pueden almacenar en caché los resultados de la solicitud preparatoria. El valor predeterminado es 600 (10 minutos).

**EditSessionCacheLimit**  
Especifica el número de entradas de datos en memoria caché que pueden estar activas en una sesión de edición de informes. El número predeterminado es 5.  

**EditSessionTimeout**  
Especifica el número de segundos tras los cuales se agotará el tiempo de espera para una sesión de edición de informes. El valor predeterminado es 7200 segundos (dos horas).  

**EnableCustomVisuals** ***(solo en Power BI Report Server)*** Para habilitar la visualización de los objetos visuales personalizados de Power BI. Los valores son True o False. *El valor predeterminado es True.*  

**ExecutionLogLevel** Establece el nivel del registro de ejecución. *El valor predeterminado es Normal.*

**InterProcessTimeoutMinutes** Establece el tiempo de espera del proceso en minutos. *El valor predeterminado es 30.*

**MaxFileSizeMb** Establece el tamaño máximo de archivo del informe en MB. *El valor predeterminado es 1000.  El máximo es 2000.*

**ModelCleanupCycleminutes** Establece el ciclo de limpieza del modelo en minutos. *El valor predeterminado es 15.*

**OfficeAccessTokenExpirationSeconds** ***(solo para Power BI Report Server)*** Establece cuánto tiempo, en segundos, se quiere que expire el token de acceso de Office. *El valor predeterminado es 60.*

**OfficeOnlineDiscoveryURL** ***(solo para Power BI Report Server)*** Establece la dirección de la instancia de Office Online Server para ver libros de Excel.

**RequireIntune** Exige a Intune que tenga acceso a los informes de la organización a través de la aplicación móvil de Power BI. *El valor predeterminado es False.*

**ScheduleRefreshTimeoutMinutes** ***(solo para Power BI Report Server)*** Establece el tiempo de expiración que se quiere para la actualización de programación. *El valor predeterminado es 120.*

**ShowDownloadMenu** Habilita el menú de descarga de herramientas cliente. *El valor predeterminado es true.*

**TimeInitialDelaySeconds** Establece cuánto tiempo se quiere retrasar en segundos la hora inicial. *El valor predeterminado es 60.*

**TrustedFileFormat** Establece todos los formatos de archivo externos que se abren dentro del explorador en el sitio de portal de Reporting Services. Los formatos de archivo externos no enumerados indican que se descargue la opción en el explorador. Los valores predeterminados son jpg, jpeg, jpe, wav, bmp, pdf, img, gif, json, mp4, web y png.

**EnablePowerBIReportExportData** ***(solo Power BI Report Server)***  
Habilita la exportación de datos de Power BI Report Server desde objetos visuales de Power BI. Los valores son True o False.  El valor predeterminado es True.  

**ScheduleRefreshTimeoutMinutes** ***(solo Power BI Report Server)***  
Tiempo de espera de actualización de datos en minutos para la actualización programada en informes de Power BI con modelos de AS incrustados. El valor predeterminado es 120 minutos.

**EnableTestConnectionDetailedErrors**  
Indica si se envían mensajes de error detallados al equipo cliente cuando los usuarios prueban las conexiones a orígenes de datos mediante el servidor de informes. El valor predeterminado es **true**. Si la opción se establece en **false**, solo se enviarán mensajes de error genéricos.

## <a name="see-also"></a>Ver también

[Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Conectar con un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Propiedades de Reporting Services](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Servidor de informes en Management Studio ayuda F1](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[Propiedades del sistema del servidor de informes](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[Script para tareas administrativas y de implementación](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[Habilitar y deshabilitar Mis informes](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
