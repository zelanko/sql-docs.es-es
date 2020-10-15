---
title: Página Opciones avanzadas de las propiedades del servidor | Microsoft Docs
description: Use la página Opciones avanzadas de las propiedades del servidor para establecer las propiedades del sistema en el servidor de informes. Esta herramienta proporciona una interfaz gráfica de usuario para que pueda establecer las propiedades sin tener que escribir código.
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.date: 08/17/2020
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 9d5132ad1ea115e051a4c9d4ba898aa53ddeb98a
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988752"
---
# <a name="server-properties-advanced-page---power-bi-report-server--reporting-services"></a>Página Opciones avanzadas de las propiedades del servidor: Power BI Report Server y Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Use esta página para establecer las propiedades del sistema en el servidor de informes. Hay varias maneras de establecer las propiedades del sistema. Esta herramienta proporciona una interfaz de usuario gráfica para que pueda establecer propiedades sin tener que escribir código.

Para abrir esta página, inicie SQL Server Management Studio, conéctese a una instancia del servidor de informes, haga clic con el botón derecho en el nombre del servidor de informes y seleccione **Propiedades**. Seleccione **Opciones avanzadas** para abrir esta página.

## <a name="options"></a>Opciones

### <a name="accesscontrolallowcredentials"></a>AccessControlAllowCredentials
(Solo Power BI Report Server, Reporting Services 2017 y versiones posteriores) Indica si la respuesta a la solicitud del cliente se puede exponer cuando la marca `credentials` está establecida en true. El valor predeterminado es **false**.

### <a name="accesscontrolallowheaders"></a>AccessControlAllowHeaders
(Solo Power BI Report Server, Reporting Services 2017 y versiones posteriores) Lista separada por comas de encabezados que el servidor permitirá cuando un cliente realiza una solicitud. Esta propiedad puede ser una cadena vacía; si se especifica *, se permiten todos los encabezados.

### <a name="accesscontrolallowmethods"></a>AccessControlAllowMethods
(Solo Power BI Report Server, Reporting Services 2017 y versiones posteriores) Lista separada por comas de métodos HTTP que el servidor permitirá cuando un cliente realiza una solicitud. Los valores predeterminados son (GET, PUT, POST, PATCH, DELETE); si se especifica *, se permiten todos los métodos.

### <a name="accesscontrolalloworigin"></a>AccessControlAllowOrigin
(Solo Power BI Report Server, Reporting Services 2017 y versiones posteriores) Lista separada por comas de los orígenes que el servidor permitirá cuando un cliente realiza una solicitud. El valor predeterminado es en blanco, lo que evita todas las solicitudes; si se especifica *, se permiten todos los orígenes siempre que no haya credenciales establecidas; si hay credenciales especificadas, se debe especificar una lista explícita de orígenes.

### <a name="accesscontrolexposeheaders"></a>AccessControlExposeHeaders
(Solo Power BI Report Server, Reporting Services 2017 y versiones posteriores) Lista separada por comas de encabezados que el servidor expondrá a los clientes. Está en blanco de forma predeterminada.

### <a name="accesscontrolmaxage"></a>AccessControlMaxAge
(Solo Power BI Report Server, Reporting Services 2017 y versiones posteriores) Especifica el número de segundos que se pueden almacenar en caché los resultados de la solicitud preparatoria. El valor predeterminado es 600 (10 minutos).

### <a name="allowedresourceextensionsforupload"></a>AllowedResourceExtensionsForUpload
(Solo Power BI Report Server y Reporting Services 2017 y versiones posteriores) Conjunto de extensiones de recursos que se pueden cargar en el servidor de informes. No es necesario incluir extensiones para tipos de archivos integrados como &ast;.rdl y &ast;.pbix. El valor predeterminado es "&ast;, &ast;.xml, &ast;.xsd, &ast;.xsl, &ast;.png, &ast;.gif, &ast;.jpg, &ast;.tif, &ast;.jpeg, &ast;.tiff, &ast;.bmp, &ast;.pdf, &ast;.svg, &ast;.rtf, &ast;.txt, &ast;.doc, &ast;.docx, &ast;.pps, &ast;.ppt, &ast;.pptx".

### <a name="customheaders"></a>CustomHeaders 

(Solo Power BI Report Server de enero de 2020 y Reporting Services 2019 y versiones posteriores)

Establece los valores de encabezado para todas las direcciones URL que coinciden con el patrón de expresión regular especificado. Los usuarios pueden actualizar el valor CustomHeaders con XML válido para establecer los valores de encabezado de las direcciones URL de solicitud seleccionadas. Los administradores pueden agregar cualquier número de encabezados en el XML. En Reporting Services 2019, de forma predeterminada, no hay ningún encabezado personalizado y el valor está en blanco. En Power BI Report Server (enero de 2020) y versiones posteriores, el valor es este:

```xml
<CustomHeaders>
    <Header>
        <Name>X-Frame-Options</Name>
        <Pattern>(?(?=.*api.*|.*rs:embed=true.*|.*rc:toolbar=false.*)(^((?!(.+)((\/api)|(\/(mobilereport|report|excel|pages|powerbi)\/(.+)(rs:embed=true|rc:toolbar=false)))).*$))|(^(?!(http|https):\/\/([^\/]+)\/powerbi.*$)))</Pattern>
        <Value>SAMEORIGIN</Value>
    </Header>
</CustomHeaders>
```

> [!NOTE]
> Un número excesivo de encabezados puede afectar el rendimiento. 

Se recomienda validar la configuración de la topología para garantizar que el conjunto de encabezados es compatible con su implementación de Reporting Services. Es posible elegir la configuración que provoca errores en los exploradores si los exploradores no tienen también la configuración adecuada. Por ejemplo, no debe agregar una configuración de HSTS si el servidor no está configurado para HTTPS. Los encabezados incompatibles pueden dar lugar a errores de representación en el explorador.

#### <a name="customheaders-xml-format"></a>Formato XML de CustomHeaders

```xml
<CustomHeaders>
    <Header>
        <Name>{Name of the header}</Name>
        <Pattern>{Regex pattern to match URLs}</Pattern>
        <Value>{Value of the header}</Value>
    </Header>
</CustomHeaders>
```

#### <a name="setting-the-customheaders-property"></a>Establecimiento de la propiedad CustomHeaders

- Se puede establecer mediante el punto de conexión SOAP de [SetSystemProperties](/dotnet/api/reportservice2010.reportingservice2010.setsystemproperties) pasando la propiedad CustomHeaders como parámetro.
- Puede usar el punto de conexión REST de [UpdateSystemProperties](https://app.swaggerhub.com/apis/microsoft-rs/PBIRS/2.0#/System/UpdateSystemProperties):  `/System/Properties` pasando la propiedad CustomHeaders.

#### <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra cómo establecer HSTS y otros encabezados personalizados para las direcciones URL con el patrón de expresión regular coincidente.

```xml
<CustomHeaders>
    <Header>
        <Name>Strict-Transport-Security</Name>
        <Pattern>\/Reports\/mobilereport</Pattern>
        <Value>max-age=86400</Value>
    </Header>
    <Header>
        <Name>Embed</Name>
        <Pattern>(.+)(/reports/)(.+)(rs:embed=true)</Pattern>
        <Value>True</Value>
    </Header>
</CustomHeaders>
```

El primer encabezado del XML anterior agrega el encabezado `Strict-Transport-Security: max-age=86400` a las solicitudes coincidentes.
- http://adventureworks/Reports/mobilereport/New%20Mobile%20Report: la expresión regular coincidió y establecerá el encabezado HSTS
- http://adventureworks/ReportServer/mobilereport/New%20Mobile%20Report: error de coincidencia

El segundo encabezado del XML anterior agrega el encabezado `Embed: True` para la dirección URL que contiene el parámetro de consulta `/reports/` y `rs:embed=true`.
- https://adventureworks/reports/mobilereport/New%20Mobile%20Report?rs:embed=true: coincidencia
- https://adventureworks/reports/mobilereport/New%20Mobile%20Report?rs:embed=false: error de coincidencia

### <a name="editsessioncachelimit"></a>EditSessionCacheLimit
Especifica el número de entradas de datos en memoria caché que pueden estar activas en una sesión de edición de informes. El número predeterminado es 5.  

### <a name="editsessiontimeout"></a>EditSessionTimeout
Especifica el número de segundos tras los cuales se agotará el tiempo de espera para una sesión de edición de informes. El valor predeterminado es 7200 segundos (dos horas). 

### <a name="enablecdnvisuals"></a>EnableCDNVisuals 
(Solo Power BI Report Server) Cuando se habilita, los informes de Power BI cargan los objetos visuales personalizados certificados más recientes desde una red de entrega de contenido (CDN) hospedada por Microsoft. Si el servidor no tiene acceso a los recursos de Internet, puede desactivar esta opción. En ese caso, los objetos visuales personalizados se cargan desde el informe que se publicó en el servidor. El valor predeterminado es **true**.  

###  <a name="enableclientprinting"></a>EnableClientPrinting  
Determina si el control ActiveX RSClientPrint está disponible para descargarlo del servidor de informes. Los valores válidos son **true** y **false**. El valor predeterminado es **true**. Para más información sobre opciones de configuración adicionales necesarias para este control, vea [Habilitar y deshabilitar la impresión del lado cliente para Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  

### <a name="enablecustomvisuals"></a>EnableCustomVisuals 
(Solo Power BI Report Server) Para habilitar la visualización de los objetos visuales de Power BI. Los valores son True o False. *El valor predeterminado es True.*  

###  <a name="enableexecutionlogging"></a>EnableExecutionLogging  
Indica si el registro de ejecución de informes está habilitado. El valor predeterminado es **true**. Para más información sobre el registro de ejecución del servidor de informes, vea [Registro de ejecución del servidor de informes y la vista ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  

### <a name="enableintegratedsecurity"></a>EnableIntegratedSecurity
Determina si se admite la seguridad integrada de Windows para las conexiones de origen de datos de informes. El valor predeterminado es **True**. Los valores válidos son los siguientes:

|Valores|Descripción|
|---------|---------|
|**True**|La seguridad integrada de Windows está habilitada.|
|**False**|La seguridad integrada de Windows no está habilitada. No se ejecutarán los orígenes de datos de informes configurados para usar la seguridad integrada de Windows.|

### <a name="enableloadreportdefinition"></a>EnableLoadReportDefinition
Seleccione esta opción para especificar si los usuarios pueden realizar una ejecución de informes no planeada desde un informe del Generador de informes. Al establecer esta opción, se determina el valor de la propiedad **EnableLoadReportDefinition** en el servidor de informes.  

Si se desactiva esta opción, la propiedad se establece en False. El servidor de informes no generará informes click-through para los informes en los que se use un modelo de informe como origen de datos. Se bloquean todas las llamadas al método LoadReportDefinition.  

Al desactivar esta opción, se mitiga una amenaza en la que un usuario malintencionado inicia un ataque por denegación de servicio sobrecargando el servidor de informes con solicitudes LoadReportDefinition.  

### <a name="enablemyreports"></a>EnableMyReports  
Indica si la característica Mis informes está habilitada. El valor **true** indica que la característica está habilitada.  

### <a name="enablepowerbireportexportdata"></a>EnablePowerBIReportExportData 
(Solo Power BI Report Server) Habilita la exportación de datos de Power BI Report Server desde los objetos visuales de Power BI. Los valores son True o False.  El valor predeterminado es True. 

### <a name="enablepowerbireportexportunderlyingdata"></a>EnablePowerBIReportExportUnderlyingData 
(Solo Power BI Report Server) Indica si un cliente puede exportar los datos subyacentes de los objetos visuales de Power BI en Power BI Report Server. Un valor de True indica que la característica está habilitada.

### <a name="enableremoteerrors"></a>EnableRemoteErrors
Incluye información de errores externa (por ejemplo, sobre los orígenes de datos de informe) con los mensajes de error que se devuelven para los usuarios que solicitan informes de los equipos remotos. Los valores válidos son **true** y **false**. El valor predeterminado es **false**. Para más información, vea [Habilitar errores remotos &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md).  

### <a name="enabletestconnectiondetailederrors"></a>EnableTestConnectionDetailedErrors
Indica si se envían mensajes de error detallados al equipo cliente cuando los usuarios prueban las conexiones a orígenes de datos mediante el servidor de informes. El valor predeterminado es **true**. Si la opción se establece en **false**, solo se enviarán mensajes de error genéricos.

###  <a name="executionlogdayskept"></a>ExecutionLogDaysKept  
Número de días que mantener la información de ejecución de informes en el registro de ejecución. Entre los valores válidos de esta propiedad están el rango **-1** - **2**,**147**,**483**y**647**. Si el valor es **-1**, no se eliminan las entradas de la tabla del registro de ejecución. El valor predeterminado es **60**.  

> [!NOTE]
> Si establece un valor de **0, se ** *eliminan* todas las entradas del registro de ejecución. Un valor de **-1** mantiene las entradas del registro de ejecución y no las elimina.

### <a name="executionloglevel"></a>ExecutionLogLevel
Establezca el nivel de registro de ejecución. *El valor predeterminado es Normal.*

### <a name="externalimagestimeout"></a>ExternalImagesTimeout
Determina el período de tiempo dentro del cual se debe recuperar un archivo de imagen externo antes de que se agote el tiempo de espera de la conexión. El valor predeterminado es **600** segundos.  

### <a name="interprocesstimeoutminutes"></a>InterProcessTimeoutMinutes
(Solo Power BI Report Server, Reporting Services 2019 y versiones posteriores) Establece el tiempo de espera del proceso en minutos. *El valor predeterminado es 30.*

### <a name="maxfilesizemb"></a>MaxFileSizeMb
Establezca el tamaño máximo del archivo en MB. *El valor predeterminado es 1000.  El máximo es 2000.*

### <a name="modelcleanupcycleminutes"></a>ModelCleanupCycleMinutes 
(Solo Power BI Report Server) Establece la frecuencia de comprobación de los modelos no utilizados en memoria en minutos. *El valor predeterminado es 15.*

### <a name="modelexpirationminutes"></a>ModelExpirationMinutes 
(Solo Power BI Report Server) Establece la frecuencia con la que los modelos sin usar se expulsan de la memoria en minutos. *El valor predeterminado es 60.*

###  <a name="myreportsrole"></a>MyReportsRole  
El nombre del rol que se usa al crear directivas de seguridad en las carpetas Mis informes del usuario. El valor predeterminado es **My Reports Role**.  

### <a name="officeaccesstokenexpirationseconds"></a>OfficeAccessTokenExpirationSeconds 
(Solo Power BI Report Server, Reporting Services 2019 y versiones posteriores) Establece cuánto tiempo, en segundos, se quiere que expire el token de acceso de Office. *El valor predeterminado es 60.*

### <a name="officeonlinediscoveryurl"></a>OfficeOnlineDiscoveryURL 
(Solo Power BI Report Server) Establece la dirección de la instancia de Office Online Server para ver Libros de Excel.

### <a name="rdlxreporttimetout"></a>RDLXReportTimetout
El valor de tiempo de espera de procesamiento del informe RDLX *(informes de Power View en SharePoint Server)*, en segundos, para todos los informes administrados en el espacio de nombres del servidor de informes. Este valor se puede invalidar en el nivel de informe. Si se establece esta propiedad, el servidor de informes intenta detener el procesamiento de un informe cuando ha expirado el tiempo especificado. Los valores válidos para esta propiedad van desde **-1** a **2****147****483****647**. Si el valor es **-1**, no se agota el tiempo de espera de los informes del espacio de nombres durante el procesamiento. El valor predeterminado es **1800**.

### <a name="requireintune"></a>RequireIntune
(Solo Power BI Report Server, Reporting Services 2017 y versiones posteriores) Requiere Intune para acceder a los informes de la organización a través de la aplicación móvil de Power BI. *El valor predeterminado es False.*

### <a name="restrictedresourcemimetypeforupload"></a>RestrictedResourceMimeTypeForUpload
(Solo Power BI Report Server de enero de 2019, Reporting Services 2017 y versiones posteriores) El conjunto de tipos MIME con el que los usuarios no pueden cargar contenido. Los recursos que ya estén almacenados con un tipo MIME restringido solo se pueden descargar como application/octet-stream en lugar de abrirse o ejecutarse en el explorador.  De forma predeterminada, no hay ningún elemento restringido en esta lista, pero se recomienda que las organizaciones lo rellenen para proporcionar la mejor experiencia.

### <a name="schedulerefreshtimeoutminutes"></a>ScheduleRefreshTimeoutMinutes 
(Solo Power BI Report Server) Tiempo de espera de actualización de datos en minutos para la actualización programada en informes de Power BI con modelos de AS incrustados. El valor predeterminado es 120 minutos.

### <a name="sessiontimeout"></a>SessionTimeout
El período, en segundos, que una sesión permanece activa. El valor predeterminado es **600**.  

### <a name="sharepointintegratedmode"></a>SharePointIntegratedMode
Esta propiedad de solo lectura indica el modo de servidor. Si este valor es False, el servidor de informes se ejecuta en modo nativo.  

### <a name="showdownloadmenu"></a>ShowDownloadMenu
(Solo Power BI Report Server, Reporting Services 2017 y versiones posteriores) Habilita el menú de descarga de las herramientas de cliente. *El valor predeterminado es true.*

### <a name="sitename"></a>SiteName
El nombre del sitio del servidor de informes mostrado en el título de la página del portal web. El valor predeterminado es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Esta propiedad puede ser una cadena vacía. La longitud máxima es de 8000 caracteres.  

### <a name="snapshotcompression"></a>SnapshotCompression
Define la manera en la que se comprimen las instantáneas. El valor predeterminado es **SQL**. Los valores válidos son los siguientes:

|Valores|Descripción|
|---------|---------|
|**SQL**|Las instantáneas se comprimen cuando se almacenan en la base de datos del servidor de informes. Esta compresión es el comportamiento actual.|
|**Ninguno**|Las instantáneas no se comprimen.|
|**All**|Las instantáneas se comprimen para todas las opciones de almacenamiento, lo que incluye la base de datos del servidor de informes o el sistema de archivos.|

### <a name="storedparameterslifetime"></a>StoredParametersLifetime
Especifica el número máximo de días que un parámetro almacenado puede estar almacenado. Los valores válidos **-1**y de **+1** a **2 147 483 647**. El valor predeterminado es **180** días.  

### <a name="storedparametersthreshold"></a>StoredParametersThreshold
Especifica el número máximo de valores de parámetro que se pueden almacenar por el servidor de informes. Los valores válidos **-1**y de **+1** a **2 147 483 647**. El valor predeterminado es **1500**.  

### <a name="supportedhyperlinkschemes"></a>SupportedHyperlinkSchemes 
(Solo Power BI Report Server de enero de 2019, Reporting Services 2019 y versiones posteriores) Establece una lista separada por comas de los esquemas de URI que se pueden definir en acciones de hipervínculo que pueden representarse o "&ast;" para habilitar todos los esquemas de hipervínculo. Por ejemplo, al establecer "http, https" se permitirían los hipervínculos a "https://www. contoso.com", pero quitaría hipervínculos a "mailto:bill@contoso.com" o "javascript:window.open(‘ www.contoso.com’, ‘_blank’)". El valor predeterminado es "&ast;".

### <a name="systemreporttimeout"></a>SystemReportTimeout
El valor de tiempo de espera de procesamiento de informes predeterminado, en segundos, para todos los informes administrados en el espacio de nombres del servidor de informes. Este valor se puede invalidar en el nivel de informe. Si se establece esta propiedad, el servidor de informes intenta detener el procesamiento de un informe cuando ha expirado el tiempo especificado. Los valores válidos para esta propiedad van desde **-1** a **2****147****483****647**. Si el valor es **-1**, no se agota el tiempo de espera de los informes del espacio de nombres durante el procesamiento. El valor predeterminado es **1800**.  

### <a name="systemsnapshotlimit"></a>SystemSnapshotLimit
Número máximo de instantáneas almacenadas para un informe. Los valores válidos para esta propiedad van desde **-1** a **2****147****483****647**. Si el valor es **-1**, no hay ningún límite de instantáneas.  

### <a name="timerinitialdelayseconds"></a>TimerInitialDelaySeconds
(Solo Power BI Report Server, Reporting Services 2017 y versiones posteriores) Establece cuánto tiempo, en segundos, quiere que se retrase la hora de inicio. *El valor predeterminado es 60.*

### <a name="trustedfileformat"></a>TrustedFileFormat
(Solo Power BI Report Server, Reporting Services 2017 y versiones posteriores) Establece todos los formatos de archivo externos que se abren en el explorador en el sitio del portal de Reporting Services. Los formatos de archivo externos no enumerados indican que se descargue la opción en el explorador. Los valores predeterminados son jpg, jpeg, jpe, wav, bmp, pdf, img, gif, json, mp4, web y png.

### <a name="usesessioncookies"></a>UseSessionCookies
Indica si el servidor de informes debería usar cookies de sesión al comunicarse con exploradores cliente. El valor predeterminado es **true**.  

## <a name="see-also"></a>Consulte también

[Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Conectar con un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Propiedades de Reporting Services](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Servidor de informes en Management Studio ayuda F1](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[Propiedades del sistema del servidor de informes](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[Script para tareas administrativas y de implementación](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[Habilitar y deshabilitar Mis informes](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).