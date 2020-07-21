---
title: Administrar archivos de registro de DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- logging
- log files
- dqs log files
ms.assetid: 4fccfd24-aede-4882-be69-ec1e82682e16
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6e22df90d4e5cb08ac5836f78f4940559be266ec
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937536"
---
# <a name="manage-dqs-log-files"></a>Administrar archivos de registro de DQS
  Los archivos de registro de[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) le ayudan a diagnosticar y solucionar los problemas relacionados con [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]y [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]. Se generan archivos de registro independientes para [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]y el [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)].  
  
 Puede utilizar [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] para configurar el valor de gravedad del registro para los módulos y las características de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] . Además, también es posible configurar varios valores (avanzados) para los archivos de registro de DQS cambiando manualmente la configuración del registro de DQS en la base de datos DQS_MAIN y un archivo XML en el equipo de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] .  
  
##  <a name="data-quality-server-log-file"></a><a name="DQSServer"></a>Archivo de registro de Data Quality Server  
 El archivo de registro de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] , DQServerLog.DQS_MAIN.log, incluye registros de las actividades que se ejecutan en [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. Si instaló la instancia predeterminada de SQL Server, el archivo DQServerLog.DQS_MAIN.log se encontrará en C:\Archivos de programa\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log. El archivo de registro de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] contiene los elementos de información siguientes, cada uno de ellos delimitado por un carácter de barra vertical (|):  
  
-   Fecha y hora  
  
-   Nombre del subproceso  
  
-   Id. de subproceso  
  
-   Gravedad del registro (FATAL, ERROR, WARN, INFO y DEBUG)  
  
    > [!NOTE]  
    >  La gravedad del registro DEBUG es la misma que Detallado.  
  
-   UID (identificador de infraestructura de DQS interno)  
  
-   Espacio de nombres  
  
-   Clase y método  
  
-   Mensaje  
  
 Junto con estos elementos, el archivo de registro también muestra información sobre la versión de la aplicación, el nombre del equipo, el nombre del usuario y el sistema operativo.  
  
 Una entrada de ejemplo del archivo de registro de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] tiene el aspecto siguiente:  
  
```  
23-08-2013 01:45:29|[]|4|INFO|PUID|InfInfoModuleStarting|Microsoft.Ssdqs.Core.Startup.ServerInit|Starting DQS ServerInit: version [12.0.0.0], machine name [DQS-TEST], user name [NT Service\MSSQLSERVER], operating system [Microsoft Windows NT 6.1.7600.0]...  
```  
  
 El archivo DQServerLog.DQS_MAIN.log es un archivo gradual, y se crea un nuevo archivo de registro cuando el existente supera el límite de tamaño del archivo gradual especificado en la configuración del registro de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] . Para obtener más información, vea [Configure Advanced Settings for DQS Log Files](../../2014/data-quality-services/configure-advanced-settings-for-dqs-log-files.md).  
  
##  <a name="data-quality-client-log-file"></a><a name="DQSClient"></a>Archivo de registro de Data Quality Client  
 El archivo de registro de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , DQClientLog.log, incluye los registros del lado cliente. El archivo de registro de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] está disponible en %APPDATA%\SSDQS\Log. El archivo de registro de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] contiene un conjunto de información similar al del archivo de registro del servidor, pero para el lado cliente.  
  
 Al igual que el archivo de registro de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] , el archivo de registro de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] es un archivo gradual, y se crea un nuevo archivo de registro cuando el existente supera el límite de tamaño del archivo gradual especificado en la configuración del registro de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Para obtener más información, vea [Configure Advanced Settings for DQS Log Files](../../2014/data-quality-services/configure-advanced-settings-for-dqs-log-files.md).  
  
##  <a name="dqs-cleansing-component-log-file"></a><a name="DQSCleansing"></a>Archivo de registro del componente de limpieza de DQS  
 El archivo de registro de [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] , DQSSSISLog.log, incluye registros de las actividades realizadas mediante [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]. El archivo de registro del componente [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] está disponible en %APPDATA%\SSDQS\Log. El archivo de registro de [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] contiene un conjunto de información similar al del archivo de registro del servidor, pero para [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)].  
  
##  <a name="related-tasks"></a><a name="RT"></a> Tareas relacionadas  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo configurar los valores de gravedad del registro para los archivos de registro de DQS mediante [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].|[Configurar los niveles de gravedad de los archivos de registro de DQS](../../2014/data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|Describe cómo realizar manualmente la configuración avanzada para los archivos de registro de DQS.|[Configurar las opciones avanzadas de los archivos de registro de DQS](../../2014/data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
  
## <a name="see-also"></a>Consulte también  
 [dqs, administración](../../2014/data-quality-services/dqs-administration.md)  
  
  
