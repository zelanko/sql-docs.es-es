---
title: Bases de datos CDC de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a96486e9-f79b-4b24-bfaf-56203dd0e435
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6cce219b5e5d5d324e5e116bb9f55a931d7caaf8
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298626"
---
# <a name="the-oracle-cdc-databases"></a>Las bases de datos CDC de Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Una instancia CDC de Oracle está asociada a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el mismo nombre en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino. Esta base de datos se denomina la base de datos CDC de Oracle (o la base de datos CDC).  
  
 La base de datos CDC se crea y configura mediante la Consola del diseñador CDC de Oracle y contiene los elementos siguientes:  
  
-   Un esquema `cdc` que se crea habilitando la base de datos para CDC de SQL Server.  
  
-   Un conjunto de tablas **cdc.xdbcdc_xxxx** usadas por la instancia CDC de Oracle.  
  
-   Un conjunto de tablas reflejadas vacías con las definiciones de las tablas capturadas en la base de datos de Oracle de origen.  
  
-   Un conjunto de tablas de cambios y funciones de acceso a cambios generadas por el mecanismo CDC de SQL Server y que son idénticas a las usadas en CDC de SQL Server no de Oracle.  
  
 El esquema `cdc` solo es accesible inicialmente para los miembros del rol fijo de base de datos **dbowner** . El acceso a las tablas y funciones de cambios está determinado por el mismo modelo de seguridad que CDC de SQL Server. Para obtener más información sobre el modelo de seguridad, vea [Modelo de seguridad](https://go.microsoft.com/fwlink/?LinkId=231151).  
  
## <a name="creating-the-cdc-database"></a>Crear la base de datos CDC  
 En la mayoría de los casos, la base de datos CDC se crea mediante la Consola del diseñador CDC, pero también se puede crear con un script de implementación CDC que se genera mediante la Consola del diseñador CDC. El administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede cambiar la configuración de la base de datos si es necesario (para elementos como almacenamiento, seguridad o disponibilidad).  
  
 Para obtener más información sobre cómo usar la Consola del diseñador CDC para crear tablas de base de datos y los scripts necesarios, vea [Usar el Asistente para nueva instancia](../../integration-services/change-data-capture/use-the-new-instance-wizard.md).  
  
## <a name="cdc-database-user-roles"></a>Roles de usuario de la base de datos CDC  
 Cuando una base de datos CDC se crea y se habilita para CDC, se crea en la base de datos CDC un usuario de base de datos denominado **cdc_service** y se asocia al inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el que se ha configurado el servicio CDC de Oracle. Este usuario se convierte en miembro de los roles de base de datos **db_datareader**, **db_datawriter**y **db_ddladmin** . Si el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también está asociado al usuario `dbo` , no se crea el usuario **cdc_service** .  
  
 Esta asignación de roles permite al servicio CDC de Oracle actualizar las tablas en el esquema `cdc` con datos capturados y con información de control.  
  
 Cuando se crea una base de datos CDC y se configuran tablas CDC de Oracle de origen, el propietario de la base de datos CDC puede conceder el permiso SELECT para las tablas reflejadas y definir roles de acceso CDC de SQL Server para controlar quién tiene acceso a los datos modificados.  
  
## <a name="mirror-tables"></a>Tablas reflejadas  
 Para cada tabla capturada, \<schema-name>.\<table-name>, en la base de datos de origen de Oracle, se crea una tabla vacía similar en la base de datos CDC, con el mismo nombre de esquema y de tabla. Las tablas de origen de Oracle con el nombre de esquema `cdc` (no distingue entre mayúsculas y minúsculas) no se pueden capturar porque el esquema `cdc` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está reservado para CDC de SQL Server.  
  
 Las tablas reflejadas están vacías; no se almacena ningún dato en ellas. Se usan para habilitar la infraestructura estándar CDC de SQL Server que usa la instancia CDC de Oracle. Para evitar que se inserten o actualicen datos en las tablas reflejadas, se deniegan todas las operaciones UPDATE, DELETE e INSERT para PUBLIC. Esto garantiza que no se puedan modificar.  
  
## <a name="access-to-change-data"></a>Obtener acceso a datos modificados  
 Debido al modelo de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] empleado para obtener acceso a los datos modificados que está asociado a una instancia de captura, el usuario debe tener acceso `select` para todas las columnas capturadas de la tabla reflejada asociada (los permisos de acceso a las tablas originales de Oracle no proporcionan acceso a las tablas de cambios en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Para obtener información sobre el modelo de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Modelo de seguridad](https://go.microsoft.com/fwlink/?LinkId=231151).  
  
 Además, si se especifica un rol de acceso cuando se crea la instancia de captura, el autor de las llamadas también debe ser miembro del rol de acceso especificado. Otras funciones generales de captura de datos modificados para obtener acceso a los metadatos son accesibles para todos los usuarios de la base de datos a través del rol PUBLIC, aunque el acceso a los metadatos devueltos se suele conseguir mediante un acceso exclusivo a las tablas de origen subyacentes y por pertenencia a cualquier rol de acceso definido.  
  
 Los datos modificados se pueden leer llamando a funciones especiales basadas en tablas generadas por el componente CDC de SQL Server cuando se crea una instancia de captura. Para obtener más información sobre esta función, vea [Funciones de captura de datos modificados (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=231152).  
  
 El acceso a datos CDC mediante el componente CDC Source de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está sujeto a las mismas reglas.  
  
## <a name="the-cdc-database-tables"></a>Las tablas de base de datos CDC  
 En esta sección se describen las tablas siguientes de la base de datos CDC.  
  
-   [Tablas de cambios (_CT)](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_Change_Tables_CT)  
  
-   [cdc.lsn_time_mapping](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdclsn_time_mapping)  
  
-   [cdc.xdbcdc_config](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_config)  
  
-   [cdc.xdbcdc_state](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_state)  
  
-   [cdc.xdbcdc_trace](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_trace)  
  
-   [cdc.xdbcdc_staged_transactions](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions)  
  
###  <a name="BKMK_Change_Tables_CT"></a> Tablas de cambios (_CT)  
 Las tablas de cambios se crean a partir de las tablas reflejadas. Contienen datos modificados que se capturan de la base de datos de Oracle. La denominación de las tablas emplea la convención siguiente:  
  
 **[cdc].[\<capture-instance>_CT]**  
  
 Cuando la captura está habilitada inicialmente para la tabla `<schema-name>.<table-name>`, el nombre predeterminado de la instancia de captura es `<schema-name>_<table-name>`. Por ejemplo, el nombre predeterminado de la instancia de captura para la tabla de Oracle HR.EMPLOYEES es HR_EMPLOYEES y la tabla de cambios asociada es [cdc]. [HR_EMPLOYEES_CT].  
  
 Las tablas de captura están escritas por la instancia CDC de Oracle. Se leen mediante funciones especiales con valores de tabla generadas por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se crea la instancia de captura. Por ejemplo, `fn_cdc_get_all_changes_HR_EMPLOYEES`. Para obtener más información sobre estas funciones CDC, vea [Funciones de captura de datos modificados (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=231152).  
  
###  <a name="BKMK_cdclsn_time_mapping"></a> cdc.lsn_time_mapping  
 El componente CDC de SQL Server genera la tabla **[cdc].[lsn_time_mapping]** . Su uso en el caso de CDC de Oracle es diferente del uso normal.  
  
 Para CDC de Oracle, los valores LSN almacenados en esta tabla se basan en el valor del número de cambio del sistema (SCN) de Oracle asociado al cambio. Los 6 primeros bytes del valor LSN son el número SCN original de Oracle.  
  
 Además, cuando se usa CDC de Oracle, las columnas de tiempo (`tran_begin_time` y `tran_end_time`) almacenan la hora UTC del cambio en lugar de la hora local, como ocurre con CDC normal de SQL Server. Esto garantiza que los cambios del horario de verano no afecten a los datos almacenados en lsn_time_mapping.  
  
###  <a name="BKMK_cdcxdbcdc_config"></a> cdc.xdbcdc_config  
 Esta tabla contiene los datos de configuración para la instancia CDC de Oracle. Se actualiza mediante la Consola del diseñador CDC. Esta tabla solo tiene una fila.  
  
 En la tabla siguiente se describen las columnas de la tabla **cdc.xdbcdc_config** .  
  
|Elemento|Descripción|  
|----------|-----------------|  
|version|Hace un seguimiento de la versión de la configuración de la instancia CDC. Se actualiza cada vez que se actualiza la tabla y cada vez que se agrega una nueva instancia de captura o cuando se quita una instancia de captura existente.|  
|connect_string|Cadena de conexión de Oracle. Un ejemplo básico es:<br /><br /> `<server>:<port>/<instance>` (por ejemplo, `erp.contoso.com:1521/orcl`).<br /><br /> La cadena de conexión también puede especificar un descriptor de conexión de Oracle Net, por ejemplo `(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp) (HOST=erp.contoso.com) (PORT=1521)) (CONNECT_DATA=(SERVICE_NAME=orcl)))`.<br /><br /> Si se usa un servidor de directorio o tnsnames, la cadena de conexión puede ser el nombre de la conexión.<br /><br /> Para obtener más información sobre las cadenas de conexión de Oracle, vea [https://go.microsoft.com/fwlink/?LinkId=231153](https://go.microsoft.com/fwlink/?LinkId=231153) para obtener información detallada sobre las cadenas de conexión a bases de datos de Oracle para el cliente Oracle Instant usado por el servicio CDC de Oracle.|  
|use_windows_authentication|Valor booleano que puede ser:<br /><br /> **0**: se proporcionan un nombre de usuario y una contraseña de Oracle para la autenticación (valor predeterminado).<br /><br /> **1**: se usa la autenticación de Windows para conectar con la base de datos Oracle. Solo puede usar esta opción si la base de datos de Oracle está configurada para usar la autenticación de Windows.|  
|username|Nombre del usuario de la base de datos de Oracle de minería de registros. Solo es necesario si **use_windows_authentication = 0**.|  
|password|Contraseña del usuario de la base de datos de Oracle de minería de registros. Solo es necesario si **use_windows_authentication = 0**.|  
|transaction_staging_timeout|Tiempo, en segundos, que una transacción de Oracle no confirmada se conserva en memoria antes de escribirse en la tabla **cdc.xdbcdc_staged_transactions** . El valor predeterminado es 120 segundos.|  
|memory_limit|Límite de la cantidad de memoria, en MB, que se puede usar para almacenar los datos en memoria caché. Un valor menor hace que se escriban más transacciones en la tabla **cdc.xdbcdc_staged_transactions** . El valor predeterminado es 50 MB.|  
|opciones|Lista de opciones con el formato nombre[=valor][; ]: se usa para especificar opciones secundarias (por ejemplo, seguimiento y optimización). Vea la tabla siguiente para obtener una descripción de las opciones disponibles.|  
  
 En la tabla siguiente se describen las opciones disponibles.  
  
|Nombre|Valor predeterminado|Min|Max|Estático|Descripción|  
|----------|-------------|---------|---------|------------|-----------------|  
|seguimiento|False|-|-|False|Los valores disponibles son:<br /><br /> True<br /><br /> False<br /><br /> on<br /><br /> off|  
|cdc_update_state_interval|10|1|120|False|Tamaño (en kilobytes) de los fragmentos de memoria asignados para una transacción (una transacción puede asignar más de un fragmento). Vea la columna memory_limit en la tabla [cdc.xdbcdc_config](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_config) .|  
|target_max_batched_transactions|100|1|1000|True|Número máximo de transacciones de Oracle que se pueden procesar como una transacción en la actualización de tablas de cambios de SQL Server.|  
|target_idle_lsn_update_interval|10|0|1|False|Intervalo (en segundos) de actualización de la tabla **lsn_time_mapping** cuando las tablas capturadas no tienen ninguna actividad.|  
|trace_retention_period|24|1|24*31|False|Tiempo (en horas) que se van a conservar los mensajes en la tabla de seguimiento.|  
|sql_reconnect_interval|2|2|3600|False|Período de tiempo (en segundos) que se va a esperar antes de volver a conectar con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este intervalo se usa además del tiempo de espera de conexión del cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|sql_reconnect_limit|-1|-1|-1|False|Número máximo de reconexiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El valor predeterminado -1 significa que el proceso intenta volver a conectarse hasta que se detiene.|  
|cdc_restart_limit|6|-1|3600|False|En la mayoría de los casos, el servicio CDC reinicia automáticamente una instancia CDC finalizada de forma anómala. Esta propiedad define después de cuántos errores por hora el servicio deja de reiniciar la instancia. El valor -1 significa que la instancia se debe reiniciar siempre.<br /><br /> El servicio vuelve para reiniciar la instancia después de cualquier actualización de la tabla de configuración.|  
|cdc_memory_report|0|0|1000|False|Si el valor del parámetro se ha cambiado, la instancia CDC imprime su informe de memoria en la tabla de seguimiento.|  
|target_command_timeout|600|1|3600|False|Tiempo de espera de comandos que funciona con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|source_character_set|-|-|-|True|Se puede establecer en una codificación específica de Oracle que se usará en lugar de la página de códigos de la base de datos de Oracle. Puede ser útil cuando la codificación real que los datos de caracteres están usando es diferente de la expresada por la página de códigos de la base de datos de Oracle.|  
|source_error_retry_interval|30|1|3600|False|Se usa antes de reintentar tras varios errores como un error de conexión o cuando hay una falta temporal de sincronización entre tablas del sistema.|  
|source_prefetch_size|100|1|10000|True|Tamaño del lote de captura previa.|  
|source_max_tables_in_query|100|1|10000|True|Número máximo de tablas en la cláusula WHERE antes de cambiar a leer el registro de Oracle sin filtrado de tabla.|  
|source_read_retry_interval|2|1|3600|False|Período de tiempo que el origen espera antes de intentar leer de nuevo los registros de transacciones de Oracle en EOF.|  
|source_reconnect_interval|30|1|3600|False|Período de tiempo (en segundos) que hay que esperar antes de intentar volver a conectar con la base de datos de origen.|  
|source_reconnect_limit|-1|-1||False|Número máximo de reconexiones de la base de datos de origen. El valor predeterminado -1 significa que el proceso intenta volver a conectarse hasta que se detiene.|  
|source_command_timeout|30|1|3600|False|Tiempo de espera de conexión cuando se usa Oracle.|  
|source_connection_timeout|30|1|3600|False|Tiempo de espera de conexión que funciona con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|trace_data_errors|True|-|-|False|booleano. **True** indica que se van a registrar los errores de truncamiento y de conversión de los datos.|  
|CDC_stop_on_breaking_schema_changes|False|-|-|False|booleano. **True** indica que se va a detener cuando se detecta un cambio de esquema.<br /><br /> **False** indica que se van a quitar la tabla reflejada y la instancia de la captura.|  
|source_oracle_home||-|-|False|Se puede establecer en una ruta de acceso o un nombre específico de Oracle Home que la instancia CDC usará para conectar con Oracle.|  
  
###  <a name="BKMK_cdcxdbcdc_state"></a> cdc.xdbcdc_state  
 Esta tabla contiene información sobre el estado guardado de la instancia CDC de Oracle. El estado de captura se emplea en escenarios de recuperación y de conmutación por error, y para el seguimiento de estado.  
  
 En la tabla siguiente se describen las columnas de la tabla **cdc.xdbcdc_state** .  
  
|Elemento|Descripción|  
|----------|-----------------|  
|status|Código de estado actual para la instancia CDC de Oracle actual. El estado describe el estado actual de CDC.|  
|sub_status|Estado de segundo nivel que proporciona información adicional sobre el estado actual.|  
|active|Valor booleano que puede ser:<br /><br /> **0**: el proceso de la instancia CDC de Oracle no está activo.<br /><br /> **1**: el proceso de la instancia CDC de Oracle está activo.|  
|error|Valor booleano que puede ser:<br /><br /> **0**: el proceso de la instancia CDC de Oracle no está en un estado de error.<br /><br /> **1**: la instancia CDC de Oracle está en un estado de error.|  
|status_message|Cadena que proporciona una descripción del error o el estado.|  
|TIMESTAMP|Marca de tiempo con la hora (UTC) en que el estado de captura se actualizó por última vez.|  
|active_capture_node|Nombre del host (el host puede ser un nodo de un clúster) que está ejecutando actualmente el servicio y la instancia CDC de Oracle (que está procesando los registros de transacciones de Oracle).|  
|last_transaction_timestamp|Marca de tiempo con la hora (UTC) en que se escribió la última transacción en las tablas de cambios.|  
|last_change_timestamp|Marca de tiempo con la hora (UTC) en que se leyó el registro de cambios más reciente del registro de transacciones de Oracle de origen. Esta marca de tiempo ayuda a identificar la latencia actual del proceso CDC.|  
|transaction_log_head_cn|Número de cambio (CN) más reciente leído del registro de transacciones de Oracle.|  
|transaction_log_tail_cn|Número de cambio (CN) en el registro de transacciones de Oracle donde se sitúa la instancia CDC de Oracle en caso de que se produzca un reinicio o una recuperación.|  
|current_cn|Número de cambio (CN) más reciente que se sabe que está en la base de datos de origen.|  
|software_version|Versión interna del servicio CDC de Oracle.|  
|completed_transactions|Número de transacciones procesadas desde que CDC se restableció por última vez.|  
|written_changes|Número de registros de cambios escritos en las tablas de cambios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|read_changes|Número de registros de cambios leídos del registro de transacciones de Oracle de origen.|  
|staged_transactions|Número de transacciones activas actualmente almacenadas provisionalmente en la tabla **cdc.xdbcdc_staged_transactions** .|  
  
###  <a name="BKMK_cdcxdbcdc_trace"></a> cdc.xdbcdc_trace  
 Esta tabla contiene información acerca del funcionamiento de la instancia CDC. La información almacenada en esta tabla incluye registros de errores, cambios importantes de estado y registros de seguimiento. La información de error también se escribe en el registro de eventos de Windows para asegurarse de que la información esté disponible si la tabla **cdc.xcbcdc_trace** no está disponible.  
  
 En la tabla siguiente se describen las columnas de la tabla cdc.xdbcdc_trace.  
  
|Elemento|Descripción|  
|----------|-----------------|  
|TIMESTAMP|Marca de tiempo UTC exacta en que se escribió el registro de seguimiento.|  
|tipo|Contiene uno de los valores siguientes.<br /><br /> error<br /><br /> INFO<br /><br /> seguimiento|  
|Nodo|Nombre del nodo en el que se escribió el registro.|  
|status|Código de estado usado por la tabla de estado.|  
|sub_status|Código de subestado usado por la tabla de estado.|  
|status_message|Mensaje de estado usado por la tabla de estado.|  
|datos|Datos adicionales para aquellos casos en los que el registro de error o seguimiento contiene una carga (por ejemplo, una entrada de registro dañada).|  
  
###  <a name="BKMK_cdcxdbcdc_staged_transactions"></a> cdc.xdbcdc_staged_transactions  
 Esta tabla almacena los registros de cambios para transacciones grandes o de ejecución prolongada hasta que se captura el evento de confirmación o reversión de la transacción. El servicio CDC de Oracle ordena los registros de cambios capturados por hora de confirmación de la transacción y después por orden cronológico de cada transacción. Las entradas del registro para la misma transacción se almacenan en memoria hasta que la transacción finaliza y se escriben en la tabla de cambios de destino o se descartan (en caso de una reversión). Puesto que hay disponible una cantidad de memoria limitada, las transacciones grandes se escriben en la tabla **cdc.xdbcdc_staged_transactions** hasta que se completan. Las transacciones también se escriben en la tabla de ensayo cuando se ejecutan durante mucho tiempo. Por tanto, cuando se reinicia la instancia CDC de Oracle, no es necesario volver a leer los antiguos cambios de los registros de transacciones de Oracle.  
  
 En la tabla siguiente se describen las columnas de la tabla **cdc.xdbcdc_staged_transactions** .  
  
|Elemento|Descripción|  
|----------|-----------------|  
|transaction_id|Identificador único de la transacción que se está almacenando provisionalmente.|  
|seq_num|Número de fila de la tabla **xcbcdc_staged_transactions** para la transacción actual (empezando en 0).|  
|data_start_cn|Número de cambio (CN) del primer cambio en los datos de esta fila.|  
|data_end_cn|Número de cambio (CN) del último cambio en los datos de esta fila.|  
|datos|Cambios almacenados provisionalmente para la transacción en forma de blob.|  
  
## <a name="see-also"></a>Consulte también  
 [Diseñador de captura de datos modificados para Oracle de Attunity](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)  
  
  
