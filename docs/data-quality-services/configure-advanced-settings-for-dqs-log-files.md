---
title: Configurar las opciones avanzadas de los archivos de registro de DQS | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- log files,advanced settings
- dqs log files,advanced settings
ms.assetid: 1d565748-9759-425c-ae38-4d2032a86868
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9f87f2bc3329122a441906cec5bcf164d2743fa9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770203"
---
# <a name="configure-advanced-settings-for-dqs-log-files"></a>Configurar las opciones avanzadas de los archivos de registro de DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo realizar la configuración avanzada para los archivos de registro de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] y [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , como configurar el límite de tamaño del archivo gradual de los archivos de registro, establecer el patrón de marca de tiempo de los eventos, etc.  
  
> [!NOTE]  
>  Estas actividades no se pueden realizar mediante [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], y están dirigidas exclusivamente a los usuarios expertos.  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
  
-   La cuenta de usuario de Windows debe ser miembro del rol fijo de servidor sysadmin en la instancia de SQL Server para modificar la configuración de la tabla A_CONFIGURATION de la base de datos DQS_MAIN.  
  
-   Debe haber iniciado sesión como miembro del grupo Administradores en el equipo donde está modificando el archivo DQLog.Client.xml para configurar los valores de registro de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] .  
  
##  <a name="DQSServer"></a> Configurar los valores de registro de Data Quality Server  
 Los valores de registro de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] se encuentran en formato XML en la columna **VALUE** de la fila **ServerLogging** de la tabla A_CONFIGURATION de la base de datos DQS_MAIN. Puede ejecutar la consulta SQL siguiente para ver la información de configuración:  
  
```  
select * from DQS_MAIN.dbo.A_CONFIGURATION where NAME='ServerLogging'  
```  
  
 Debe actualizar la información correspondiente en la columna **VALUE** de la fila **ServerLogging** para cambiar la configuración del registro de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] . En este ejemplo, actualizaremos los valores de registro de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] para establecer el límite de tamaño del archivo gradual en 25000 kB (el valor predeterminado es 20000 kB).  
  
1.  Inicie Microsoft SQL Server Management Studio y conéctese a la instancia adecuada de SQL Server.  
  
2.  En el Explorador de objetos, haga clic con el botón secundario en el servidor y, a continuación, haga clic en **Nueva consulta**.  
  
3.  En la ventana del editor de consultas, copie las instrucciones SQL siguientes:  
  
    ```  
    -- Begin the transaction.  
    BEGIN TRAN  
    GO  
    -- set the XML value field for the row with name=ServerLogging  
    update DQS_MAIN.dbo.A_CONFIGURATION   
    set VALUE='<configuration>  
      <configSections>  
        <section name="loggingConfiguration" type="Microsoft.Practices.EnterpriseLibrary.Logging.Configuration.LoggingSettings, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" />  
      </configSections>  
      <loggingConfiguration name="Logging Application Block" tracingEnabled="true" defaultCategory="" logWarningsWhenNoCategoriesMatch="true">  
        <listeners>  
          <add fileName="###REPLACE_THIS_WITH_SQL_SERVER_INSTANCE_LOG_FOLDER_NAME###DQServerLog.###REPLACE_THIS_WITH_SQL_CATALOG_NAME###.log" footer="" formatter="Custom Text Formatter" header="" rollFileExistsBehavior="Increment" rollInterval="None" rollSizeKB="25000" timeStampPattern="yyyy-MM-dd" listenerDataType="Microsoft.Practices.EnterpriseLibrary.Logging.Configuration.RollingFlatFileTraceListenerData, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" traceOutputOptions="None" filter="All" type="Microsoft.Practices.EnterpriseLibrary.Logging.TraceListeners.RollingFlatFileTraceListener, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="Rolling Flat File Trace Listener" />  
        </listeners>  
        <formatters>  
          <add template="{timestamp(local)}|[{threadName}]|{dictionary({value}|)}{message}" type="Microsoft.Practices.EnterpriseLibrary.Logging.Formatters.TextFormatter, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="Custom Text Formatter" />  
        </formatters>  
        <logFilters>  
          <add enabled="true" type="Microsoft.Practices.EnterpriseLibrary.Logging.Filters.LogEnabledFilter, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="LogEnabled Filter" />  
        </logFilters>  
        <categorySources />  
        <specialSources>  
          <allEvents switchValue="All" name="All Events" />  
          <notProcessed switchValue="All" name="Unprocessed Category" />  
          <errors switchValue="All" name="Logging Errors & Warnings">  
            <listeners>  
              <add name="Rolling Flat File Trace Listener" />  
            </listeners>  
          </errors>  
        </specialSources>  
      </loggingConfiguration>  
    </configuration>'  
    WHERE NAME='ServerLogging'  
    GO  
    -- check the result  
    select * from DQS_MAIN.dbo.A_CONFIGURATION where NAME='ServerLogging'  
  
    -- Commit the transaction.  
    COMMIT TRAN  
  
    ```  
  
4.  Presione F5 para ejecutar las instrucciones. Vea el panel **Resultados** para comprobar que las instrucciones se han ejecutado correctamente.  
  
5.  Para aplicar los cambios realizados en la configuración de registro de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] , debe ejecutar las instrucciones Transact-SQL siguientes. Abra una nueva ventana del editor de consultas y pegue las instrucciones Transact-SQL siguientes:  
  
    ```  
    USE [DQS_MAIN]  
    GO  
    DECLARE @return_value int  
    EXEC @return_value = [internal_core].[RefreshLogSettings]  
    SELECT 'Return Value' = @return_value  
    GO  
  
    ```  
  
6.  Presione F5 para ejecutar las instrucciones. Vea el panel **Resultados** para comprobar que las instrucciones se han ejecutado correctamente.  
  
> [!NOTE]  
>  La configuración de registro de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] se genera y se almacena dinámicamente en el archivo DQS_MAIN.Log, que normalmente se encuentra en C:\Archivos de programa\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log si ha instalado la instancia predeterminada de SQL Server. Sin embargo, los cambios realizados directamente en este archivo no se conservan, y serán reemplazados por la configuración de la tabla A_CONFIGURATION de la base de datos DQS_MAIN.  
  
##  <a name="DQSClient"></a> Configurar los valores de registro de Data Quality Client  
 El archivo de configuración de los valores de registro de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , DQLog.Client.xml, suele estar disponible en C:\Archivos de programa\Microsoft SQL Server\130\Tools\Binn\DQ\config. El contenido del archivo XML es similar al del archivo XML que modificó con anterioridad para los valores de configuración del registro de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] . Para configurar los valores de registro de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] :  
  
1.  Ejecute cualquier herramienta de edición de XML o el Bloc de notas como administrador.  
  
2.  Abra el archivo DQLog.Client.xml en la herramienta o en el Bloc de notas.  
  
3.  Realice los cambios necesarios y guarde el archivo para aplicarlos.  
  
## <a name="see-also"></a>Ver también  
 [Configurar los niveles de gravedad de los archivos de registro de DQS](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)  
  
  
