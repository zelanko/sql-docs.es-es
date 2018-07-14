---
title: Propiedades del servidor (página de opciones avanzadas) - Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 2016-10-18
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.advanced.f1
ms.assetid: 07b78a84-a6aa-4502-861d-349720ef790e
caps.latest.revision: 16
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8b8459ccb49c2e8d2d681cada3646d7d9aa447b5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37258131"
---
# <a name="server-properties-advanced-page---reporting-services"></a>Propiedades del servidor (página de opciones avanzadas) - Reporting Services
  Use esta página para establecer las propiedades del sistema en el servidor de informes. Hay varias maneras de establecer las propiedades del sistema. Esta herramienta proporciona una interfaz de usuario gráfica para que pueda establecer propiedades sin tener que escribir código.  
  
 Para abrir esta página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a una instancia del servidor de informes, haga clic con el botón derecho en el nombre del servidor de informes y seleccione **Propiedades**. Haga clic en **Avanzadas** para abrir esta página.  
  
## <a name="options"></a>Opciones  
 **EnableMyReports**  
 Indica si la característica Mis informes está habilitada. Un valor de `true` indica que la característica está habilitada.  
  
 **MyReportsRole**  
 El nombre del rol que se usa al crear directivas de seguridad en las carpetas Mis informes del usuario. El valor predeterminado es `My Reports Role`.  
  
 **EnableClientPrinting**  
 Determina si el control ActiveX RSClientPrint está disponible para descargarlo del servidor de informes. Los valores válidos son `true` y `false`. El valor predeterminado es `true`. Para más información sobre opciones de configuración adicionales necesarias para este control, vea [Habilitar y deshabilitar la impresión del lado cliente para Reporting Services](../report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  
  
 **EnableExecutionLogging**  
 Indica si el registro de ejecución de informes está habilitado. El valor predeterminado es `true`. Para obtener más información sobre el registro de ejecución del servidor de informes, vea [registro de ejecución del servidor de informes y la vista ExecutionLog3](../report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
 **ExecutionLogDaysKept**  
 Número de días que mantener la información de ejecución de informes en el registro de ejecución. Los valores válidos para esta propiedad incluyen `-1` a través de `2`,`147`,`483`,`647`. Si el valor es `-1` no se eliminan las entradas de la tabla del registro de ejecución. El valor predeterminado es `60`.  
  
 **SessionTimeout**  
 El período, en segundos, que una sesión permanece activa. El valor predeterminado es `600`.  
  
 **SharePointIntegratedMode**  
 Ésta es una propiedad de solo lectura que indica el modo de servidor. Si este valor es False, el servidor de informes se ejecuta en modo nativo.  
  
 **SiteName**  
 El nombre del sitio del servidor de informes mostrado en el título de la página de Administrador de informes. El valor predeterminado es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Esta propiedad puede ser una cadena vacía. La longitud máxima es de 8000 caracteres.  
  
 **StoredParametersLifetime**  
 Especifica el número máximo de días que un parámetro almacenado puede estar almacenado. Los valores válidos son `-1`, `+1` a través de `2,147,483,647`. El valor predeterminado es `180` días.  
  
 **StoredParametersThreshold**  
 Especifica el número máximo de valores de parámetro que se pueden almacenar por el servidor de informes. Los valores válidos son `-1`, `+1` a través de `2,147,483,647`. El valor predeterminado es `1500`.  
  
 **UseSessionCookies**  
 Indica si el servidor de informes debería usar cookies de sesión al comunicarse con exploradores cliente. El valor predeterminado es `true`.  
  
 **ExternalImagesTimeout**  
 Determina el período de tiempo dentro del cual se debe recuperar un archivo de imagen externo antes de que se agote el tiempo de espera de la conexión. El valor predeterminado es `600` segundos.  
  
 **SnapshotCompression**  
 Define la manera en la que se comprimen las instantáneas. El valor predeterminado es `SQL`. Los valores válidos son los siguientes:  
  
 **SQL =** las instantáneas se comprimen cuando se almacenan en la base de datos del servidor de informes. Éste es el comportamiento actual.  
  
 **None =** no se comprimen las instantáneas.  
  
 **All =** las instantáneas se comprimen para todas las opciones de almacenamiento, entre las que se incluyen la base de datos del servidor de informes o el sistema de archivos.  
  
 **SystemReportTimeout**  
 El valor de tiempo de espera de procesamiento de informes predeterminado, en segundos, para todos los informes administrados en el espacio de nombres del servidor de informes. Este valor se puede invalidar en el nivel de informe. Si se establece esta propiedad, el servidor de informes intenta detener el procesamiento de un informe cuando ha expirado el tiempo especificado. Los valores válidos son `-1` a través de `2`,`147`,`483`,`647`. Si el valor es `-1`, no se agota el tiempo de los informes del espacio de nombres durante el procesamiento. El valor predeterminado es `1800`.  
  
 **SystemSnapshotLimit**  
 Número máximo de instantáneas almacenadas para un informe. Los valores válidos son `-1` a través de `2`,`147`,`483`,`647`. Si el valor es `-1`, no hay ningún límite de instantáneas.  
  
 **EnableIntegratedSecurity**  
 Determina si se admite la seguridad integrada de Windows para las conexiones de origen de datos del informe. El valor predeterminado es `True`. Los valores válidos son los siguientes:  
  
 `True` = la seguridad integrada de Windows está habilitada.  
  
 `False` = la seguridad integrada de Windows no está habilitada. No se ejecutarán los orígenes de datos de informes que se configuran para usar la seguridad integrada de Windows.  
  
 `EnableLoadReportDefinition`  
 Seleccione esta opción para especificar si los usuarios pueden realizar la ejecución de notificaciones ad hoc desde un informe del Generador de informes. Al establecer esta opción determina el valor de la `EnableLoadReportDefinition` propiedad del servidor de informes.  
  
 Si desactiva esta opción, la propiedad se establecerá en False y el servidor de informes no generará informes click-through para los informes que usan un modelo de informe como origen de datos. Se bloquearán las llamadas al método LoadReportDefinition.  
  
 Al desactivar esta opción, se mitiga una amenaza en la que un usuario malintencionado inicia un ataque por denegación de servicio sobrecargando el servidor de informes con solicitudes LoadReportDefinition.  
  
 **EnableRemoteErrors**  
 Incluye información de errores externa (por ejemplo, sobre los orígenes de datos de informe) con los mensajes de error que se devuelven para los usuarios que solicitan informes de los equipos remotos. Los valores válidos son `true` y `false`. El valor predeterminado es `false`. Para más información, vea [Habilitar errores remotos &#40;Reporting Services&#41;](../report-server/enable-remote-errors-reporting-services.md).  
  
 **EnableReportDesignClientDownload**  
 Especifica si el paquete de instalación del Generador de informes se puede descargar del servidor de informes. Si borra este valor, la dirección URL al Generador de informes no funcionará. Para más información, vea [Configurar el acceso al Generador de informes](../report-server/configure-report-builder-access.md).  
  
 **EditSessionCacheLimit**  
 Especifica el número de entradas de datos en memoria caché que pueden estar activas en una sesión de edición de informes. El número predeterminado es 5.  
  
 **EditSessionTimeout**  
 Especifica el número de segundos tras los cuales se agotará el tiempo de espera para una sesión de edición de informes. El valor predeterminado es de 7200 segundos (2 horas).  
  
 **EnableTestConnectionDetailedErrors**  
 Indica si se han enviado al equipo cliente los mensajes de error detallados cuando los usuarios prueban las conexiones a orígenes de datos mediante el servidor de informes. El valor predeterminado es `true`. Si la opción se establece en `false`, solo los mensajes de error genéricos se envían.  
  
## <a name="see-also"></a>Vea también  
 [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Conectar con un servidor de informes en Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Propiedades de Reporting Services](../report-server-web-service/net-framework/reporting-services-properties.md)   
 [Servidor de informes en Management Studio ayuda F1](report-server-in-management-studio-f1-help.md)   
 [Propiedades del sistema del servidor de informes](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
 [Script para tareas administrativas y de implementación](script-deployment-and-administrative-tasks.md)   
 [Habilitar y deshabilitar Mis informes](../report-server/enable-and-disable-my-reports.md)  
  
  
