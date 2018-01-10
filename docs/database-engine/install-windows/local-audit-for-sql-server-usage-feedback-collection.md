---
title: "Auditoría local para colección de comentarios sobre el uso de SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 02/28/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-security
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Local Audit
ms.assetid: a0665916-7789-4f94-9086-879275802cf3
caps.latest.revision: "8"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d1dba346ae2e2cb5f68ff93613a2f3c12729780
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="local-audit-for-sql-server-usage-feedback-collection"></a>Auditoría local para colección de comentarios sobre el uso de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
## <a name="introduction"></a>Introducción

Microsoft SQL Server contiene características habilitadas para Internet que pueden recopilar y enviar información sobre el equipo o dispositivo ("información estándar sobre equipos") a Microsoft. El componente de Auditoría local de [colección de comentarios sobre el uso de SQL Server](http://support.microsoft.com/kb/3153756) escribe los datos que recopila el servicio en una carpeta designada y que representa los datos (registros) que se enviarán a Microsoft. El propósito de la Auditoría local es permitir que los clientes vean todos los datos que Microsoft recopila con esta característica, por motivos de cumplimiento, reglamentarios o por validación de privacidad.  

Desde SQL Server 2016 CU2, Auditoría local se puede configurar a nivel de instancia para Motor de base de datos de SQL Server y Analysis Services (SSAS). En SQL Server 2016 CU4 y SQL Server 2016 SP1, la auditoría local también está habilitada para SQL Server Integration Services (SSIS). Otros componentes de SQL Server que se instalan durante la configuración y herramientas de SQL Server que se descargan o instalan después de la configuración no cuentan con la funcionalidad de Auditoría local para la colección de comentarios sobre el uso. 

## <a name="prerequisites"></a>Prerequisites 

A continuación, aparecen los requisitos previos para habilitar Auditoría local en cada instancia de SQL Server: 

1. La instancia aplica una revisión a SQL Server 2016 RTM CU2 o versión superior. 

1. El usuario debe ser un administrador del sistema o debe tener un rol con acceso para agregar y modificar una clave del Registro, crear carpetas, administrar la seguridad de las carpetas y detener e iniciar un servicio de Windows.  

## <a name="pre-configuration-steps-prior-to-turning-on-local-audit"></a>Pasos de configuración previa antes de activar la Auditoría local 

Antes de activar la Auditoría local, un administrador del sistema debe:

1. Saber el nombre de la instancia de SQL Server y la cuenta de inicio de sesión del servicio Telemetría CEIP de SQL Server. 

1. Configurar una carpeta nueva para los archivos de Auditoría local.

1. Conceder permisos a la cuenta de inicio de sesión del servicio Telemetría CEIP de SQL Server.

1. Crear una configuración de clave del Registro para configurar el directorio de destino de Auditoría local. 

    Para el Motor de base de datos e Integration Services, cree la clave en *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL14.\<INSTANCENAME\>\\CPE*. 
    
    Para Analysis Services, cree la clave en *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS14.\<INSTANCENAME\>\\CPE*.

### <a name="get-the-sql-server-ceip-service-logon-account"></a>Obtener la cuenta de inicio de sesión del servicio CEIP de SQL Server

Complete los pasos siguientes para obtener la cuenta de inicio de sesión del servicio Telemetría CEIP de SQL Server
 
1. Inicie **Servicios** : haga clic en el botón **Windows**  y escriba *services.msc*. 

2. Vaya al servicio correspondiente. Por ejemplo, para el motor de base de datos, ubique **Servicio CEIP de SQL Server \<nombre de instancia\>**. En el caso de Analysis Services, busque **CEIP de SQL Server Analysis Services \<nombre de instancia\>**. En el caso de Integration Services, busque el **servicio CEIP 13 de SQL Server Integration Services**.

3. Haga clic con el botón derecho en el servicio y elija **Propiedades**. 

4. Haga clic en la pestaña **Iniciar sesión** . La cuenta de inicio de sesión aparece en **Esta cuenta**. 

### <a name="configure-a-new-folder-for-the-local-audit-files"></a>Configurar una carpeta nueva para los archivos de Auditoría local.    

Cree una carpeta nueva (directorio de Auditoría local) donde Auditoría local escribirá los registros. Por ejemplo, la ruta de acceso completa al directorio de Auditoría local para una instancia predeterminada del motor de la base de datos sería la siguiente: *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\*. 
 
> Nota: Configurar la ruta de acceso al directorio para Auditoría local fuera de la ruta de instalación de SQL Server para evitar que permitir la funcionalidad de auditoría y la aplicación de revisiones provoquen problemas potenciales con SQL Server.

  ||Decisión de diseño|Recomendación|  
  |------|-----------------|----------|  
  |![Casilla](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Disponibilidad de espacio |En una carga de trabajo moderada con alrededor de 10 bases de datos, disponga de unos 2 MB de espacio en disco por día por instancia.|  
|![Casilla](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Directorios independientes | Cree un directorio para cada instancia. Por ejemplo, use *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\* para una instancia de SQL Server denominada `MSSQLSERVER`. Esto simplifica la administración de archivos.
|![Casilla](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Carpetas independientes |Use una carpeta específica para cada servicio. Por ejemplo, para un nombre de instancia determinado, debe tener una carpeta para el motor de base de datos. Si una instancia de SSAS usa el mismo nombre de instancia, cree una carpeta independiente para SSAS. Si tiene las instancias de Motor de base de datos y de Analysis Services configuradas en la misma carpeta, Auditoría local escribirá todo en el mismo archivo de registro desde ambas instancias.| 
|![Casilla](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Conceder permisos a la cuenta de inicio de sesión del servicio Telemetría de CIEP de SQL Server|Habilite **Mostrar el contenido de la carpeta**, Acceso de **lectura** y **escritura** a la cuenta de inicio de sesión del servicio Telemetría CEIP de SQL Server.|


### <a name="grant-permissions-to-the-sql-server-ciep-telemetry-service-logon-account"></a>Conceder permisos a la cuenta de inicio de sesión del servicio Telemetría de CIEP de SQL Server
  
1. En **Explorador de archivos**, vaya a la ubicación donde se encuentra la carpeta nueva.  

1. Haga clic con el botón derecho en la carpeta nueva y elija **Propiedades**. 

1. En la **pestaña Seguridad**, haga clic en **Editar** permiso Administrar.

1. Haga clic en **Agregar** y escriba la credencial del servicio Telemetría CEIP de SQL Server, por ejemplo, `NT Service\SQLTELEMETRY`.   

1. Haga clic en **Comprobar nombres** para validar el nombre que se proporcionó y, luego, haga clic en **Aceptar**. 

1. En el cuadro de diálogo **Permiso** , elija la cuenta de inicio de sesión en el servicio Telemetría CEIP de SQL Server y haga clic en **Mostrar el contenido de la carpeta**, **Lectura** y **Escritura**.  

1. Haga clic en **Aceptar** para aplicar de inmediato los cambios en los permisos. 
  
### <a name="create-a-registry-key-setting-to-configure-local-audit-target-directory"></a>Crear una configuración de clave del Registro para configurar el directorio de destino de Auditoría local.

1. Inicie regedit.  

1. Vaya a la ruta de CPE correspondiente. 

    Para el motor de base de datos e Integration Services, use *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL14.\<INSTANCENAME\>\\CPE*. 
    
    Para Analysis Services, use *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS14.\<INSTANCENAME\>\\CPE*.

1. Haga clic con el botón derecho en la ruta de CPE y elija **Nuevo**. Haga clic en **Valor de cadena**.

1. Ponga un nombre a la nueva clave de registro `UserRequestedLocalAuditDirectory`. 
 
## <a name="turning-local-audit-on-or-off"></a>Activar o desactivar Auditoría local

Una vez que complete los pasos de configuración previa, puede activar Auditoría local. Para ello, use una cuenta de Administrador del sistema o un rol similar con acceso para modificar las claves del Registro a fin de activar o desactivar Auditoría local con los pasos siguientes. 

1. Inicie **regedit**.  

1. Vaya a la ruta de CPE correspondiente. 

    Para el motor de base de datos e Integration Services, use *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL14.\<INSTANCENAME\>\\CPE*. 
    
    Para Analysis Services, use *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS14.\<INSTANCENAME\>\\CPE*.

1. Haga clic con el botón derecho en **UserRequestedLocalAuditDirectory** y, luego, haga clic en *Modificar*. 

1. Para activar Auditoría local, escriba la ruta de acceso a Auditoría local, por ejemplo, *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\*.
 
    Para desactivar Auditoría local, vacíe el valor en **UserRequestedLocalAuditDirectory**.

1. Cierre **regedit**. 

CEIP de SQL Server debe reconocer inmediatamente la configuración de Auditoría local si el servicio ya está en ejecución. Para iniciar el servicio CEIP de SQL Server, el administrador del sistema o alguna persona con acceso para iniciar o detener los servicios de Windows puede seguir estos pasos: 

1. Inicie la aplicación Servicios: haga clic en el botón Windows y escriba Servicios. 

1. Vaya al servicio correspondiente. 

    Para Motor de base de datos, use **Servicio CEIP de SQL Server (\<NOMBREINSTANCIA\>)**. 
    
    Para Analysis Services, use **CEIP de SQL Server Analysis Services (\<NOMBREINSTANCIA\>)**. 

1. Haga clic con el botón derecho en el servicio y elija Reiniciar. 

1. Compruebe que el estado del servicio es **En ejecución**. 

Auditoría local generará un archivo de registro al día. Los archivos de registro tendrán este formato: `<YYYY-MM-DD>.json`. Por ejemplo, *2016-07-12.json*. Si ya hay un archivo correspondiente al día en cuestión en el directorio designado, Auditoría local lo anexará a este. En caso contrario, se creará un archivo nuevo correspondiente al día. 

> Nota: Después de habilitar Auditoría local, puede demorar hasta 5 minutos en escribir el archivo de registro por primera vez. 

## <a name="maintenance"></a>Mantenimiento 

1. Para limitar el uso del espacio en disco que ocupan los archivos que escribe Auditoría local, configure una directiva o un trabajo periódico para limpiar el directorio de Auditoría local y quitar los archivos antiguos e innecesarios.  

2. Proteja la ruta de acceso al directorio de Auditoría local para que solo las personas adecuadas puedan tener acceso a él. Tenga en cuenta que los archivos de registro contienen información según lo descrito en [Cómo configurar SQL Server 2016 para enviar comentarios a Microsoft](http://support.microsoft.com/kb/3153756). El acceso a este archivo debe evitar que la mayoría de los miembros de su organización pueda leerlo.  

## <a name="data-dictionary-of-local-audit-output-data-structure"></a>Diccionario de datos de estructura de datos de salida de Auditoría local 

- Los archivos de registro de Auditoría local tienen el formato JSON y contienen un conjunto de objetos (filas) que representan puntos de datos que se envían de vuelta a Microsoft en **emitTime**.  

- Cada fila sigue un esquema específico que se identifica por **schemaVersion**.   

- Cada fila es una salida de una sesión de servicio de SQLCEIP que se identifica como **sessionID**.  

- Las filas se emiten en una secuencia que se identifica por **sequence**. 

- Cada fila de punto de datos contiene la salida de un **queryIdentifier** , que puede ser una consulta T-SQL, una sesión de XE o un mensaje relacionado con un tipo de seguimiento, identificado como **traceName**.   

- Los valores**queryIdentifiers** están agrupados y tienen versiones junto con **querySetVersion**. 

- Los valores**data** contienen la salida de la ejecución de consulta correspondiente que usó **queryTimeInTicks**. 

- Los valores**queryIdentifiers** para consultas T-SQL tienen la definición de consulta T-SQL almacenada en la consulta. 


| Jerarquía de información de Auditoría local lógica | Columnas relacionadas |
| ------ | -------|
| Encabezado | emitTime, schemaVersion 
| Máquina | hostname, domainHash, sqmID, operatingSystem 
| Instancia | instanceName, correlationID, clientVersion 
| Session | sessionID, traceName 
| Consulta | sequence, querySetVersion, queryIdentifier, query, queryTimeInTicks 
| data |  datos 

### <a name="namevalue-pairs-definition-and-examples"></a>Definición y ejemplos de pares nombre-valor 

Las columnas siguientes representan el orden de la salida de archivo de Auditoría local. Se usa un hash unidireccional con SHA 256 para anonimizar los valores para varias de las columnas siguientes.  

| Nombre | Description | Valores de ejemplo
|-------|--------| ----------|
|hostname | Nombre de la máquina anónima donde está instalado SQL Server| de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11 
|domainHash| Hash de dominio anónimo de la máquina que hospeda la instancia de SQL Server | de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11 
|sqmId |El identificador que representa la máquina donde está instalado SQL Server | 02AF58F5-753A-429C-96CD-3900E90DB990 
|NOMBREINSTANCIA| El nombre de la instancia de SQL Server anónima| e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855 
|schemaVersion| La versión del esquema de SQLCEIP |  3 
|emitTime |Hora de emisión del punto de datos en hora UTC | 2016-09-08T17:20:22.1124269Z 
|sessionID | El identificador de la sesión del servicio SQLCEIP | 89decf9a-ad11-485c-94a7-fefb3a02ed86 
| correlationId | El marcador de posición para un identificador adicional | 0 
|sequence | El número de secuencia de los puntos de datos enviados dentro de la sesión | 15 
| clientVersion | Versión de la instancia de SQL Server | 13.0.2161.3 ((SQL16_RTM_QFE-CU).160907-1223) 
| operatingSystem | La versión del sistema operativo donde está instalada la instancia de SQL Server | Microsoft Windows Server 2012 R2 Datacenter 
| querySetVersion | La versión de un grupo de definiciones de consulta | 1.0.0.0 
|traceName | Categorías de seguimientos: (SQLServerXeQueries, SQLServerPeriodicQueries, SQLServerOneSettingsException) | SQLServerPeriodicQueries 
|queryIdentifier | Un identificador de la consulta | SQLServerProperties.002 
|datos   | El resultado de la información recopilada en queryIdentifier como salida de la consulta T-SQL, la sesión de XE o la aplicación |   [{"Collation": "SQL_Latin1_General_CP1_CI_AS","SqlFTinstalled": "0" "SqlIntSec": "1","IsSingleUser": "0","SqlFilestreamMode": "0","SqlPbInstalled": "0","SqlPbNodeRole": "","SqlVersionMajor": "13","SqlVersionMinor": "0","SqlVersionBuild": "2161","ProductBuildType": "","ProductLevel": "RTM","ProductUpdateLevel": "CU2","ProductUpdateReference": "KB3182270","ProductRevision": "3","SQLEditionId": "-1534726760","IsClustered": "0","IsHadrEnabled": "0","SqlAdvAInstalled": "0","PacketReceived": "1210","Version": "Microsoft SQL Server 2016 (RTM-CU2) (KB3182270) - 13.0.2161.3 (X64) \n\tSep  7 2016 14:24:16 \n\tCopyright (c) Microsoft Corporation\n\tStandard Edition (64-bit) on Windows Server 2012 R2 Datacenter 6.3 \u003cX64\u003e (Build 9600: ) (Hypervisor)\n"}],
|Query| Si corresponde, la definición de consulta T-SQL relacionada con el identificador queryIdentifier que genera los datos.        El servicio CEIP de SQL Server no carga este componente. Solo se incluye en Auditoría local como referencia para los clientes.| SELECT\n      SERVERPROPERTY(\u0027Collation\u0027) AS [Collation],\n      SERVERPROPERTY(\u0027IsFullTextInstalled\u0027) AS [SqlFTinstalled],\n      SERVERPROPERTY(\u0027IsIntegratedSecurityOnly\u0027) AS [SqlIntSec],\n      SERVERPROPERTY(\u0027IsSingleUser\u0027) AS [IsSingleUser],\n      SERVERPROPERTY (\u0027FileStreamEffectiveLevel\u0027) AS [SqlFilestreamMode],\n      SERVERPROPERTY(\u0027IsPolybaseInstalled\u0027) AS [SqlPbInstalled],\n      SERVERPROPERTY(\u0027PolybaseRole\u0027) AS [SqlPbNodeRole],\n      SERVERPROPERTY(\u0027ProductMajorVersion\u0027) AS [SqlVersionMajor],\n      SERVERPROPERTY(\u0027ProductMinorVersion\u0027) AS [SqlVersionMinor],\n      SERVERPROPERTY(\u0027ProductBuild\u0027) AS [SqlVersionBuild],\n      SERVERPROPERTY(\u0027ProductBuildType\u0027) AS ProductBuildType,\n      SERVERPROPERTY(\u0027ProductLevel\u0027) AS ProductLevel,\n      SERVERPROPERTY(\u0027ProductUpdateLevel\u0027) AS ProductUpdateLevel,\n      SERVERPROPERTY(\u0027ProductUpdateReference\u0027) AS ProductUpdateReference,\n      RIGHT(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)),CHARINDEX(\u0027.\u0027, REVERSE(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)))) - 1) AS ProductRevision,\n      SERVERPROPERTY(\u0027EditionID\u0027) AS SQLEditionId,\n      SERVERPROPERTY(\u0027IsClustered\u0027) AS IsClustered,\n      SERVERPROPERTY(\u0027IsHadrEnabled\u0027) AS IsHadrEnabled,\n      SERVERPROPERTY(\u0027IsAdvancedAnalyticsInstalled\u0027) AS [SqlAdvAInstalled],\n      @@PACK_RECEIVED AS PacketReceived,\n      @@VERSION AS Version
|queryTimeInTicks | La duración necesaria para que se ejecute la consulta con la siguiente categoría de seguimiento: (SQLServerXeQueries, SQLServerPeriodicQueries) |  0 
 
### <a name="trace-categories"></a>Categorías de seguimiento 
Actualmente recopilamos las siguientes categorías de seguimiento: 

- **SQLServerXeQueries**: contiene puntos de datos recopilados a través de una sesión de eventos extendidos. 

- **SQLServerPeriodicQueries**: contiene puntos de datos recopilados a través de consultas periódicas ejecutadas en una instancia de SQL Server. 

- **SQLServerPerDBPeriodicQueries**: contiene puntos de datos recopilados a través de consultas periódicas ejecutadas en hasta 30 bases de datos en una instancia de SQL Server. 

- **SQLServerOneSettingsException**: contiene mensajes de excepción relacionados con la actualización de un esquema o un conjunto de consultas. 

- **DigitalProductID**: contiene puntos de datos para agregar el id. de producto digital con hash anónimo (SHA-256) de instancias de SQL Server. 

### <a name="local-audit-file-examples"></a>Ejemplos de archivos de Auditoría local



A continuación, aparece un fragmento de una salida de archivo JSON de Auditoría local.

```JSON
{
    "hostName": "de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11",
    "domainHash": "de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11",
    "sqmId": "02AF58F5-753A-429C-96CD-3900E90DB990",
    "instanceName": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
    "schemaVersion": "3",
    "emitTime": "2016-09-08T17:20:22.1124269Z",
    "sessionId": "89decf9a-ad11-485c-94a7-fefb3a02ed86",
    "correlationId": 0,
    "sequence": 15,
    "clientVersion": "13.0.2161.3 ((SQL16_RTM_QFE-CU).160907-1223)",
    "operatingSystem": "Microsoft Windows Server 2012 R2 Datacenter",
    "querySetVersion": "1.0.0.0",
    "traceName": "SQLServerPeriodicQueries",
    "queryIdentifier": "SQLServerProperties.002",
    "data": [
      {
        "Collation": "SQL_Latin1_General_CP1_CI_AS",
        "SqlFTinstalled": "0",
        "SqlIntSec": "1",
        "IsSingleUser": "0",
        "SqlFilestreamMode": "0",
        "SqlPbInstalled": "0",
        "SqlPbNodeRole": "",
        "SqlVersionMajor": "13",
        "SqlVersionMinor": "0",
        "SqlVersionBuild": "2161",
        "ProductBuildType": "",
        "ProductLevel": "RTM",
        "ProductUpdateLevel": "CU2",
        "ProductUpdateReference": "KB3182270",
        "ProductRevision": "3",
        "SQLEditionId": "-1534726760",
        "IsClustered": "0",
        "IsHadrEnabled": "0",
        "SqlAdvAInstalled": "0",
        "PacketReceived": "1210",
        "Version": "Microsoft SQL Server 2016 (RTM-CU2) (KB3182270) - 13.0.2161.3 (X64) \n\tSep  7 2016 14:24:16 \n\tCopyright (c) Microsoft Corporation\n\tStandard Edition (64-bit) on Windows Server 2012 R2 Datacenter 6.3 \u003cX64\u003e (Build 9600: ) (Hypervisor)\n"
      }
    ],
    "query": "SELECT\n      SERVERPROPERTY(\u0027Collation\u0027) AS [Collation],\n      SERVERPROPERTY(\u0027IsFullTextInstalled\u0027) AS [SqlFTinstalled],\n      SERVERPROPERTY(\u0027IsIntegratedSecurityOnly\u0027) AS [SqlIntSec],\n      SERVERPROPERTY(\u0027IsSingleUser\u0027) AS [IsSingleUser],\n      SERVERPROPERTY (\u0027FileStreamEffectiveLevel\u0027) AS [SqlFilestreamMode],\n      SERVERPROPERTY(\u0027IsPolybaseInstalled\u0027) AS [SqlPbInstalled],\n      SERVERPROPERTY(\u0027PolybaseRole\u0027) AS [SqlPbNodeRole],\n      SERVERPROPERTY(\u0027ProductMajorVersion\u0027) AS [SqlVersionMajor],\n      SERVERPROPERTY(\u0027ProductMinorVersion\u0027) AS [SqlVersionMinor],\n      SERVERPROPERTY(\u0027ProductBuild\u0027) AS [SqlVersionBuild],\n      SERVERPROPERTY(\u0027ProductBuildType\u0027) AS ProductBuildType,\n      SERVERPROPERTY(\u0027ProductLevel\u0027) AS ProductLevel,\n      SERVERPROPERTY(\u0027ProductUpdateLevel\u0027) AS ProductUpdateLevel,\n      SERVERPROPERTY(\u0027ProductUpdateReference\u0027) AS ProductUpdateReference,\n      RIGHT(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)),CHARINDEX(\u0027.\u0027, REVERSE(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)))) - 1) AS ProductRevision,\n      SERVERPROPERTY(\u0027EditionID\u0027) AS SQLEditionId,\n      SERVERPROPERTY(\u0027IsClustered\u0027) AS IsClustered,\n      SERVERPROPERTY(\u0027IsHadrEnabled\u0027) AS IsHadrEnabled,\n      SERVERPROPERTY(\u0027IsAdvancedAnalyticsInstalled\u0027) AS [SqlAdvAInstalled],\n      @@PACK_RECEIVED AS PacketReceived,\n      @@VERSION AS Version",
    "queryTimeInTicks": 0
  } ,
  {
    "hostName": "de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11",
    "domainHash": "de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11",
    "sqmId": "02AF58F5-753A-429C-96CD-3900E90DB990",
    "instanceName": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
    "schemaVersion": "3",
    "emitTime": "2016-09-08T17:20:24.9819144Z",
    "sessionId": "89decf9a-ad11-485c-94a7-fefb3a02ed86",
    "correlationId": 0,
    "sequence": 61,
    "clientVersion": "13.0.2161.3 ((SQL16_RTM_QFE-CU).160907-1223)",
    "operatingSystem": "Microsoft Windows Server 2012 R2 Datacenter",
    "querySetVersion": "1.0.0.0",
    "traceName": "SQLServerPeriodicQueries",
    "queryIdentifier": "ExternalScriptStats.001",
    "data": [
      {
        "counter_name": "Total Executions                                                                                                                ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Parallel Executions                                                                                                             ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Streaming Executions                                                                                                            ",
        "cntr_value": "0"
      },
      {
        "counter_name": "SQL CC Executions                                                                                                               ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Implied Auth. Logins                                                                                                            ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Total Execution Time (ms)                                                                                                       ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Execution Errors                                                                                                                ",
        "cntr_value": "0"
      }
    ],  
    "query": "select counter_name, cntr_value from sys.dm_os_performance_counters where object_name like \u0027%External Scripts%\u0027",
    "queryTimeInTicks": 155834
  } 
```
## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

**¿De qué manera los administradores de bases de datos leen los archivos de registro de Auditoría local?**
Estos archivos de registro están escritos en formato JSON. Cada línea será un objeto JSON que representa parte de la telemetría que se cargó a Microsoft. Los nombres de los campos deben ser claros. 

**¿Qué ocurre si el administrador de base de datos deshabilita Colección de comentarios sobre el uso?**
No se escribirá ningún archivo de Auditoría local. 

**¿Qué ocurre si no hay conectividad a Internet o si la máquina está detrás de un firewall?**
No se enviarán comentarios sobre el uso de SQL Server 2016 a Microsoft. De todos modos, se intentarían escribir los registros de Auditoría local si la configuración es correcta.

**¿De qué manera los administradores de bases de datos deshabilitan Auditoría local?**
Deshabilitan la entrada de la clave del Registro UserRequestedLocalAuditDirectory.

**¿Quiénes pueden leer los archivos de registro de Auditoría local?**
Cualquier persona de la organización que cuente con acceso al directorio de Auditoría local.

**¿De qué manera los administradores de bases de datos administran los archivos de registro escritos en el directorio designado?**
Los administradores de bases de datos deberán administrar automáticamente la limpieza de los archivos del directorio para evitar que se use demasiado espacio en disco.

**¿Existe algún cliente o herramienta que se pueda usar para leer esta salida JSON?**
Es posible leer la entrada con el Bloc de notas, Visual Studio o cualquier lector de JSON de su preferencia.
De manera alternativa, puede leer el archivo JSON y analizar los datos de una instancia de SQL Server 2016 como se muestra a continuación. Para más detalles sobre cómo leer un archivo JSON en SQL Server, visite [Importing JSON files into SQL Server using OPENROWSET (BULK) and OPENJSON (Transact-SQL)](http://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/10/07/bulk-importing-json-files-into-sql-server/)(Importación de archivos JSON a SQL Server con OPENROWSET [BULK] y OPENJSON [Transact-SQL]).

```Transact-SQL
DECLARE @JSONFile AS VARCHAR(MAX)

-- Read the JSON file into variable 
SELECT @JSONFile = BulkColumn 
FROM OPENROWSET (BULK 'C:\SQLCEIPAudit\MSSQLSERVER\2016-09-08.json', SINGLE_CLOB) MyFile 

-- Check if the JSON file has been read properly and if it's in a JSON format
SELECT 
    @JSONFile LocalAuditOutput, 
    ISJSON(@JSONFile) IsFileInJSONFormat

-- Get the query identifier, query and the data (output of the query)   
SELECT 
    sequence,
    queryIdentifier,
    query,
    data
FROM OPENJSON(@JSONFile) 
    WITH (sessionId VARCHAR(64)
         ,sequence INT
         ,queryIdentifier VARCHAR(128)
         ,query VARCHAR(MAX)
         ,data NVARCHAR(MAX) AS JSON)
-- Get specific details about the output of "DatabaseProperties.001" query  
SELECT 
    QueryIdentifier,
    DatabaseID,
    CompatibilityLevel,
    IsQueryStoreOn
FROM OPENJSON(@JSONFile) 
    WITH (sessionId VARCHAR(64)
         ,sequence INT
         ,queryIdentifier VARCHAR(128)
         ,query VARCHAR(MAX)
         ,data NVARCHAR(MAX) AS JSON) 
    CROSS APPLY OPENJSON(data) 
        WITH (   DatabaseID varchar(128) '$.database_id'
                ,CompatibilityLevel varchar(128) '$.compatibility_level'
                ,IsQueryStoreOn varchar(128) '$.QS'
             )
WHERE queryIdentifier = 'DatabaseProperties.001'
```

## <a name="see-also"></a>Ver también
[Auditoría local para colección de comentarios sobre el uso de SSMS](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-telemetry-ssms)

