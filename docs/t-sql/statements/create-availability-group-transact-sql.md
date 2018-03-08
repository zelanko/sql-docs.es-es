---
title: Crear grupo de disponibilidad (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AVAILABILITY GROUP
- CREATE_AVAILABILITY_TSQL
- CREATE_AVAILABILITY_GROUP_TSQL
- CREATE AVAILABILITY GROUP
- CREATE AVAILABILITY
- AVAILABILITY_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- CREATE AVAILABILITY GROUP statement
- Availability Groups [SQL Server], creating
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: a3d55df7-b4e4-43f3-a14b-056cba36ab98
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e0a4792974ec9aa78678aec74dc390e992471e64
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="create-availability-group-transact-sql"></a>CREATE AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Crea un nuevo grupo de disponibilidad, si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está habilitada para la característica [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].  
  
> [!IMPORTANT]  
>  Ejecute CREATE AVAILABILITY GROUP en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que desea usar como réplica principal inicial del nuevo grupo de disponibilidad. Esta instancia de servidor debe residir en un nodo de clúster de conmutación por error de Windows Server (WSFC).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```SQL  
  
CREATE AVAILABILITY GROUP group_name  
   WITH (<with_option_spec> [ ,...n ] )  
   FOR [ DATABASE database_name [ ,...n ] ]  
   REPLICA ON <add_replica_spec> [ ,...n ]  
   AVAILABILITY GROUP ON <add_availability_group_spec> [ ,...2 ]  
   [ LISTENER ‘dns_name’ ( <listener_option> ) ]  
[ ; ]  
  
<with_option_spec>::=   
    AUTOMATED_BACKUP_PREFERENCE = { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
  | FAILURE_CONDITION_LEVEL  = { 1 | 2 | 3 | 4 | 5 }   
  | HEALTH_CHECK_TIMEOUT = milliseconds  
  | DB_FAILOVER  = { ON | OFF }   
  | DTC_SUPPORT  = { PER_DB | NONE }  
  | BASIC  
  | DISTRIBUTED
  | REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = { integer }
  | CLUSTER_TYPE = { WSFC | EXTERNAL | NONE } 
  
<add_replica_spec>::=  
  <server_instance> WITH  
    (  
       ENDPOINT_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY },  
       FAILOVER_MODE = { AUTOMATIC | MANUAL | EXTERNAL }  
       [ , <add_replica_option> [ ,...n ] ]  
    )   
  
  <add_replica_option>::=  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
            [ ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL } ]   
        [,] [ READ_ONLY_ROUTING_URL = 'TCP://system-address:port' ]  
     } )  
     | PRIMARY_ROLE ( {   
            [ ALLOW_CONNECTIONS = { READ_WRITE | ALL } ]   
        [,] [ READ_ONLY_ROUTING_LIST = { ( ‘<server_instance>’ [ ,...n ] ) | NONE } ]  
     } )  
     | SESSION_TIMEOUT = integer  
  
<add_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = MANUAL,  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<listener_option> ::=  
   {  
      WITH DHCP [ ON ( <network_subnet_option> ) ]  
    | WITH IP ( { ( <ip_address_option> ) } [ , ...n ] ) [ , PORT = listener_port ]  
   }  
  
  <network_subnet_option> ::=  
     ‘four_part_ipv4_address’, ‘four_part_ipv4_mask’    
  
  <ip_address_option> ::=  
     {   
        ‘four_part_ipv4_address’, ‘four_part_ipv4_mask’  
      | ‘ipv6_address’  
     }  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *group_name*  
 Especifica el nombre del nuevo grupo de disponibilidad. *nombre_grupo* debe ser válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [identificador](../../relational-databases/databases/database-identifiers.md), y debe ser único en todos los grupos de disponibilidad del clúster de WSFC. La longitud máxima del nombre de un grupo de disponibilidad es 128 caracteres.  
  
 AUTOMATED_BACKUP_PREFERENCE  **=**  {PRINCIPAL | SECONDARY_ONLY | SECUNDARIO | NINGUNO}  
 Especifica una preferencia sobre cómo un trabajo de copia de seguridad debe evaluar la réplica principal cuando elige realizar copias de seguridad. Puede crear un script con un trabajo de copia de seguridad para que se tenga en cuenta la preferencia de copia de seguridad automatizada. Es importante entender que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no aplica la preferencia, por lo que las copias de seguridad ad hoc no resultan afectadas.  
  
 Los valores admitidos son los siguientes:  
  
 PRIMARY  
 Especifica que las copias de seguridad deben realizarse siempre en la réplica principal. Esta opción es útil si necesita usar características de copia de seguridad, como crear copias de seguridad diferenciales, que no se admiten cuando la copia de seguridad se ejecuta en una réplica secundaria.  
  
> [!IMPORTANT]  
>  Si piensa usar el trasvase de registros para preparar cualquier base de datos secundaria de un grupo de disponibilidad, establezca la preferencia de copia de seguridad automatizada en **Principal** hasta que todas las bases de datos secundarias se hayan preparado y combinado con el grupo de disponibilidad.  
  
 SECONDARY_ONLY  
 Especifica que las copias de seguridad no deben realizarse nunca en la réplica principal. Si la réplica principal es la única réplica en línea, no se debe realizar la copia de seguridad.  
  
 SECONDARY  
 Especifica que las copias de seguridad se deben realizar en una réplica secundaria a menos que la réplica principal sea la única réplica en línea. En ese caso, la copia de seguridad se debe realizar en la réplica principal. Éste es el comportamiento predeterminado.  
  
 Ninguno  
 Especifica que, de acuerdo con sus preferencias, los trabajos de copia de seguridad omitan el rol de las réplicas de disponibilidad cuando la réplica realiza copias de seguridad. Tenga en cuenta que los trabajos de copia de seguridad pueden considerar otros factores, como la prioridad de copia de seguridad de cada réplica de disponibilidad junto con su estado operativo y de conexión.  
  
> [!IMPORTANT]  
>  No se aplica el valor AUTOMATED_BACKUP_PREFERENCE. La interpretación de esta preferencia depende de la lógica, si existe, del script con los trabajos de copia de seguridad ejecutado para las bases de datos de un grupo de disponibilidad dado. La configuración de preferencia de copia de seguridad automatizada no tiene ningún efecto sobre las copias de seguridad ad hoc. Para obtener más información, vea [Configurar copia de seguridad en réplicas de disponibilidad &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).  
  
> [!NOTE]  
>  Para ver la preferencia de copia de seguridad automatizada de un grupo de disponibilidad existente, seleccione la **automated_backup_preference** o **automated_backup_preference_desc** columna de la [ Sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) vista de catálogo. Además, [sys.fn_hadr_backup_is_preferred_replica &#40; Transact-SQL &#41; ](../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md) puede utilizarse para determinar la réplica de copia de seguridad preferida.  Esta función devuelve 1 para al menos una de las réplicas, incluso cuando `AUTOMATED_BACKUP_PREFERENCE = NONE`.  
  
 FAILURE_CONDITION_LEVEL  **=**  {1 | 2 | **3** | 4 | 5}  
 Especifica qué condiciones de error desencadenan una conmutación por error automática para este grupo de disponibilidad. FAILURE_CONDITION_LEVEL se establece en el nivel de grupo, pero sólo es relevante en réplicas de disponibilidad que están configuradas para el modo de disponibilidad de confirmación sincrónica (AVAILIBILITY_MODE  **=**  SYNCHRONOUS_COMMIT). Además, las condiciones de error pueden desencadenar una conmutación por error automática solamente si las réplicas principales y secundarias están configuradas para el modo de conmutación automática por error (FAILOVER_MODE  **=**  automática) y la réplica secundaria sincronizada actualmente con la réplica principal.  
  
 Los niveles de condición de error (1-5) abarcan desde el nivel menos restrictivo (1) al más restrictivo (5). Un nivel de condición dado abarca todos los niveles menos restrictivos. Así pues, el nivel de condición más estricto (el nivel 5) incluye los cuatro niveles de condición menos restrictivos (1-4), el nivel 4 incluye los niveles 1-3, y así sucesivamente. En la tabla siguiente se describe la condición de error correspondiente a cada nivel.  
  
|Nivel|Condición de error|  
|-----------|-----------------------|  
|1|Especifica que se debe iniciar una conmutación por error automática en los casos siguientes:<br /><br /> -El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio no está funcionando.<br /><br /> -La concesión del grupo de disponibilidad para conectarse al clúster de WSFC expira porque no se ha recibido ninguna confirmación de la instancia del servidor. Para obtener más información, vea [Cómo funciona: tiempo de espera de concesión de AlwaysOn de SQL Server](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-AlwaysOn-lease-timeout.aspx).|  
|2|Especifica que se debe iniciar una conmutación por error automática en los casos siguientes:<br /><br /> -La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se conecta al clúster, y se supera el umbral HEALTH_CHECK_TIMEOUT especificado por el usuario del grupo de disponibilidad.<br /><br /> -La réplica de disponibilidad está en estado de error.|  
|3|Especifica que se debe iniciar una conmutación automática por error en caso de errores internos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] graves, como bloqueos por subproceso huérfanos, infracciones graves de acceso de escritura o un volcado excesivo.<br /><br /> Éste es el comportamiento predeterminado.|  
|4|Especifica que se debe iniciar una conmutación automática por error en caso de errores internos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] moderados, tales como una condición persistente de memoria insuficiente en el grupo de recursos de servidor interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|5|Especifica que se debe iniciar una conmutación por error automática en el caso de condiciones de error designadas, incluidas las siguientes:<br /><br /> -Agotamiento de subprocesos de trabajo del motor de SQL.<br /><br /> -La detección de un interbloqueo irresoluble.|  
  
> [!NOTE]  
>  La falta de respuesta de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a solicitudes del cliente no se aplica a los grupos de la disponibilidad.  
  
 Los valores FAILURE_CONDITION_LEVEL y HEALTH_CHECK_TIMEOUT definen una *directiva de conmutación por error flexible* para un grupo determinado. Esta directiva flexible de conmutación por error proporciona mayor control sobre las condiciones que deben causar una conmutación por error automática. Para obtener más información, vea [directiva de conmutación por error Flexible para conmutación automática por error de un grupo de disponibilidad &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
 HEALTH_CHECK_TIMEOUT  **=**  *milisegundos*  
 Especifica el tiempo de espera (en milisegundos) para la [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) sistema procedimiento almacenado para devolver información de estado del servidor antes de que el clúster de WSFC se da por supuesto que la instancia del servidor es lenta o se ha bloqueado. HEALTH_CHECK_TIMEOUT se establece en el nivel de grupo, pero sólo es relevante en réplicas de disponibilidad que están configuradas para el modo de disponibilidad de confirmación sincrónica con conmutación automática por error (AVAILIBILITY_MODE  **=**  SINCRÓNICA _COMMIT).  Además, un tiempo de espera de comprobación de estado puede desencadenar una conmutación por error automática solamente si las réplicas principales y secundarias están configuradas para el modo de conmutación automática por error (FAILOVER_MODE  **=**  automática) y la base de datos secundaria réplica está sincronizada actualmente con la réplica principal.  
  
 El valor predeterminado de HEALTH_CHECK_TIMEOUT es 30000 milisegundos (30 segundos). El valor mínimo es 15000 milisegundos (15 segundos) y el valor máximo es 4294967295 milisegundos.  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** no realiza comprobaciones de estado en el nivel de base de datos.  
  
 DB_FAILOVER  **=**  {ON | {OFF}  
 Especifica la respuesta que se realiza cuando una base de datos en la réplica principal está sin conexión. Cuando se establece en ON, cualquier estado distinto de ONLINE para una base de datos del grupo de disponibilidad desencadena una conmutación por error automática. Cuando esta opción se establece en OFF, solo el estado de la instancia se utiliza para desencadenar la conmutación automática por error.  
  
  Para obtener más información sobre esta configuración, consulte [opción de detección de estado de nivel de base de datos](../../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md) 
  
 DTC_SUPPORT  **=**  {PER_DB | NINGUNO}  
 Especifica si se admiten las transacciones entre bases de datos mediante el Coordinador de transacciones distribuidas (DTC). Solo se admiten las transacciones entre bases de datos a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. PER_DB crea el grupo de disponibilidad con compatibilidad con estas transacciones. Para obtener más información, vea [Transacciones entre bases de datos y transacciones distribuidas para la creación de reflejo de la base de datos o grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
 BASIC  
 Se utiliza para crear un grupo de disponibilidad básica. Grupos de disponibilidad básica se limitan a una base de datos y dos réplicas: una réplica principal y una réplica secundaria. Esta opción es un sustituto de la base de datos en desuso creación de reflejo de la característica en SQL Server Standard Edition. Para obtener más información, vea [grupos de disponibilidad básica &#40; Siempre en grupos de disponibilidad &#41; ](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md). Grupos de disponibilidad básica se admiten a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  

 DISTRIBUTED  
 Se utiliza para crear un grupo de disponibilidad distribuido. Esta opción se usa con el parámetro AVAILABILITY GROUP ON para conectar dos grupos de disponibilidad en clústeres de conmutación por error de Windows Server.  Para obtener más información, vea [Distributed Availability Groups &#40;Always On Availability Groups&#41; (Grupos de disponibilidad distribuida &#40;grupos de disponibilidad AlwaysOn&#41;)](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md). Grupos de disponibilidad distribuidos se admiten a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. 

 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT   
 Se introdujo en SQL Server de 2017. Se usa para establecer un número mínimo de las réplicas secundarias sincrónicas debe confirmar antes de la réplica principal confirma una transacción. Garantiza que las transacciones de SQL Server espera hasta que se actualizan los registros de transacciones en el número mínimo de las réplicas secundarias. El valor predeterminado es 0, que proporciona el mismo comportamiento que SQL Server 2016. El valor mínimo es 0. El valor máximo es el número de réplicas menos 1. Esta opción se relaciona con las réplicas en el modo de confirmación sincrónica. Cuando las réplicas están en modo de confirmación sincrónica, escrituras en la réplica principal esperan hasta que se escribe en las réplicas secundarias sincrónicas en el registro de transacciones de la base de datos de réplica. Si un servidor SQL Server que hospeda una réplica secundaria sincrónica deja de responder, el servidor SQL Server que hospeda la réplica principal marca las réplicas secundarias no SINCRONIZADAS y continuar. Cuando se pone en línea la base de datos que no responden se encuentra en un estado "no sincronizado" y la réplica se marca como en mal estado hasta que el servidor principal puede ser sincrónico nuevo. Esta configuración garantiza que la réplica principal espera hasta que el número mínimo de las réplicas haya confirmado cada transacción. Si el número mínimo de réplicas no está disponible, a continuación, se confirma en la réplica principal producirá un error. Para el tipo de clúster `EXTERNAL` se cambia dicha configuración cuando se agrega el grupo de disponibilidad a un recurso de clúster. Vea [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](../../linux/sql-server-linux-availability-group-ha.md).

 CLUSTER_TYPE  
 Se introdujo en SQL Server de 2017. Se usa para identificar si el grupo de disponibilidad está en un clúster de conmutación por error de Windows Server (WSFC).  Se establece en WSFC al grupo de disponibilidad está en una instancia de clúster de conmutación por error en un clúster de conmutación por error de Windows Server. Establece en externa cuando el clúster está administrado por un administrador de clústeres que no es un clúster de conmutación por error de Windows Server, como Linux marcapasos. Se establece en NONE cuando los grupos de disponibilidad no usa WSFC para la coordinación de clúster. Por ejemplo, cuando un grupo de disponibilidad incluye servidores Linux con ningún administrador de clústeres. 

 DATABASE *database_name*  
 Especifica una lista de una o varias bases de datos de usuario en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (es decir, la instancia de servidor en la que se crea el grupo de disponibilidad). Puede especificar varias bases de datos para un grupo de disponibilidad, pero cada base de datos puede pertenecer a solo un grupo de disponibilidad. Para obtener información sobre el tipo de bases de datos que puede admitir un grupo de disponibilidad, consulte [requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md). Para averiguar qué bases de datos locales ya pertenecen a un grupo de disponibilidad, consulte el **replica_id** columna en el [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) vista de catálogo.  
  
 La cláusula DATABASE es opcional. Si se omite, el nuevo grupo de disponibilidad está vacío.  
  
 Una vez haya creado el grupo de disponibilidad, conectarse a cada instancia del servidor que hospeda una réplica secundaria y, a continuación, prepare cada base de datos secundaria y unir al grupo de disponibilidad. Para obtener más información, vea [Iniciar el movimiento de datos en una base de datos secundaria AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
> [!NOTE]  
>  Más adelante, podrá agregar las bases de datos que reúnan los requisitos en la instancia del servidor que hospede la réplica principal actual para un grupo de disponibilidad. También puede quitar una base de datos secundaria de un grupo de disponibilidad. Para obtener más información, vea [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md).  
  
 REPLICA ON  
 Especifica de una a cinco instancias de SQL Server para que hospeden réplicas de disponibilidad en el nuevo grupo de disponibilidad.  Cada réplica se especifica mediante la dirección de su instancia de servidor seguida de una cláusula WITH (…). Como mínimo, debe especificar la instancia del servidor local, que se convierte en la réplica principal inicial. Opcionalmente, puede especificar también hasta cuatro réplicas secundarias.  
  
 Debe unir cada réplica secundaria al grupo de disponibilidad. Para obtener más información, vea [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md).  
  
> [!NOTE]  
>  Si especifica menos de cuatro réplicas secundarias al crear un grupo de disponibilidad, puede agregar una réplica secundaria adicional en cualquier momento mediante el [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción. También puede utilizar esta instrucción para quitar réplicas secundarias de un grupo de disponibilidad existente.  
  
 \<instancia_del_sevidor > especifica la dirección de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que es el host para una réplica. El formato de la dirección depende de si la instancia es la instancia predeterminada o una instancia con nombre y de si es una instancia independiente o una instancia de clúster de conmutación por error (FCI), tal como sigue:  
  
 { '*nombre_sistema*[\\*nombre_instancia*]' | '*nombre_red_FCI*[\\*nombre_instancia*]' }  
  
 Los componentes de esta dirección son los siguientes:  
  
 *nombre_sistema*  
 Es el nombre de NetBIOS del equipo en el que reside la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este equipo debe ser un nodo de WSFC.  
  
 *nombre_red_FCI*  
 Es el nombre de red que se utiliza para tener acceso a un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Utilice este argumento si la instancia de servidor participa como asociado de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ejecución de SELECT [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md) en una FCI instancia del servidor devuelve su totalidad '*nombre_red_fci*[\\*instance_name*]' cadena (que es el nombre de la réplica completa).  
  
 *nombre_instancia*  
 Es el nombre de una instancia de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hospedada por *system_name* o *nombre_red_fci* y HADR no tiene el servicio está habilitado. En el caso de una instancia del servidor predeterminada, *nombre_instancia* es opcional. El nombre de la instancia no distingue mayúsculas de minúsculas. En una instancia de servidor independiente, este nombre de valor es el mismo que el valor devuelto por la ejecución de SELECT [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md).  
  
 \  
 Es un separador que se usa solo cuando se especifica *instance_name*, para separarlo de *system_name* o *nombre_red_fci*.  
  
 Para obtener información acerca de los requisitos previos para los nodos WSFC y las instancias de servidor, consulte [requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 ENDPOINT_URL **='**TCP**://***system-address***:***port***'**  
 Especifica la ruta de acceso de dirección URL para el [extremo de reflejo de la base de datos](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md) en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la réplica de disponibilidad que se está definiendo en la cláusula REPLICA ON actual.  
  
 La cláusula ENDPOINT_URL es obligatoria. Para obtener más información, vea [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
 **'**TCP**://***system-address***:***port***'**  
 Determina una dirección URL para especificar una dirección URL del extremo o una dirección URL de enrutamiento de solo lectura. Los parámetros de la dirección URL son como sigue:  
  
 *system-address*  
 Es una cadena, como un nombre de sistema, un nombre de dominio completo o una dirección IP, que identifica sin ambigüedad el equipo de destino.  
  
 *port*  
 Es un número de puerto que está asociado al extremo de creación de reflejo de la instancia del servidor asociado (para la opción de ENDPOINT_URL) o al número de puerto que utiliza [!INCLUDE[ssDE](../../includes/ssde-md.md)] de la instancia del servidor (para la opción de READ_ONLY_ROUTING_URL).  
  
 AVAILABILITY_MODE  **=**  {{SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY}  
 SYNCHRONOUS_COMMIT o ASYNCHRONOUS_COMMIT especifica si la réplica principal tiene que esperar la réplica secundaria confirme la protección (escritura) de las entradas del registro en el disco antes de la réplica principal puede confirmar la transacción en un determinado elemento principal base de datos. Las transacciones realizadas en diferentes bases de datos en la misma réplica principal se pueden confirmar de manera independiente. SQL Server de 2017 CU 1 presenta CONFIGURATION_ONLY. Réplica CONFIGURATION_ONLY solo se aplica a los grupos de disponibilidad con CLUSTER_TYPE = externo o CLUSTER_TYPE = NONE. 
  
 SYNCHRONOUS_COMMIT  
 Especifica que la réplica principal espera la confirmación de transacciones hasta que se hayan protegido en esta réplica secundaria (modo de confirmación sincrónica). Puede especificar SYNCHRONOUS_COMMIT hasta para tres réplicas, incluida la réplica principal.  
  
 ASYNCHRONOUS_COMMIT  
 Especifica que la réplica principal confirma las transacciones sin esperar a que esta réplica secundaria proteja el registro (modo de disponibilidad de confirmación sincrónica). Puede especificar ASYNCHRONOUS_COMMIT hasta para cinco réplicas de disponibilidad, incluida la réplica principal.  

 CONFIGURATION_ONLY especifica que la réplica principal sincrónicamente confirmar los metadatos de configuración del grupo de disponibilidad en la base de datos maestra en esta réplica. La réplica no contiene datos de usuario. Esta opción:

- Se pueden hospedar en cualquier edición de SQL Server, incluida la Express Edition.
- Requiere el extremo de reflejo de la réplica CONFIGURATION_ONLY como tipo de datos `WITNESS`.
- No se pueden modificar.
- No es válida cuando `CLUSTER_TYPE = WSFC`. 

   Para obtener más información, consulte [única réplica de configuración](../../linux/sql-server-linux-availability-group-ha.md).
  
 La cláusula AVAILABILITY_MODE es obligatoria. Para obtener más información, vea [Modos de disponibilidad &#40;grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).  
  
 FAILOVER_MODE  **=**  {AUTOMÁTICA | MANUAL}  
 Especifica el modo de conmutación por error de la réplica de disponibilidad que está definiendo.  
  
 AUTOMATIC  
 Habilita la conmutación por error automática. Esta opción solo se admite si especifica también AVAILABILITY_MODE = SYNCHRONOUS_COMMIT. Puede especificar AUTOMATIC para dos réplicas de disponibilidad, incluida la réplica principal.  
  
> [!NOTE]  
>  Las instancias de clúster de conmutación por error (FCI) de SQL Server no admiten la conmutación automática por error de grupos de disponibilidad, por lo tanto, todas las réplicas de disponibilidad hospedadas por un FCI solo se pueden configurar para la conmutación por error manual.  
  
 MANUAL  
 Habilita manual conmutación por error planeada o forzada la conmutación por error manual (suele denominarse *conmutación por error forzada*) por el Administrador de base de datos.  
  
 La cláusula FAILOVER_MODE es obligatoria. Los dos tipos de conmutación por error manual, la conmutación por error manual sin pérdida de datos y la conmutación por error forzada (con posible pérdida de datos), se admiten en diferentes condiciones. Para obtener más información, vea [Conmutación por error y modos de conmutación por error &#40;Grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).  
  
 SEEDING_MODE  **=**  {AUTOMÁTICA | MANUAL}  
 Especifica cómo se propagando inicialmente la réplica secundaria.  
  
 AUTOMATIC  
 Habilita la propagación directa. Este método propaga la réplica secundaria a través de la red. Este método no requiere una copia de seguridad y restaurar una copia de la base de datos principal en la réplica.  
  
> [!NOTE]  
>  Para la propagación directa, deberá permitir crear base de datos en cada réplica secundaria mediante una llamada a **ALTER AVAILABILITY GROUP** con el **GRANT CREATE ANY DATABASE** opción.  
  
 MANUAL  
 Especifica la propagación manual (valor predeterminado). Este método debe crear una copia de seguridad de la base de datos en la réplica principal y restaurar manualmente la copia de seguridad en la réplica secundaria.  
  
 BACKUP_PRIORITY  **=** *n*  
 Especifica la prioridad para realizar copias de seguridad en esta réplica en relación con las otras réplicas del mismo grupo de disponibilidad. El valor es un número entero en el intervalo de 0..100. Estos valores tienen los significados siguientes:  
  
-   1..100 indica que la réplica de disponibilidad se podría elegir para realizar copias de seguridad. 1 indica la prioridad mínima y 100 indica la prioridad máxima. Si BACKUP_PRIORITY = 1, la réplica de disponibilidad se elegiría para realizar copias de seguridad solamente si no hay réplicas más prioritarias disponibles actualmente.  
  
-   0 indica que esta réplica de disponibilidad no es para realizar copias de seguridad. Esto es útil, por ejemplo, para una réplica de disponibilidad remota en la que no desee nunca realizar la conmutación por error para las copias de seguridad.  
  
 Para obtener más información, vea [Secundarias activas: copia de seguridad en las réplicas secundarias &#40;Grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).  
  
 SECONDARY_ROLE **(** ... **)**  
 Especifica la configuración de rol específica que se aplicará si esta réplica de disponibilidad posee actualmente el rol secundario (es decir, siempre que sea una réplica secundaria). Dentro de los paréntesis, especifique una o ambas de las opciones de rol secundario. Si se especifican ambas, utilice una lista separada por comas.  
  
 Las opciones de rol secundario son las siguientes:  
  
 ALLOW_CONNECTIONS  **=**  {N | READ_ONLY | ALL}  
 Especifica si las bases de datos de una réplica de disponibilidad determinada que está realizando el rol secundario (es decir, actuando como réplica secundaria) pueden aceptar conexiones de los clientes; uno de los tipos de conexión siguientes:  
  
 NO  
 No se permiten conexiones de usuario a las bases de datos secundarias de esta réplica. No están disponibles para acceso de lectura. Éste es el comportamiento predeterminado.  
  
 READ_ONLY  
 Solo se permiten conexiones a las bases de datos de la réplica secundaria donde la propiedad Application Intent se establece en **ReadOnly**. Para obtener más información acerca de esta propiedad, vea [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 ALL  
 Se permiten todas las conexiones con las bases de datos de la réplica secundaria para acceso de solo lectura.  
  
 Para obtener más información, vea [Secundarias activas: réplicas secundarias legibles &#40;Grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 READ_ONLY_ROUTING_URL **='**TCP**://***system-address***:***port***'**  
 Especifica la dirección URL que se va a usar para enrutar las solicitudes de conexión de intención de lectura de enrutamiento para esta réplica de disponibilidad. Es la dirección URL en la que escucha el motor de base de datos de SQL Server. Normalmente, la instancia predeterminada del motor de base de datos de SQL Server escucha en el puerto TCP 1433.  
  
 Para una instancia con nombre, se puede obtener el número de puerto consultando la **puerto** y **type_desc** columnas de la [sys.dm_tcp_listener_states](../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md) vista de administración dinámica. La instancia del servidor utiliza el agente de escucha de Transact-SQL (**type_desc = 'TSQL'**).  
  
 Para obtener más información acerca de cómo calcular la URL de enrutamiento de solo lectura para una réplica, vea [calcular read_only_routing_url para AlwaysOn](http://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-AlwaysOn.aspx).  
  
> [!NOTE]  
>  En el caso de una instancia con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se debe configurar el agente de escucha de Transact-SQL para que use un puerto específico. Para obtener más información, vea [Configurar un servidor para que escuche en un puerto TCP específico &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
 PRIMARY_ROLE **(** ... **)**  
 Especifica la configuración de rol específica que se aplicará si esta réplica de disponibilidad posee actualmente el rol principal (es decir, siempre que sea la réplica principal). Dentro de los paréntesis, especifique una o ambas de las opciones de rol primarias. Si se especifican ambas, utilice una lista separada por comas.  
  
 El rol principal de las opciones es el siguiente:  
  
 ALLOW_CONNECTIONS  **=**  {READ_WRITE | ALL}  
 Especifica el tipo de conexión que la base de datos de una réplica de disponibilidad determinada que está realizando el rol principal (es decir, actuando como réplica principal) puede aceptar de los clientes; uno de los tipos de conexión siguientes:  
  
 READ_WRITE  
 No se permiten las conexiones en las que la propiedad de conexión Application Intent esté establecida en **ReadOnly** .  Cuando la propiedad Application Intent está establecida en **ReadWrite** o no tiene ningún valor, se permite la conexión. Para obtener más información sobre propiedad de conexión Application Intent, vea [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 ALL  
 Se permiten todas las conexiones con las bases de datos de la réplica principal. Éste es el comportamiento predeterminado.  
  
 READ_ONLY_ROUTING_LIST  **=**  { **('**\<instancia_de_servidor >**'** [ **,**... *n* ] **)** | Ninguno} especifica una lista separada por comas de instancias de servidor que hospedan réplicas de disponibilidad para este grupo de disponibilidad que cumplen los requisitos siguientes cuando se ejecuta en el rol secundario:  
  
-   Está configurado para permitir todas las conexiones o las conexiones de solo lectura (vea el argumento ALLOW_CONNECTIONS de la opción SECONDARY_ROLE de más arriba).  
  
-   Tiene definida su dirección URL de enrutamiento de solo lectura (vea el argumento READ_ONLY_ROUTING_URL de la opción de SECONDARY_ROLE de más arriba).  
  
 Estos son los valores de READ_ONLY_ROUTING_LIST:  
  
 \<instancia_de_servidor > especifica la dirección de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que es el host para una réplica que tiene una réplica secundaria legible cuando se ejecuta en el rol secundario.  
  
 Use una lista separada por comas para especificar todas las instancias del servidor que pueden hospedar una réplica secundaria inteligible. Enrutamiento de solo lectura, sigue el orden en el servidor que las instancias se especifican en la lista. Si incluye la instancia del servidor de host de una réplica en la lista de enrutamiento de solo lectura de la réplica, por lo general, resulta recomendable colocar esta instancia del servidor al final de la lista, ya que las conexiones de intención de lectura van a una réplica secundaria, si hay alguna disponible. .  
  
 A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], puede que las solicitudes de lectura de equilibrio de carga entre las réplicas secundarias legibles. Esto se especifica mediante la colocación de las réplicas en un conjunto de paréntesis en la lista de enrutamiento de solo lectura anidado. Para obtener más información y ejemplos, vea [configurar el equilibrio de carga entre réplicas de solo lectura](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing).  
  
 Ninguno  
 Especifica que cuando esta réplica de disponibilidad es la réplica principal, enrutamiento de solo lectura no se admite. Éste es el comportamiento predeterminado.  
  
 SESSION_TIMEOUT  **=**  *entero*  
 Especifica el período de espera de la sesión en segundos. Si no especifica esta opción, el período equivale a 10 segundos de forma predeterminada. El valor mínimo es de 5 segundos.  
  
> [!IMPORTANT]  
>  Es recomendable que mantenga el período de espera en 10 segundos o más.  
  
 Para obtener más información sobre el período de tiempo de espera de sesión, vea [información general de grupos de disponibilidad AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
 GRUPO DE DISPONIBILIDAD EN  
 Especifica dos grupos de disponibilidad que constituyen una *grupo de disponibilidad distribuido*. Cada grupo de disponibilidad forma parte de su propio clúster de conmutación por error de Windows Server (WSFC). Cuando se crea un grupo de disponibilidad distribuidos, el grupo de disponibilidad en la instancia actual de SQL Server se convierte en el grupo de disponibilidad principal. El segundo grupo de disponibilidad se convierte en el grupo de disponibilidad secundaria.  
  
 Debe unirse al grupo de disponibilidad secundaria al grupo de disponibilidad distribuido. Para obtener más información, vea [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md).  
  
 \<ag_name > especifica el nombre del grupo de disponibilidad que constituye una mitad del grupo de disponibilidad distribuidos.  
  
 LISTENER **='**TCP**://***system-address***:***port***'**  
 Especifica la ruta de acceso de dirección URL para el agente de escucha asociado al grupo de disponibilidad.  
  
 La cláusula de agente de escucha es obligatoria.  
  
 **'**TCP**://***system-address***:***port***'**  
 Especifica una dirección URL para el agente de escucha asociado al grupo de disponibilidad. Los parámetros de la dirección URL son como sigue:  
  
 *system-address*  
 Es una cadena, como un nombre de sistema, un nombre de dominio completo o una dirección IP, que identifica de forma inequívoca el agente de escucha.  
  
 *port*  
 Es un número de puerto que está asociado con el extremo de reflejo del grupo de disponibilidad. Tenga en cuenta que esto no es el puerto del agente de escucha.  
  
 AVAILABILITY_MODE  **=**  {SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY}  
 Especifica si la réplica principal tiene que esperar para que el grupo de disponibilidad secundaria confirme la protección (escritura) de las entradas del registro en el disco antes de la réplica principal puede confirmar la transacción en una base de datos principal.  
  
 SYNCHRONOUS_COMMIT  
 Especifica que la réplica principal espera la confirmación de transacciones hasta que se hayan protegido en el grupo de disponibilidad secundaria. Puede especificar SYNCHRONOUS_COMMIT hasta dos grupos de disponibilidad, incluido el grupo de disponibilidad principal.  
  
 ASYNCHRONOUS_COMMIT  
 Especifica que la réplica principal confirma las transacciones sin esperar a este grupo de disponibilidad secundaria proteger el registro. Puede especificar ASYNCHRONOUS_COMMIT hasta dos grupos de disponibilidad, incluido el grupo de disponibilidad principal.  
  
 La cláusula AVAILABILITY_MODE es obligatoria.  
  
 FAILOVER_MODE  **=**  {MANUAL}  
 Especifica el modo de conmutación por error del grupo de disponibilidad distribuidos.  
  
 MANUAL  
 Habilita manual conmutación por error planeada o forzada la conmutación por error manual (suele denominarse *conmutación por error forzada*) por el Administrador de base de datos.  
  
 La cláusula FAILOVER_MODE es obligatoria y la única opción es MANUAL. No se admite la conmutación por error automática al grupo de disponibilidad secundario.  
  
 SEEDING_MODE  **=**  {AUTOMÁTICA | MANUAL}  
 Especifica cómo se propagando inicialmente el grupo de disponibilidad secundaria.  
  
 AUTOMATIC  
 Habilita la propagación directa. Este método propaga el grupo de disponibilidad secundaria a través de la red. Este método no requiere una copia de seguridad y restaurar una copia de la base de datos principal en las réplicas del grupo de disponibilidad secundaria.  
  
 MANUAL  
 Especifica la propagación manual (valor predeterminado). Este método debe crear una copia de seguridad de la base de datos en la réplica principal y restaurar manualmente la copia de seguridad en las réplicas del grupo de disponibilidad secundaria.  
  
 Agente de escucha **'***dns_name***' (** \<listener_option > **)** define un nuevo agente de escucha del grupo de disponibilidad para este grupo de disponibilidad. LISTENER es un argumento opcional.  
  
> [!IMPORTANT]  
>  Antes de crear su primer agente de escucha, recomendamos encarecidamente que lea [crear o configurar un agente de escucha del grupo de disponibilidad &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
>   
>  Después de crear un agente de escucha para un grupo de disponibilidad determinado, es absolutamente recomendable que haga lo siguiente:  
>   
>  -   Pida al administrador de red que reserve la dirección IP del agente de escucha para su uso exclusivo.  
> -   Proporcione el nombre del host DNS del agente de escucha a los desarrolladores de aplicaciones para que lo usen en las cadenas de conexión cuando soliciten conexiones cliente a este grupo de disponibilidad.  
  
 *dns_name*  
 Especifica el nombre de host DNS del agente de escucha del grupo de disponibilidad. El nombre DNS del agente de escucha debe ser único en el dominio y en NetBIOS.  
  
 *dns_name* es un valor de cadena. Este nombre solo puede contener caracteres alfanuméricos, guiones (-) y caracteres de subrayado (_), en cualquier orden. Los nombres de host DNS no distinguen entre mayúsculas y minúsculas. La longitud máxima es de 63 caracteres.  
  
 Es recomendable que especifique una cadena que tenga sentido. Por ejemplo, para un grupo de disponibilidad denominado `AG1`, un nombre de host DNS significativo sería `ag1-listener`.  
  
> [!IMPORTANT]  
>  NetBIOS reconoce solo los 15 primeros caracteres en dns_name. Si tiene dos clústeres WSFC controlados por el mismo Active Directory e intenta crear agentes de escucha de grupo de disponibilidad en ambos clústeres utilizando nombres con más de 15 caracteres y un prefijo idéntico de 15 caracteres, un error informa de que la red el Virtual Recurso de nombre no se pudo poner en línea. Para obtener información acerca de las reglas de nomenclatura de prefijos para los nombres DNS, vea [Asignación de nombres de dominio](http://technet.microsoft.com/library/cc731265\(WS.10\).aspx).  
  
 \<listener_option > LISTENER toma uno de los siguientes \<listener_option > opciones: 
  
 CON DHCP [ON { **('***four_part_ipv4_address***','***four_part_ipv4_mask***')** }]  
 Especifica que el agente de escucha del grupo de disponibilidad usa el protocolo de configuración dinámica de Host (DHCP).  Si lo desea, utilice la cláusula ON para identificar la red en el que se creó este agente de escucha. DHCP está limitado a una sola subred que se utiliza para las instancias de servidor que hospeda una réplica del grupo de disponibilidad.  
  
> [!IMPORTANT]  
>  No se recomienda DHCP en el entorno de producción. Si hay un tiempo de inactividad y expira la concesión de IP para DHCP, se necesitará más tiempo para registrar la nueva dirección IP de red DHCP que está asociada con el nombre DNS de escucha, lo que puede afectar a la conectividad de cliente. Sin embargo, DHCP es adecuado para configurar el entorno de desarrollo y pruebas para comprobar características básicas de los grupos de disponibilidad y para la integración con las aplicaciones.  
  
 Por ejemplo:  
  
 `WITH DHCP ON ('10.120.19.0','255.255.254.0')`  
  
 WITH IP **(** { **(‘***four_part_ipv4_address***’,‘***four_part_ipv4_mask***’)** | **(‘***ipv6_address***’)** } [ **,** ...*n* ] **)** [ **,** PORT **=***listener_port* ]  
 Especifica que, en lugar de utilizar DHCP, el agente de escucha del grupo de disponibilidad usa uno o más direcciones IP estáticas. Para crear un grupo de disponibilidad a través de varias subredes, cada subred requiere una dirección IP estática en la configuración de la escucha. Para una subred determinada, la dirección IP estática puede ser una dirección IPv4 o una dirección IPv6. Póngase en contacto con el Administrador de red para obtener una dirección IP estática para cada subred que hospeda una réplica para el nuevo grupo de disponibilidad.  
  
 Por ejemplo:  
  
 `WITH IP ( ('10.120.19.155','255.255.254.0') )`  
  
 *four_part_ipv4_address*  
 Especifica una dirección IPv4 de cuatro partes para el agente de escucha de un grupo de disponibilidad. Por ejemplo, `10.120.19.155`.  
  
 *four_part_ipv4_mask*  
 Especifica una máscara IPv4 de cuatro partes para el agente de escucha de un grupo de disponibilidad. Por ejemplo, `255.255.254.0`.  
  
 *ipv6_address*  
 Especifica una dirección IPv6 para el agente de escucha de un grupo de disponibilidad. Por ejemplo, `2001::4898:23:1002:20f:1fff:feff:b3a3`.  
  
 PUERTO  **=**  *listener_port*  
 Especifica el número de puerto:*listener_port*— que va a usar un agente de escucha del grupo de disponibilidad especificado por una cláusula WITH IP. PORT es opcional.  
  
 Se admite el número de puerto predeterminado, 1433. Sin embargo, si le preocupa la seguridad, le recomendamos que use otro número de puerto.  
  
 Por ejemplo: `WITH IP ( ('2001::4898:23:1002:20f:1fff:feff:b3a3') ) , PORT = 7777`  
  
## <a name="prerequisites-and-restrictions"></a>Requisitos previos y restricciones  
 Para obtener información sobre los requisitos previos para la creación de un grupo de disponibilidad, consulte [requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 Para obtener información acerca de las restricciones en las instrucciones de Transact-SQL AVAILABILITY GROUP, consulte [información general de instrucciones de Transact-SQL para grupos de disponibilidad AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md).  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Se requiere la pertenencia al rol fijo de servidor **sysadmin** y el permiso de servidor CREATE AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-configuring-backup-on-secondary-replicas-flexible-failover-policy-and-connection-access"></a>A. Configurar la copia de seguridad en réplicas secundarias, la directiva flexible de conmutación por error y el acceso de conexión  
 En el ejemplo siguiente se crea un grupo de disponibilidad denominado `MyAg` para dos bases de datos de usuario, `ThisDatabase` y `ThatDatabase`. En la tabla siguiente se resumen los valores especificados para las opciones establecidas en el grupo de disponibilidad en conjunto.  
  
|Opción de grupo|Configuración|Description|  
|------------------|-------------|-----------------|  
|AUTOMATED_BACKUP_PREFERENCE|SECONDARY|Esta preferencia de copia de seguridad automatizada indica que las copias de seguridad deben aparecer en una réplica secundaria, excepto cuando la réplica principal es la única réplica en línea (este es el comportamiento predeterminado). Para que el valor de AUTOMATED_BACKUP_PREFERENCE surta efecto, debe crear scripts de trabajos de copia de seguridad en las bases de datos de disponibilidad para tener en cuenta la preferencia de copia de seguridad automatizada.|  
|FAILURE_CONDITION_LEVEL|3|Este nivel de condición de error especifica que se debe iniciar una conmutación por error automática en caso de errores internos graves de SQL Server, como bloqueos por subprocesos huérfanos, infracciones graves de acceso de escritura o un volcado excesivo.|  
|HEALTH_CHECK_TIMEOUT|600000|Este valor de tiempo de espera de comprobación de mantenimiento, 60 segundos, especifica que el clúster de WSFC esperará 60000 milisegundos para la [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) procedimiento para devolver información de estado del servidor sobre una instancia del servidor que está almacenado del sistema hospeda una réplica de confirmación sincrónica automática antes de que el clúster se da por supuesto que la instancia del servidor host es lenta o se ha bloqueado. (El valor predeterminado es 30000 segundos).|  
  
 Tres réplicas de disponibilidad se hospedan en las instancias del servidor predeterminadas en los equipos denominados `COMPUTER01`, `COMPUTER02` y `COMPUTER03`. En la tabla siguiente se resumen los valores especificados para las opciones de cada réplica.  
  
|Opción de réplica|Valor en `COMPUTER01`|Valor en `COMPUTER02`|Valor en `COMPUTER03`|Description|  
|--------------------|-----------------------------|-----------------------------|-----------------------------|-----------------|  
|ENDPOINT_URL|TCP://*COMPUTER01:5022*|TCP://*COMPUTER02:5022*|TCP://*COMPUTER03:5022*|En este ejemplo, los sistemas están en el mismo dominio, por lo que las direcciones URL de extremo pueden usar el nombre del equipo como dirección del sistema.|  
|AVAILABILITY_MODE|SYNCHRONOUS_COMMIT|SYNCHRONOUS_COMMIT|ASYNCHRONOUS_COMMIT|Dos de las réplicas usan el modo de confirmación sincrónica. Cuando están sincronizadas, admiten la conmutación por error sin pérdida de datos. La tercera réplica, que usa el modo de disponibilidad de confirmación asincrónica.|  
|FAILOVER_MODE|AUTOMATIC|AUTOMATIC|MANUAL|Las réplicas de confirmación sincrónica admiten la conmutación automática por error y la conmutación por error manual planeada. La réplica en modo de disponibilidad de confirmación sincrónica solo admite la conmutación por error manual forzada.|  
|BACKUP_PRIORITY|30|30|90|Una prioridad más alta, 90, se asigna a la réplica de confirmación asincrónica que a las réplicas de confirmación sincrónica. Las copias de seguridad tienden a aparecer en la instancia del servidor que hospeda la réplica de confirmación asincrónica.|  
|SECONDARY_ROLE|( ALLOW_CONNECTIONS = NO,<br /><br /> READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01:1433' )|( ALLOW_CONNECTIONS = NO,<br /><br /> READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02:1433' )|( ALLOW_CONNECTIONS = READ_ONLY, <br />READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03:1433' )|Solo la réplica de confirmación asincrónica actúa como réplica secundaria legible.<br /><br /> Especifica el nombre del equipo y el número de puerto del motor de base de datos predeterminado (1433).<br /><br /> Este argumento es opcional.|  
|PRIMARY_ROLE|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = (COMPUTER03) )|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = (COMPUTER03) )|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = NONE )|En el rol principal, todas las réplicas rechazan los intentos de conexión de intención de lectura.<br /><br /> Las solicitudes de conexión de intención de lectura se enrutan a COMPUTER03 si la réplica local se ejecuta en el rol secundario. Cuando la réplica se ejecuta en rol principal, el enrutamiento de solo lectura está deshabilitado.<br /><br /> Este argumento es opcional.|  
|SESSION_TIMEOUT|10|10|10|Este ejemplo especifica el valor de tiempo de espera predeterminado (10). Este argumento es opcional.|  
  
 Finalmente, el ejemplo especifica la cláusula opcional LISTENER para crear un agente de escucha de grupo de disponibilidad para el nuevo grupo de disponibilidad. Un nombre DNS único, `MyAgListenerIvP6`, se especifica para este agente de escucha. Las dos réplicas están en varias subredes, por lo que el agente de escucha debe usar direcciones IP estáticas. Para cada una de las dos réplicas de disponibilidad, la cláusula WITH IP especifica una dirección IP estática, `2001:4898:f0:f00f::cf3c` y `2001:4898:e0:f213::4ce2`, que usan el formato IPv6. Este ejemplo especifica también que se use el argumento opcional PORT para definir el puerto `60173` como puerto de escucha.  
  
```SQL
CREATE AVAILABILITY GROUP MyAg   
   WITH (  
      AUTOMATED_BACKUP_PREFERENCE = SECONDARY,  
      FAILURE_CONDITION_LEVEL  =  3,   
      HEALTH_CHECK_TIMEOUT = 600000  
       )  
  
   FOR   
      DATABASE  ThisDatabase, ThatDatabase   
   REPLICA ON   
      'COMPUTER01' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC,  
         BACKUP_PRIORITY = 30,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = NO,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01:1433' ),
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER03) ),  
         SESSION_TIMEOUT = 10  
         ),   
  
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC,  
         BACKUP_PRIORITY = 30,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = NO,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER03) ),  
         SESSION_TIMEOUT = 10  
         ),   
  
      'COMPUTER03' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03:5022',  
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
         FAILOVER_MODE =  MANUAL,  
         BACKUP_PRIORITY = 90,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = NONE ),  
         SESSION_TIMEOUT = 10  
         );
GO  
ALTER AVAILABIIITY GROUP [MyAg]
  ADD LISTENER ‘MyAgListenerIvP6’ ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173 );   
GO  
```  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Crear un grupo de disponibilidad &#40; Transact-SQL &#41;](../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [Usar el Asistente para grupo de disponibilidad &#40; SQL Server Management Studio &#41;](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar el cuadro de diálogo Nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar el Asistente para grupo de disponibilidad &#40; SQL Server Management Studio &#41;](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Vea también  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [Quitar grupo de disponibilidad &#40; Transact-SQL &#41;](../../t-sql/statements/drop-availability-group-transact-sql.md)   
 [Solucionar problemas de configuración de grupos de disponibilidad &#40; AlwaysOn SQL Server &#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)   
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Agentes de escucha del grupo de disponibilidad, conectividad de cliente y conmutación por error de aplicación &#40; SQL Server &#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  

