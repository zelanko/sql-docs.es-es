---
title: Trabajar con Oracle CDC Service | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 04be5896-2301-45f5-a8ce-5f4ef2b69aa5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ae456229482288e2fcf5e27f822e4f6f11540930
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749987"
---
# <a name="working-with-the-oracle-cdc-service"></a>Trabajar con el servicio CDC de Oracle
  En esta sección se describen algunos conceptos importantes del servicio CDC de Oracle. Los conceptos incluidos en esta sección son:  
  
-   [La base de datos MSXDBCDC](#BKMK_MSXDBCDC)  
  
     En esta sección se describen las tablas incluidas en esta base de datos y su importancia para CDC.  
  
-   [Las bases de datos CDC](#BKMK_CDCdatabas)  
  
     En esta sección se proporciona una breve descripción de las bases de datos CDC. Estas bases de datos se crean mediante la Consola del diseñador CDC de Oracle. Vea la documentación incluida con la instalación de la Consola del diseñador CDC para obtener más información acerca de las bases de datos CDC.  
  
-   [Usar la línea de comandos para configurar el servicio CDC](#BKMK_CommandConfigCDC)  
  
     En esta sección se describen los comandos de la línea de comandos que se pueden usar para configurar el servicio CDC de Oracle.  
  
##  <a name="BKMK_MSXDBCDC"></a> La base de datos MSXDBCDC  
 MSXDBCDC (Microsoft External-Database CDC) es una base de datos especial que se necesita cuando se usa el servicio CDC para Oracle con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 El nombre de esta base de datos no se puede cambiar. Si existe una base de datos denominada MSXDBCDC en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del host y contiene tablas distintas de las definidas por el servicio CDC para Oracle, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del host no se puede usar.  
  
 Los usos principales de esta base de datos son los siguientes:  
  
-   Sirve como registro de los servicios CDC de Oracle asociados a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esta información se usa para los componentes de configuración y diseño del servicio, y para admitir la coordinación de varios servicios CDC con el mismo nombre en distintos nodos por encima del cual está el activo.  
  
-   Sirve como registro de las instancias CDC de Oracle contenidas en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el servicio CDC que controla cada instancia y la versión de configuración que usa cada una. Esta información es equivalente a la columna **is_cdc_enabled** de la tabla **sys.databases** de la base de datos maestra. El servicio CDC examina periódicamente la tabla **dbo.xdbcdc_databases** para identificar los cambios realizados en la configuración de CDC o en la lista de instancias capturadas.  
  
-   Contiene procedimientos almacenados propiedad de **sysadmin**que ayudan a crear y mantener las instancias CDC. Son similares a los procedimientos del sistema que se emplean para la implementación de la característica CDC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="creating-the-msxdbcdc-database"></a>Crear la base de datos MSXDBCDC  
 Se debe crear una base de datos MSXDBCDC antes de que se pueda definir el servicio CDC de Oracle. Solo puede crear una base de datos MSXDBCDC en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La base de datos MSXDBCDC se crea al preparar una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para CDC de Oracle. Se puede crear mediante la Consola de configuración del servicio CDC de Oracle o ejecutando un script de creación generado por dicha consola.  
  
 El propietario de esta base de datos es el administrador del servicio CDC de Oracle, que puede controlar todas las instancias CDC de Oracle hospedadas en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Vea también:**  
  
 [Cómo preparar SQL Server para CDC](prepare-sql-server-for-cdc.md)  
  
### <a name="the-msxdbcdc-database-tables"></a>Las tablas de la base de datos MSXDBCDC  
 En esta sección se describen las siguientes tablas de la base de datos MSXDBCDC.  
  
-   [dbo.xdbcdc_trace](#BKMK_dboxdbcdc_trace)  
  
-   [dbo.xdbcdc_databases](#BKMK_dboxdbcdc_databases)  
  
-   [dbo.xdbcdc_services](#BKMK_dboxdbcdc_services)  
  
###  <a name="BKMK_dboxdbcdc_trace"></a> dbo.xdbcdc_trace  
 Esta tabla almacena información de seguimiento del servicio CDC de Oracle. La información almacenada en esta tabla incluye cambios importantes de estado y registros de seguimiento.  
  
 El servicio CDC de Oracle escribe los registros de errores y algunos registros de información tanto en el registro de eventos de Windows como en la tabla de seguimiento. En algunos casos la tabla de seguimiento quizás no sea accesible, en cuyo caso la información de error será accesible desde el registro de eventos.  
  
 A continuación se describen los elementos incluidos en la tabla **dbo.xdbcdc_trace** .  
  
|Elemento|Descripción|  
|----------|-----------------|  
|TIMESTAMP|Marca de tiempo UTC exacta en que se escribió el registro de seguimiento.|  
|tipo|Contiene uno de los valores siguientes.<br /><br /> error<br /><br /> INFO<br /><br /> seguimiento|  
|Nodo|Nombre del nodo en el que se escribió el registro.|  
|status|Código de estado usado por la tabla de estado.|  
|sub_status|Código de subestado usado por la tabla de estado.|  
|status_message|Mensaje de estado usado por la tabla de estado.|  
|origen|Nombre del componente CDC de Oracle que produjo el registro de seguimiento.|  
|text_data|Datos de texto adicionales para aquellos casos en los que el registro de errores o de seguimiento contiene una carga de texto.|  
|binary_data|Datos binarios adicionales para aquellos casos en los que el registro de errores o de seguimiento contiene una carga binaria.|  
  
 La instancia CDC de Oracle eliminará las filas antiguas de la tabla de seguimiento según la directiva de retención de las tablas de cambios.  
  
###  <a name="BKMK_dboxdbcdc_databases"></a> dbo.xdbcdc_databases  
 Esta tabla contiene los nombres de las bases de datos CDC del servicio CDC para Oracle en la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cada base de datos corresponde a una instancia CDC de Oracle. El servicio CDC de Oracle usa esta tabla para determinar qué instancias se deben iniciar o detener y para qué instancias hay que cambiar la configuración.  
  
 En la tabla siguiente se describen los elementos incluidos en la tabla **dbo.xdbcdc_databases** .  
  
|Elemento|Descripción|  
|----------|-----------------|  
|NAME|Nombre de la base de datos de Oracle en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|config_version|Marca de tiempo (UTC) del último cambio en la tabla **xdbcdc_config** de la base de datos CDC correspondiente o marca de tiempo (UTC) de la fila actual de esta tabla.<br /><br /> El desencadenador UPDATE aplica un valor GETUTCDATE() para este elemento. **config_version** permite al servicio CDC identificar la instancia CDC que hay que comprobar para ver si hay un cambio de configuración o para ver si está habilitada/deshabilitada.|  
|cdc_service_name|Este elemento determina qué servicio CDC de Oracle controla la base de datos de Oracle seleccionada.|  
|enabled|Indica si la instancia CDC de Oracle está activa (1) o deshabilitada (0). Cuando el servicio CDC de Oracle se inicia, solo se inician las instancias marcadas como habilitadas (1).<br /><br /> **Nota**: Una instancia CDC de Oracle puede deshabilitarse debido a un error que no se puede reintentar. En este caso, la instancia se debe reiniciar manualmente después de que se resuelva el error.|  
  
###  <a name="BKMK_dboxdbcdc_services"></a> dbo.xdbcdc_services  
 Esta tabla enumera los servicios CDC asociados a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del host. La Consola del diseñador CDC emplea esta tabla para determinar la lista de servicios CDC configurados para la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . También la usa el servicio CDC para asegurarse de que solo un servicio de Windows en ejecución administra un nombre dado de servicio CDC de Oracle.  
  
 A continuación se describen los elementos de estado de captura que se incluyen en la tabla **dbo.xdbcdc_databases** .  
  
|Elemento|Descripción|  
|----------|-----------------|  
|cdc_service_name|Nombre del servicio CDC de Oracle (el nombre del servicio de Windows).|  
|cdc_service_sql_login|Nombre del inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado por el servicio CDC de Oracle para conectar con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Un nuevo usuario de SQL denominado cdc_service se crea y asocia a este nombre de inicio de sesión, y después se agrega como miembro de los roles fijos de base de datos db_ddladmin, db_datareader y db_datawriter para cada base de datos CDC administrada por el servicio.|  
|ref_count|Este elemento cuenta el número de equipos donde está instalado el mismo servicio CDC de Oracle. Se incrementa con cada adición de un servicio CDC de Oracle con el mismo nombre y disminuye cuando se quita un servicio. Cuando el contador llega a cero, se elimina esta fila.|  
|active_service_node|Nombre del nodo de Windows que controla actualmente el servicio CDC. Cuando el servicio se detiene correctamente, esta columna se establece en NULL, lo que indica que ya no hay un servicio activo.|  
|active_service_heartbeat|Este elemento hace un seguimiento del servicio CDC actual para determinar si sigue estando activo.<br /><br /> Este elemento se actualiza periódicamente con la marca de tiempo UTC actual de la base de datos para el servicio CDC activo. El intervalo predeterminado es de 30 segundos, aunque se puede configurar.<br /><br /> Cuando un servicio CDC pendiente detecta que el latido no se actualizó una vez transcurrido el intervalo configurado, el servicio pendiente intenta asumir el rol del servicio CDC activo.|  
|opciones|Este elemento especifica las opciones secundarias, como el seguimiento o la optimización. Se escribe con el formato **nombre[=valor][; ]**. La cadena de opciones emplea la misma semántica que la cadena de conexión ODBC. Si la opción es booleana (con un valor de sí/no), el valor solo puede incluir el nombre.<br /><br /> Trace tiene los siguientes valores posibles:<br /><br /> true<br /><br /> on<br /><br /> false<br /><br /> off<br /><br /> \<nombre de clase > [, nombre de clase >]<br /><br /> El valor predeterminado es **false**.<br /><br /> <br /><br /> **service_heartbeat_interval** es el intervalo de tiempo (en segundos) para que el servicio actualice la columna active_service_heartbeat. El valor predeterminado es **30**. El valor máximo es **3600**.<br /><br /> **service_config_polling_interval** es el intervalo de sondeo (en segundos) para que el servicio CDC compruebe si hay cambios de configuración. El valor predeterminado es **30**. El valor máximo es **3600**.<br /><br /> **sql_command_timeout** es el tiempo de espera de comandos que funciona con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El valor predeterminado es **1**. El valor máximo es **3600**.|  
||  
  
### <a name="the-msxdbcdc-database-stored-procedures"></a>Los procedimientos almacenados de la base de datos MSXDBCDC  
 En esta sección se describen los siguientes procedimientos almacenados de la base de datos MSXDBCDC.  
  
-   [dbo.xcbcdc_reset_db(Database Name)](#BKMK_dboxcbcdc_reset_db)  
  
-   [dbo.xdbcdc_disable_db(dbname)](#BKMK_dboxdbcdc_disable_db)  
  
-   [dbo.xcbcdc_add_service(svcname,sqlusr)](#BKMK_dboxcbcdc_add_service)  
  
-   [dbo.xdbcdc_start(dbname)](#BKMK_dboxdbcdc_start)  
  
-   [dbo.xdbcdc_stop(dbname)](#BKMK_dboxdbcdc_stop)  
  
###  <a name="BKMK_dboxcbcdc_reset_db"></a> dbo.xcbcdc_reset_db(Database Name)  
 Este procedimiento borra los datos de una instancia CDC de Oracle. Se usa:  
  
-   Para reiniciar la captura de datos omitiendo datos anteriores, por ejemplo después de la recuperación de la base de datos de origen o después de un período de inactividad en el que no están disponibles algunos registros de transacciones de Oracle.  
  
-   Cuando hay daños en el estado CDC (concretamente, en los datos de las tablas cdc.*).  
  
 El procedimiento **dbo.xcbcdc_reset_db** realiza las tareas siguientes:  
  
-   Detiene la instancia CDC (si está activa).  
  
-   Trunca las tablas de cambios, la tabla **cdc_lsn_mapping** y la tabla **cdc_ddl_history** .  
  
-   Borra la tabla **cdc_xdbcdc_state** .  
  
-   Borra la columna start_lsn para cada fila de **cdc_change_table**.  
  
 Para poder usar el procedimiento **dbo.xcbcdc_reset_db** , el usuario debe ser miembro del rol de base de datos **db_owner** para la base de datos de la instancia CDC indicada, o debe ser miembro del rol fijo de servidor **sysadmin** o **serveradmin** .  
  
 Para más información sobre las tablas CDC, vea *Las bases de datos CDC* en el sistema de Ayuda de la Consola del diseñador CDC.  
  
###  <a name="BKMK_dboxdbcdc_disable_db"></a> dbo.xdbcdc_disable_db(dbname)  
 El procedimiento **dbo.xcbcdc_disable_db** realiza la tarea siguiente:  
  
-   Quita la entrada para la base de datos CDC seleccionada de la tabla MSXDBCDC.xdbcdc_databases.  
  
 Para poder usar el procedimiento **dbo.xcbcdc_disable_db** , el usuario debe ser miembro del rol de base de datos **db_owner** para la instancia CDC indicada, o debe ser miembro del rol fijo de servidor **sysadmin** o **serveradmin** .  
  
 Para obtener más información acerca de las tablas CDC, vea Las bases de datos CDC en el sistema de Ayuda de la Consola del diseñador CDC.  
  
###  <a name="BKMK_dboxcbcdc_add_service"></a> dbo.xcbcdc_add_service(svcname,sqlusr)  
 El procedimiento **dbo.xcbcdc_add_service** agrega una entrada a la tabla **MSXDBCDC.xdbcdc_services** y agrega un incremento de uno a la columna ref_count para el nombre del servicio en la tabla **MSXDBCDC.xdbcdc_services** . Cuando **ref_count** es 0, se elimina la fila.  
  
 Para poder usar el procedimiento **dbo.xcbcdc_add_service\<service name, username>**, el usuario debe ser miembro del rol de base de datos **db_owner** para la base de datos de la instancia CDC indicada, o debe ser miembro del rol fijo de servidor **sysadmin** o **serveradmin**.  
  
###  <a name="BKMK_dboxdbcdc_start"></a> dbo.xdbcdc_start(dbname)  
 El procedimiento **dbo.xdbcdc_start** envía una solicitud de inicio al servicio CDC que controla la instancia CDC seleccionada para que inicie el procesamiento de cambios.  
  
 Para poder usar el procedimiento **dbo.xcdcdc_start** , el usuario debe ser miembro del rol de base de datos **db_owner** para la base de datos CDC, o debe ser miembro de los roles **sysadmin** o **serveradmin** para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
###  <a name="BKMK_dboxdbcdc_stop"></a> dbo.xdbcdc_stop(dbname)  
 El procedimiento **dbo.xdbcdc_stop** envía una solicitud de detención al servicio CDC que controla la instancia CDC seleccionada para que detenga el procesamiento de cambios.  
  
 Para poder usar el procedimiento **dbo.xcdcdc_stop** , el usuario debe ser miembro del rol de base de datos **db_owner** para la base de datos CDC, o debe ser miembro de los roles **sysadmin** o **serveradmin** para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="BKMK_CDCdatabase"></a> Las bases de datos CDC  
 Cada instancia CDC de Oracle empleada en un servicio CDC está asociada a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] específica denominada la base de datos CDC. Esta base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se hospeda en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asociada al servicio CDC de Oracle.  
  
 La base de datos CDC contiene un esquema cdc especial. El servicio CDC de Oracle usa este esquema con nombres de tabla con el prefijo **xdbcdc_**. Este esquema se emplea por seguridad y coherencia.  
  
 Tanto la instancia CDC de Oracle como las bases de datos CDC se crean mediante la Consola del diseñador CDC de Oracle. Para obtener más información acerca de las bases de datos CDC, vea la documentación incluida con la instalación de la Consola del diseñador CDC de Oracle.  
  
##  <a name="BKMK_CommandConfigCDC"></a> Usar la línea de comandos para configurar el servicio CDC  
 Puede usar el programa de servicio CDC de Oracle (xdbcdcsvc.exe) desde la línea de comandos. El programa de servicio CDC es un archivo ejecutable de 32 bits y 64 bits nativo de Windows.  
  
 **Vea también**  
  
 [Cómo usar la interfaz de línea de comandos del servicio CDC](how-to-use-the-cdc-service-command-line-interface.md)  
  
### <a name="service-program-commands"></a>Comandos del programa de servicio  
 En esta sección se describen los siguientes comandos que se usan para configurar el servicio CDC.  
  
-   [Config](#BKMK_config)  
  
-   [Crear](#BKMK_create)  
  
-   [Delete](#BKMK_delete)  
  
###  <a name="BKMK_config"></a> Config  
 Use `Config` para actualizar una configuración del servicio CDC de Oracle desde un script. El comando se puede usar para actualizar únicamente determinadas partes de la configuración del servicio CDC (por ejemplo, solo la cadena de conexión sin conocer la contraseña de la clave asimétrica). El comando debe ser ejecutado por un administrador del equipo. A continuación se muestra un ejemplo del comando `Config` .  
  
```  
"<path>xdbcdcsvc.exe" config  
     <cdc-service-name>  
     [connect= <sql-server-connection-string>]  
     [key= <asym-key-password>]  
     [svcacct= <windows-account> <windows-password>]  
     [sqlacct= <sql-username> <sql-password>]  
  
```  
  
 Donde:  
  
 **cdc-service-name** es el nombre del servicio CDC que se va a actualizar. Es un parámetro obligatorio.  
  
 **sql-server-connection-string** es la cadena de conexión que se va a actualizar. Si la cadena de conexión contiene espacios en blanco o comillas, se debe escribir entre comillas dobles ("). Las comillas incrustadas se convierten duplicando las comillas.  
  
 **asym-key-password** es la contraseña que se va a actualizar.  
  
 **windows-account**y **windows-password** son las credenciales de la cuenta de Windows para el servicio que se está actualizando.  
  
 **sql-username**y **sql-password** son las credenciales de autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se están actualizando. Si sqlacct tiene un nombre de usuario vacío y una contraseña vacía, el servicio CDC de Oracle conectará con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la autenticación de Windows.  
  
 **Nota**: Los parámetros que contienen espacios o comillas dobles se deben escribir entre comillas dobles ("). Las comillas dobles incrustadas se deben duplicar (por ejemplo, para usar **"A#B" D** como contraseña debe escribir **""A#B"" D"**).  
  
###  <a name="BKMK_create"></a> Crear  
 Use `Create` para crear un servicio CDC de Oracle desde un script. El comando debe ser ejecutado por un administrador del equipo. A continuación se muestra un ejemplo del comando `Create` :  
  
```  
"<path>xdbcdcsvc.exe" create  
     <cdc-service-name>  
     [connect= "<sql-server-connection-string>"]  
     [key= <asym-key-password>]  
     [svcacct <windows-account> <windows-password>]  
     [sqlacct <sql-username> <sql-password>]  
```  
  
 Donde:  
  
 **cdc-service-name** es el nombre del servicio recién creado. Si ya hay un servicio con este nombre, el programa devuelve un error. No debe usar nombres largos ni nombres con espacios en blanco. Los caracteres "/" y "\\" no son válidos en los nombres de servicio. Es un parámetro obligatorio.  
  
 **sql-server-connection-string** es la cadena de conexión que se usará para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está asociada al nuevo servicio CDC de Oracle.  
  
 **asym-key-password** es la contraseña que protege la clave asimétrica empleada para almacenar las credenciales de minería de registros de la base de datos de origen.  
  
 **windows-account**y **windows-password** son el nombre de cuenta y la contraseña asociados al servicio CDC de Oracle que se está creando.  
  
 **sql-username**y **sql-password** son el nombre de cuenta y la contraseña de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usados para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si ambos parámetros están vacíos, el servicio CDC para Oracle conectará con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la autenticación de Windows.  
  
 **Nota**: Los parámetros que contienen espacios o comillas dobles se deben escribir entre comillas dobles ("). Las comillas dobles incrustadas se deben duplicar (por ejemplo, para usar **"A#B" D** como contraseña debe escribir **""A#B"" D"**).  
  
###  <a name="BKMK_delete"></a> Delete  
 Use `Delete` para eliminar correctamente el servicio CDC de Oracle desde un script. Este comando debe ser ejecutado por un administrador del equipo. A continuación se muestra un ejemplo del comando `Delete` .  
  
```  
"<path>xdbcdcsvc.exe" delete  
    <cdc-service-name>  
  
```  
  
 Donde:  
  
 **cdc-service-name** es el nombre del servicio CDC que se va a eliminar.  
  
 **Nota**: Los parámetros que contienen espacios o comillas dobles se deben escribir entre comillas dobles ("). Las comillas dobles incrustadas se deben duplicar (por ejemplo, para usar **"A#B" D** como contraseña debe escribir **""A#B"" D"**).  
  
## <a name="see-also"></a>Vea también  
 [Cómo usar la interfaz de línea de comandos del servicio CDC](how-to-use-the-cdc-service-command-line-interface.md)   
 [Cómo preparar SQL Server para CDC](prepare-sql-server-for-cdc.md)  
  
  
