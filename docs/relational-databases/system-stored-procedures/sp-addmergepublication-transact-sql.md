---
title: sp_addmergepublication (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addmergepublication
- sp_addmergepublication_TSQL
helpviewer_keywords:
- sp_addmergepublication
ms.assetid: 28a629a1-7374-4614-9b04-279d290a942a
caps.latest.revision: 72
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ad636ff51a7a64cf1d46e8bb39b4937137454dd4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spaddmergepublication-transact-sql"></a>sp_addmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una publicación de combinación nueva. Este procedimiento almacenado se ejecuta en el publicador de la base de datos que se publica.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addmergepublication [ @publication = ] 'publication'   
    [ , [ @description = ] 'description'   
    [ , [ @retention = ] retention ]   
    [ , [ @sync_mode = ] 'sync_mode' ]   
    [ , [ @allow_push = ] 'allow_push' ]   
    [ , [ @allow_pull = ] 'allow_pull' ]   
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]   
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]   
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @dynamic_filters = ] 'dynamic_filters' ]   
    [ , [ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder' ]   
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @pre_snapshot_script = ] 'pre_snapshot_script' ]   
    [ , [ @post_snapshot_script = ] 'post_snapshot_script' ]   
    [ , [ @compress_snapshot = ] 'compress_snapshot' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]   
    [ , [ @conflict_retention = ] conflict_retention ]   
    [ , [ @keep_partition_changes = ] 'keep_partition_changes' ]   
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]   
    [ , [ @allow_synctoalternate = ] 'allow_synctoalternate' ]   
    [ , [ @validate_subscriber_info = ] 'validate_subscriber_info' ]   
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]   
    [ , [ @max_concurrent_merge = ] maximum_concurrent_merge ]   
    [ , [ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots ]  
    [ , [ @use_partition_groups = ] 'use_partition_groups' ]  
    [ , [ @publication_compatibility_level = ] 'backward_comp_level' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot' ]   
    [ , [ @allow_web_synchronization = ] 'allow_web_synchronization' ]   
    [ , [ @web_synchronization_url = ] 'web_synchronization_url' ]  
    [ , [ @allow_partition_realignment = ] 'allow_partition_realignment' ]  
    [ , [ @retention_period_unit = ] 'retention_period_unit' ]  
    [ , [ @generation_leveling_threshold = ] generation_leveling_threshold ]  
    [ , [ @automatic_reinitialization_policy = ] automatic_reinitialization_policy ]  
    [ , [ @conflict_logging = ] 'conflict_logging' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicación***'**  
 Es el nombre de la publicación de mezcla que se va a crear. *publicación* es **sysname**, no tiene ningún valor predeterminado y debe no ser la palabra clave todos. El nombre de la publicación debe ser único en la base de datos.  
  
 [  **@description =** ] **'***descripción***'**  
 Es la descripción de la publicación. *descripción* es **nvarchar (255)**, su valor predeterminado es null.  
  
 [  **@retention =** ] *retención*  
 Es el período de retención, en retención unidades de período, para el que desea guardar los cambios para la dada *publicación*. *retención* es **int**, su valor predeterminado es 14 unidades. Unidades del período de retención se definen mediante *retention_period_unit*. Si la suscripción no está sincronizada en el período de retención y se han quitado, por medio de una operación de limpieza en el distribuidor, los cambios pendientes que podía haber recibido, la suscripción expira y es necesario reinicializarla. El período de retención máximo permitido es el número de días comprendido entre el 31 de diciembre de 9999 y la fecha actual.  
  
> [!NOTE]  
>  El período de retención para las publicaciones de combinación tiene un plazo de gracia de 24 horas para adaptarse a los suscriptores de las diferentes zonas horarias. Si, por ejemplo, se establece un período de retención de un día, el período de retención real será de 48 horas.  
  
 [  **@sync_mode =** ] **'***sync_mode***'**  
 Es el modo de la sincronización inicial de suscriptores con la publicación. *sync_mode* es **nvarchar (10)**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**Native** (valor predeterminado)|Genera la salida de todas las tablas mediante un programa de copia masiva en modo nativo.|  
|**carácter**|Genera la salida de todas las tablas mediante un programa de copia masiva en modo de caracteres. Debe admitir [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] y no-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores.|  
  
 [  **@allow_push =** ] **'***allow_push***'**  
 Especifica si es posible crear suscripciones de inserción para la publicación indicada. *allow_push* es **nvarchar (5)**, su valor predeterminado es TRUE, que permite suscripciones de inserción en la publicación.  
  
 [  **@allow_pull =** ] **'***allow_pull***'**  
 Especifica si es posible crear suscripciones de extracción para la publicación indicada. *allow_pull* es **nvarchar (5)**, su valor predeterminado es TRUE, que permite suscripciones de extracción en la publicación. Debe especificar True para compatibilidad con [!INCLUDE[ssEW](../../includes/ssew-md.md)] los suscriptores.  
  
 [  **@allow_anonymous =** ] **'***allow_anonymous***'**  
 Especifica si es posible crear suscripciones anónimas para la publicación indicada. *allow_anonymous* es **nvarchar (5)**, su valor predeterminado es TRUE, que permite suscripciones anónimas en la publicación. Para admitir [!INCLUDE[ssEW](../../includes/ssew-md.md)] suscriptores, debe especificar **true**.  
  
 [  **@enabled_for_internet =** ] **'***enabled_for_internet***'**  
 Especifica si la publicación está habilitada para Internet y determina si se puede utilizar el protocolo de transferencia de archivos (FTP) para transferir los archivos de instantánea a un suscriptor. *enabled_for_internet* es **nvarchar (5)**, con un valor predeterminado es FALSE. Si **true**, los archivos de sincronización para la publicación se colocan en el directorio C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp. El usuario debe crear el directorio Ftp. Si **false**, la publicación no está habilitada para el acceso a Internet.  
  
 [  **@centralized_conflicts =**] **'***centralized_conflicts***'**  
 Este parámetro ha quedado desusado y solo se admite para la compatibilidad de scripts con versiones anteriores. Use *conflict_logging* para especificar la ubicación donde se almacenan los registros de conflictos.  
  
 [  **@dynamic_filters =**] **'***dynamic_filters***'**  
 Permite que la publicación de mezcla use filtros de filas con parámetros. *dynamic_filters* es **nvarchar (5)**, con un valor predeterminado es FALSE.  
  
> [!NOTE]  
>  No se recomienda especificar este parámetro; es mejor que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determine de forma automática si se están utilizando filtros de fila con parámetros. Si especifica un valor de **true** para *dynamic_filters*, debe definir un filtro de fila con parámetros para el artículo. Para más información, consulte [Definir y modificar un filtro de fila con parámetros para un artículo de mezcla](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
 [  **@snapshot_in_defaultfolder =** ] **'***snapshot_in_default_folder***'**  
 Especifica si los archivos de instantáneas se almacenan en la carpeta predeterminada. *snapshot_in_default_folder* es **nvarchar (5)**, con un valor predeterminado es TRUE. Si **true**, archivos de instantáneas se pueden encontrar en la carpeta predeterminada. Si **false**, archivos de instantáneas se almacenarán en la ubicación alternativa especificada por *alternate_snapshot_folder*. Las ubicaciones alternativas pueden encontrarse en otro servidor, en una unidad de red o en medios extraíbles (como CD-ROM o discos extraíbles). También puede guardar los archivos de instantáneas en un sitio FTP (Protocolo de transferencia de archivos), para que el suscriptor los recupere más tarde. Tenga en cuenta que este parámetro puede ser true y seguir teniendo una ubicación especificada por *alt_snapshot_folder*. Esta combinación especifica que los archivos de instantáneas se almacenarán tanto en la ubicación predeterminada como en la alternativa.  
  
 [  **@alt_snapshot_folder =** ] **'***alternate_snapshot_folder***'**  
 Especifica la ubicación de la carpeta alternativa de la instantánea. *alternate_snapshot_folder* es **nvarchar (255)**, su valor predeterminado es null.  
  
 [  **@pre_snapshot_script =** ] **'***pre_snapshot_script***'**  
 Especifica un puntero a un **.sql** ubicación del archivo. *pre_snapshot_script* es **nvarchar (255)**, su valor predeterminado es null. El Agente de mezcla ejecutará el script previo a la instantánea antes que cualquiera de los scripts de objetos replicados al aplicar la instantánea en un suscriptor. El script se ejecuta en el contexto de seguridad utilizado por el Agente de mezcla durante la conexión con la base de datos de suscripciones. Las secuencias de comandos anterior a la instantánea no se ejecutan en [!INCLUDE[ssEW](../../includes/ssew-md.md)] los suscriptores.  
  
 [  **@post_snapshot_script =** ] **'***post_snapshot_script***'**  
 Especifica un puntero a un **.sql** ubicación del archivo. *post_snapshot_script* es **nvarchar (255)**, su valor predeterminado es null. El Agente de mezcla ejecutará el script posterior a la instantánea después de que se apliquen los demás scripts y datos de objetos replicados durante una sincronización inicial. El script se ejecuta en el contexto de seguridad utilizado por el Agente de mezcla durante la conexión con la base de datos de suscripciones. Las secuencias de comandos posterior a la instantánea no se ejecutan en [!INCLUDE[ssEW](../../includes/ssew-md.md)] los suscriptores.  
  
 [  **@compress_snapshot =** ] **'***compress_snapshot***'**  
 Especifica que la instantánea escrita en la **@alt_snapshot_folder** ubicación está comprimida en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. *compress_snapshot* es **nvarchar (5)**, con un valor predeterminado es FALSE. **false** especifica que no se comprimirá la instantánea; **true** especifica que se comprimirá la instantánea. No se pueden comprimir archivos de instantáneas superiores a 2 GB. Los archivos de instantáneas comprimidos se descomprimen en la ubicación en la que se ejecuta el Agente de mezcla; normalmente, se utilizan suscripciones de extracción con las instantáneas comprimidas para descomprimir los archivos en el suscriptor. La instantánea de la carpeta predeterminada no se puede comprimir. Para admitir [!INCLUDE[ssEW](../../includes/ssew-md.md)] suscriptores, debe especificar **false**.  
  
 [  **@ftp_address =** ] **'***ftp_address***'**  
 Es la dirección de red del servicio FTP para el distribuidor. *ftp_address* es **sysname**, su valor predeterminado es null. Especifica dónde se encuentran el agente de mezcla de un suscriptor para recoger los archivos de instantáneas de publicación. Puesto que esta propiedad se almacena para todas las publicaciones, cada publicación puede tener diferentes *ftp_address*. La publicación debe ser compatible con la propagación de instantáneas mediante FTP.  
  
 [  **@ftp_port=** ] *ftp_port*  
 Es el número de puerto del servicio FTP para el distribuidor. *ftp_port* es **int**, su valor predeterminado es 21. Especifica dónde se encuentran los archivos de instantánea de la publicación para que los recoja el Agente de mezcla de un suscriptor. Puesto que esta propiedad se almacena para todas las publicaciones, cada publicación puede tener su propio *ftp_port*.  
  
 [  **@ftp_subdirectory =** ] **'***ftp_subdirectory***'**  
 Especifica dónde estarán disponibles los archivos de instantánea para que los recupere el Agente de mezcla del suscriptor si la publicación admite la propagación de instantáneas mediante FTP. *ftp_subdirectory* es **nvarchar (255)**, su valor predeterminado es null. Puesto que esta propiedad se almacena para todas las publicaciones, cada publicación puede tener su propio *ftp_subdirctory* o elegir no tener subdirectorio, indicándolo con un valor NULL.  
  
 En la generación previa de instantáneas para publicaciones con filtros con parámetros, la instantánea de datos de cada partición del suscriptor debe estar en su propia carpeta. La estructura de directorios para las instantáneas generadas previamente mediante FTP debe ser la siguiente:  
  
 *alternate_snapshot_folder*\ftp\\*publisher_publicationDB_publication*\\*partitionID*.  
  
> [!NOTE]  
>  Los valores indicados en cursiva dependen de la configuración específica de la publicación y partición del suscriptor.  
  
 [  **@ftp_login =** ] **'***ftp_login***'**  
 Es el nombre de usuario que se utiliza para conectar con el servicio FTP. *ftp_login* es **sysname**, su valor predeterminado es 'anonymous'.  
  
 [  **@ftp_password =** ] **'***ftp_password***'**  
 Es la contraseña del usuario que se utiliza para conectarse al servicio FTP. *ftp_password* es **sysname**, su valor predeterminado es null.  
  
> [!IMPORTANT]  
>  No utilice una contraseña en blanco. Utilice una contraseña segura.  
  
 [  **@conflict_retention =** ] *conflict_retention*  
 Especifica el período de retención, expresado en días, durante el que se conservan los conflictos. *conflict_retention* es **int**, con un valor predeterminado de 14 días antes el conflicto se purga fila de la tabla de conflictos.  
  
 [  **@keep_partition_changes =** ] **'***keep_partition_changes***'**  
 Especifica si se permiten optimizaciones de cambio de particiones cuando no se pueden usar las particiones precalculadas. *keep_partition_changes* es **nvarchar (5)**, con un valor predeterminado es TRUE. **false** significa que las particiones de los cambios no se optimiza y cuando no se utilizan particiones precalculadas, las particiones enviadas a todos los suscriptores se comprobarán cuando cambian los datos de una partición. **True** significa que los cambios de partición se optimiza y solo los suscriptores que tienen filas en las particiones modificadas se ven afectados. Al utilizar particiones precalculadas, establezca *use_partition_groups* a **true** y establecer *keep_partition_changes* a **false**. Para obtener más información, vea [Optimizar el rendimiento de los filtros con parámetros con particiones calculadas previamente](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
> [!NOTE]  
>  Si especifica un valor de **true** para *keep_partition_changes*, especifique un valor de **1** para el parámetro de agente de instantáneas **- MaxNetworkOptimization** . Para obtener más información acerca de este parámetro, vea [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md). Para obtener información acerca de cómo especificar parámetros de agente, vea [administración del agente de replicación](../../relational-databases/replication/agents/replication-agent-administration.md).  
  
 Con [!INCLUDE[ssEW](../../includes/ssew-md.md)] suscriptores, *keep_partition_changes* debe establecerse en true para asegurarse de que las eliminaciones se propagan correctamente. Si se establece en false, el suscriptor puede tener más filas de las esperadas.  
  
 [  **@allow_subscription_copy=** ] **'***allow_subscription_copy***'**  
 Habilita o deshabilita la funcionalidad de copia de las bases de datos de suscripciones suscritas a esta publicación. *allow_subscription_copy* es **nvarchar (5)**, con un valor predeterminado es FALSE. El tamaño de la base de datos de suscripciones que se va a copiar debe ser inferior a 2 gigabytes (GB).  
  
 [  **@allow_synctoalternate =** ] **'***allow_synctoalternate***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@validate_subscriber_info =** ] **'***validate_subscriber_info***'**  
 Muestra las funciones que se usan para definir una partición de suscriptor de los datos publicados cuando se usan filtros de fila con parámetros. *validate_subscriber_info* es **nvarchar (500)**, su valor predeterminado es null. El Agente de mezcla utiliza esta información para validar la partición del suscriptor. Por ejemplo, si [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) se utiliza en el filtro de fila con parámetros, el parámetro debe ser `@validate_subscriber_info=N'SUSER_SNAME()'`.  
  
> [!NOTE]  
>  No se recomienda especificar este parámetro; es mejor que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determine de forma automática el criterio de filtrado.  
  
 [  **@add_to_active_directory =** ] **'***add_to_active_directory***'**  
 Este parámetro ha quedado desusado y solo se admite para la compatibilidad de scripts con versiones anteriores. Ya no se puede agregar información de publicación a [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory.  
  
 [  **@max_concurrent_merge =** ] *maximum_concurrent_merge*  
 Número máximo de procesos de mezcla simultáneos. *maximum_concurrent_merge* es **int** con un valor predeterminado es 0. Un valor de **0** para esta propiedad significa que no hay ningún límite en el número de procesos de mezcla simultáneos que se ejecutan en un momento dado. Esta propiedad establece un límite para el número de procesos de mezcla simultáneos que se pueden ejecutar con una publicación de combinación en un momento determinado. Si hay más procesos de mezcla programados para ejecutarse simultáneamente de los que permite el valor de esta propiedad, los trabajos restantes se colocan en una cola hasta que finalice el proceso de mezcla que se está ejecutando en ese momento.  
  
 [  **@max_concurrent_dynamic_snapshots =**] *max_concurrent_dynamic_snapshots*  
 Número máximo de sesiones del Agente de instantáneas que se pueden ejecutar simultáneamente para generar instantáneas de datos filtrados en particiones del suscriptor. *maximum_concurrent_dynamic_snapshots* es **int** con un valor predeterminado es 0. Si **0**, no hay ningún límite para las sesiones de instantánea número. Si hay más procesos de instantánea programados al mismo tiempo que los que permite ejecutar el valor, los trabajos sobrantes se colocarán en una cola y esperarán hasta que finalice el proceso de instantánea que se está ejecutando actualmente.  
  
 [  **@use_partition_groups =** ] **'***use_partition_groups***'**  
 Especifica que se deben usar particiones precalculadas para optimizar el proceso de sincronización. *use_partition_groups* es **nvarchar (5)**, y puede tener uno de estos valores:  
  
|Value|Description|  
|-----------|-----------------|  
|**true**|La publicación utiliza particiones previamente calculadas.|  
|**False**|La publicación no utiliza particiones previamente calculadas.|  
|NULL(Default)|El sistema decide la estrategia de partición.|  
  
 Las particiones precalculadas se utilizan de manera predeterminada. Para evitar usar particiones precalculadas, *use_partition_groups* debe establecerse en **false**. Si es NULL, el sistema decidirá si se pueden utilizar. Si precalculadas particiones no se puede usar, a continuación, este valor se convierte en **false** sin generar errores. En tales casos, *keep_partition_changes* se puede establecer en **true** para proporcionar alguna optimización. Para obtener más información, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md) y [optimizar el rendimiento de filtro con parámetros con particiones precalculadas](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
 [  **@publication_compatibility_level =** ] *backward_comp_level*  
 Indica la compatibilidad con versiones anteriores de la publicación. *backward_comp_level* es **nvarchar(6)**, y puede tener uno de estos valores:  
  
|Value|Versión|  
|-----------|-------------|  
|**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
  
 [  **@replicate_ddl =** ] *replicate_ddl*  
 Indica si la publicación admite replicación de esquema. *replicate_ddl* es **int**, su valor predeterminado es 1. **1** indica que se replican instrucciones de DDL (lenguaje) de definición de datos ejecutadas en el publicador, y **0** indica que no se replican las instrucciones de DDL. Para más información, vea [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Realizar cambios de esquema en bases de datos de publicaciones).  
  
 El *@replicate_ddl* parámetro se observa cuando una instrucción DDL agrega una columna. El *@replicate_ddl* parámetro se ignora cuando una instrucción DDL modifica o quita una columna por las razones siguientes.  
  
-   Cuando se quita una columna, sysarticlecolumns debe actualizarse para evitar que las nuevas instrucciones DML incluyan la columna quitada lo que haría que el agente de distribución genere un error. El *@replicate_ddl* parámetro se ignora porque la replicación siempre debe replicar el cambio de esquema.  
  
-   Cuando se modifica una columna, es posible que el tipo de datos de origen o la nulabilidad hayan cambiado, lo que hace que las instrucciones DML contengan un valor que quizás no sea compatible con la tabla en el suscriptor. Estas instrucciones DML pueden hacer que el agente de distribución genere un error. El *@replicate_ddl* parámetro se ignora porque la replicación siempre debe replicar el cambio de esquema.  
  
-   Cuando una instrucción DDL agrega una nueva columna, sysarticlecolumns no incluye la nueva columna. Las instrucciones DML no intentarán replicar datos para la nueva columna. Se respeta el parámetro porque la DDL es aceptable se realice o no la replicación.  
  
 [  **@allow_subscriber_initiated_snapshot =** ] **'***allow_subscriber_initiated_snapshot***'**  
 Indica si los suscriptores de esta publicación pueden iniciar el proceso de instantánea para generar instantáneas filtradas para su partición de datos. *allow_subscriber_initiated_snapshot* es **nvarchar (5)**, con un valor predeterminado es FALSE. **True** indica que los suscriptores pueden iniciar el proceso de instantáneas.  
  
 [  **@allow_web_synchronization =** ] **'***allow_web_synchronization***'**  
 Especifica si la publicación se habilita para sincronización web. *allow_web_synchronization* es **nvarchar (5)**, con un valor predeterminado es FALSE. **True** especifica que se pueden sincronizar las suscripciones a esta publicación a través de HTTPS. Para más información, consulte [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md). Para admitir [!INCLUDE[ssEW](../../includes/ssew-md.md)] suscriptores, debe especificar **true**.  
  
 [  **@web_synchronization_url=** ] **'***web_synchronization_url***'**  
 Especifica el valor predeterminado de la dirección URL de Internet utilizada para la sincronización web. *web_synchronization_url*s **nvarchar (500)**, su valor predeterminado es null. Define la dirección URL de Internet predeterminada si no establece explícitamente una cuando [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) se ejecuta.  
  
 [  **@allow_partition_realignment =** ] **'***allow_partition_realignment***'**  
 Determina si se envían eliminaciones al suscriptor cuando una modificación de la fila del publicador provoca que se modifique su partición. *allow_partition_realignment* es **nvarchar (5)**, con un valor predeterminado es TRUE. **True** envía las eliminaciones al suscriptor para reflejar los resultados de un cambio en la partición mediante la eliminación de datos que ya no forma parte de la partición del suscriptor. **false** deja los datos de una partición antigua en el suscriptor, donde no se replicarán los cambios realizados en estos datos en el publicador al suscriptor, pero los cambios realizados en el suscriptor se replicarán al publicador. Establecer *allow_partition_realignment* a **false** se utiliza para conservar los datos de una partición antigua en una suscripción cuando los datos deben ser accesibles para fines históricos.  
  
> [!NOTE]  
>  Datos que permanecen en el suscriptor como resultado de establecer *allow_partition_realignment* a **false** deben tratarse como si fueran de solo lectura; sin embargo, esto no se aplica mediante el sistema de replicación.  
  
 [  **@retention_period_unit =** ] **'***retention_period_unit***'**  
 Especifica las unidades para el período de retención establecido *retención*. *retention_period_unit* es **nvarchar (10)**, y puede tener uno de los siguientes valores.  
  
|Value|Versión|  
|-----------|-------------|  
|**día** (valor predeterminado)|El período de retención se especifica en días.|  
|**week**|El período de retención se especifica en semanas.|  
|**month**|El período de retención se especifica en meses.|  
|**year**|El período de retención se especifica en años.|  
  
 [  **@generation_leveling_threshold=** ] *generation_leveling_threshold*  
 Especifica el número de cambios que se encuentran en una generación. Una generación es un conjunto de cambios que se entregan a un publicador o suscriptor. *generation_leveling_threshold* es **int**, con un valor predeterminado de 1000.  
  
 [  **@automatic_reinitialization_policy =** ] *automatic_reinitialization_policy*  
 Especifica si se cargan cambios desde el suscriptor antes que una reinicialización automática requerido un cambio en la publicación, donde un valor de **1** no se especificó para **@force_reinit_subscription**. *automatic_reinitialization_policy* es de tipo bit, con un valor predeterminado de 0. **1** significa que los cambios se cargan desde el suscriptor antes de que se produzca una reinicialización automática.  
  
> [!IMPORTANT]  
>  Si se agrega, quita o modifica un filtro con parámetros, los cambios pendientes en el suscriptor no se pueden cargar en el publicador durante la reinicialización. Si desea cargar los cambios pendientes, sincronice todas las suscripciones antes de cambiar el filtro.  
  
 [  **@conflict_logging =** ] **'***conflict_logging***'**  
 Especifica dónde se almacenan los registros conflictivos. *conflict_logging* es **nvarchar (15)**, y puede tener uno de los siguientes valores:  
  
|Value|Description|  
|-----------|-----------------|  
|**publicador**|Los registros de conflictos se almacenan en el publicador.|  
|**suscriptor**|Los registros de conflictos se almacenan en el suscriptor que causó el conflicto. No se admite para [!INCLUDE[ssEW](../../includes/ssew-md.md)] los suscriptores.|  
|**ambos**|Los registros de conflictos se almacenan tanto en el publicador como en el suscriptor.|  
|NULL (predeterminado)|La replicación establece automáticamente *conflict_logging* a **ambos** cuando el valor *backward_comp_level* es **90RTM** y **publisher** en todos los demás casos.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addmergepublication** se utiliza en la replicación de mezcla.  
  
 Para enumerar los objetos de publicación a Active Directory mediante la **@add_to_active_directory** parámetro, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto debe estar ya creado en Active Directory.  
  
 Si existen varias publicaciones que publicar el mismo objeto de base de datos, solamente las publicaciones con un *replicate_ddl* valo **1** replicará ALTER TABLE, ALTER VIEW, ALTER PROCEDURE, ALTER FUNCTION y Instrucciones ALTER TRIGGER de DDL. Sin embargo, todas las publicaciones que publiquen la columna quitada replicarán una instrucción ALTER TABLE DROP COLUMN de DDL.  
  
 Para [!INCLUDE[ssEW](../../includes/ssew-md.md)] los suscriptores, el valor de *alternate_snapshot_folder* solamente se utiliza cuando el valor de *snapshot_in_default_folder* es **false**.  
  
 Con la replicación DDL habilitada (* replicate_ddl ***= 1**) para una publicación, con el fin de realizar sin replicación DDL cambios en la publicación, [sp_changemergepublication &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)primero debe ejecutar para establecer *replicate_ddl* a **0**. Una vez que se han ejecutado las instrucciones de DDL sin replicación, **sp_changemergepublication** puede ejecutarse de nuevo para volver a activar la replicación DDL.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_AddMergePub](../../relational-databases/replication/codesnippet/tsql/sp-addmergepublication-t_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_addmergepublication**.  
  
## <a name="see-also"></a>Vea también  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
