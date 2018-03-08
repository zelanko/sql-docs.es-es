---
title: GRUPO de disponibilidad de ALTER (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/02/2018
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
- ALTER_AVAILABILITY_GROUP_TSQL
- ALTER_AVAILABILITY_TSQL
- ALTER AVAILABILITY GROUP
- ALTER AVAILABILITY
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- ALTER AVAILABILITY GROUP statement
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: f039d0de-ade7-4aaf-8b7b-d207deb3371a
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d9f18ee709fde7c9f239b08f553eaf43fad6e9d2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="alter-availability-group-transact-sql"></a>ALTER AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Modifica un existente grupo de disponibilidad AlwaysOn en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La mayoría de los argumentos de ALTER AVAILABILITY GROUP solo se admiten en la réplica principal actual. Sin embargo, los argumentos JOIN, FAILOVER y FORCE_FAILOVER_ALLOW_DATA_LOSS solo se admiten en réplicas secundarias.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```SQL  
  
ALTER AVAILABILITY GROUP group_name   
  {  
     SET ( <set_option_spec> )   
   | ADD DATABASE database_name   
   | REMOVE DATABASE database_name  
   | ADD REPLICA ON <add_replica_spec>   
   | MODIFY REPLICA ON <modify_replica_spec>  
   | REMOVE REPLICA ON <server_instance>  
   | JOIN  
   | JOIN AVAILABILITY GROUP ON <add_availability_group_spec> [ ,...2 ]  
   | MODIFY AVAILABILITY GROUP ON <modify_availability_group_spec> [ ,...2 ]  
   | GRANT CREATE ANY DATABASE  
   | DENY CREATE ANY DATABASE  
   | FAILOVER  
   | FORCE_FAILOVER_ALLOW_DATA_LOSS   | ADD LISTENER ‘dns_name’ ( <add_listener_option> )  
   | MODIFY LISTENER ‘dns_name’ ( <modify_listener_option> )  
   | RESTART LISTENER ‘dns_name’  
   | REMOVE LISTENER ‘dns_name’  
   | OFFLINE  
  }  
[ ; ]  
  
<set_option_spec> ::=   
    AUTOMATED_BACKUP_PREFERENCE = { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
  | FAILURE_CONDITION_LEVEL  = { 1 | 2 | 3 | 4 | 5 }   
  | HEALTH_CHECK_TIMEOUT = milliseconds  
  | DB_FAILOVER  = { ON | OFF }   
  | REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = { integer }
  
<server_instance> ::=   
 { 'system_name[\instance_name]' | 'FCI_network_name[\instance_name]' }  
  
<add_replica_spec>::=  
  <server_instance> WITH  
    (  
       ENDPOINT_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY },  
       FAILOVER_MODE = { AUTOMATIC | MANUAL }   
       [ , <add_replica_option> [ ,...n ] ]  
    )   
  
  <add_replica_option>::=  
       SEEDING_MODE = { AUTOMATIC | MANUAL }   
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
          ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL }   
        | READ_ONLY_ROUTING_URL = 'TCP://system-address:port'   
          } )  
     | PRIMARY_ROLE ( {   
          ALLOW_CONNECTIONS = { READ_WRITE | ALL }   
        | READ_ONLY_ROUTING_LIST = { ( ‘<server_instance>’ [ ,...n ] ) | NONE }   
          } )  
     | SESSION_TIMEOUT = seconds  
  
<modify_replica_spec>::=  
  <server_instance> WITH  
    (    
       ENDPOINT_URL = 'TCP://system-address:port'   
     | AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }   
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }   
     | SEEDING_MODE = { AUTOMATIC | MANUAL }   
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
          ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL }   
        | READ_ONLY_ROUTING_URL = 'TCP://system-address:port'   
          } )  
     | PRIMARY_ROLE ( {   
          ALLOW_CONNECTIONS = { READ_WRITE | ALL }   
        | READ_ONLY_ROUTING_LIST = { ( ‘<server_instance>’ [ ,...n ] ) | NONE }   
          } )  
     | SESSION_TIMEOUT = seconds  
    )   
  
<add_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = MANUAL,  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<modify_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER = 'TCP://system-address:port'  
       | AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
       | SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<add_listener_option> ::=  
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
  
<modify_listener_option>::=  
    {  
       ADD IP ( <ip_address_option> )   
     | PORT = listener_port  
    }  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *group_name*  
 Especifica el nombre del nuevo grupo de disponibilidad. *nombre_grupo* debe ser válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador y deben ser único en todos los grupos de disponibilidad del clúster de WSFC.  
  
 AUTOMATED_BACKUP_PREFERENCE  **=**  {PRINCIPAL | SECONDARY_ONLY | SECUNDARIO | NINGUNO}  
 Especifica una preferencia sobre cómo un trabajo de copia de seguridad debe evaluar la réplica principal cuando elige realizar copias de seguridad. Puede crear un script con un trabajo de copia de seguridad para que se tenga en cuenta la preferencia de copia de seguridad automatizada. Es importante entender que no se aplica la preferencia por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por lo que no tiene efecto en las copias de seguridad ad hoc.  
  
 Solo se admite en la réplica principal.  
  
 Éstos son sus valores:  
  
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
>  No se aplica el valor AUTOMATED_BACKUP_PREFERENCE. La interpretación de esta preferencia depende de la lógica, si existe, del script con los trabajos de copia de seguridad ejecutado para las bases de datos de un grupo de disponibilidad dado. La configuración de preferencia de copia de seguridad automatizada no influye en las copias de seguridad ad hoc. Para obtener más información, vea [Configurar copia de seguridad en réplicas de disponibilidad &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).  
  
> [!NOTE]  
>  Para ver la preferencia de copia de seguridad automatizada de un grupo de disponibilidad existente, seleccione la **automated_backup_preference** o **automated_backup_preference_desc** columna de la [ Sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) vista de catálogo. Además, [sys.fn_hadr_backup_is_preferred_replica &#40; Transact-SQL &#41; ](../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md) puede utilizarse para determinar la réplica de copia de seguridad preferida.  Esta función siempre devolverá 1 al menos para una de las réplicas, incluso aunque `AUTOMATED_BACKUP_PREFERENCE = NONE`.  
  
 FAILURE_CONDITION_LEVEL  **=**  {1 | 2 | **3** | 4 | 5}  
 Especifica qué condiciones de error desencadenarán una conmutación por error automática para este grupo de disponibilidad. FAILURE_CONDITION_LEVEL se establece en el nivel de grupo, pero sólo es relevante en réplicas de disponibilidad que están configuradas para el modo de disponibilidad de confirmación sincrónica (AVAILIBILITY_MODE  **=**  SYNCHRONOUS_COMMIT). Además, las condiciones de error pueden desencadenar una conmutación por error automática solamente si las réplicas principales y secundarias están configuradas para el modo de conmutación automática por error (FAILOVER_MODE  **=**  automática) y la réplica secundaria sincronizada actualmente con la réplica principal.  
  
 Solo se admite en la réplica principal.  
  
 Los niveles de condición de error (1-5) abarcan desde el nivel menos restrictivo (1) al más restrictivo (5). Un nivel de condición dado abarca todos los niveles menos restrictivos. Así pues, el nivel de condición más estricto (el nivel 5) incluye los cuatro niveles de condición menos restrictivos (1-4), el nivel 4 incluye los niveles 1-3, y así sucesivamente. En la tabla siguiente se describe la condición de error correspondiente a cada nivel.  
  
|Nivel|Condición de error|  
|-----------|-----------------------|  
|1|Especifica que se debe iniciar una conmutación por error automática en los casos siguientes:<br /><br /> El servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está inactivo.<br /><br /> La concesión del grupo de disponibilidad para conectarse al clúster de WSFC expira porque no se ha recibido ninguna confirmación de la instancia del servidor. Para obtener más información, vea [Cómo funciona: tiempo de espera de concesión de AlwaysOn de SQL Server](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx).|  
|2|Especifica que se debe iniciar una conmutación por error automática en los casos siguientes:<br /><br /> La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se conecta al clúster y se ha superado el umbral de HEALTH_CHECK_TIMEOUT del grupo de disponibilidad especificado por el usuario.<br /><br /> La réplica de disponibilidad tiene un estado de error.|  
|3|Especifica que se debe iniciar una conmutación automática por error en caso de errores internos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] graves, como bloqueos por subproceso huérfanos, infracciones graves de acceso de escritura o un volcado excesivo.<br /><br /> Éste es el comportamiento predeterminado.|  
|4|Especifica que se debe iniciar una conmutación automática por error en caso de errores internos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] moderados, tales como una condición persistente de memoria insuficiente en el grupo de recursos de servidor interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|5|Especifica que se debe iniciar una conmutación por error automática en el caso de condiciones de error designadas, incluidas las siguientes:<br /><br /> Se han agotado los subprocesos de trabajo del motor de SQL.<br /><br /> Detección de un interbloqueo irresoluble.|  
  
> [!NOTE]  
>  La falta de respuesta de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a solicitudes del cliente no se aplica a los grupos de la disponibilidad.  
  
 Los valores FAILURE_CONDITION_LEVEL y HEALTH_CHECK_TIMEOUT definen una *directiva de conmutación por error flexible* para un grupo determinado. Esta directiva flexible de conmutación por error proporciona mayor control sobre las condiciones que deben causar una conmutación por error automática. Para obtener más información, vea [directiva de conmutación por error Flexible para conmutación automática por error de un grupo de disponibilidad &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
 HEALTH_CHECK_TIMEOUT  **=**  *milisegundos*  
 Especifica el tiempo de espera (en milisegundos) para la [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) sistema procedimiento almacenado para devolver información de estado del servidor antes de que el clúster WSFC se da por supuesto que la instancia del servidor es lenta o se ha bloqueado. HEALTH_CHECK_TIMEOUT se establece en el nivel de grupo, pero sólo es relevante en réplicas de disponibilidad que están configuradas para el modo de disponibilidad de confirmación sincrónica con conmutación automática por error (AVAILIBILITY_MODE  **=**  SINCRÓNICA _COMMIT).  Además, un tiempo de espera de comprobación de estado puede desencadenar una conmutación por error automática solamente si las réplicas principales y secundarias están configuradas para el modo de conmutación automática por error (FAILOVER_MODE  **=**  automática) y la base de datos secundaria réplica está sincronizada actualmente con la réplica principal.  
  
 El valor predeterminado de HEALTH_CHECK_TIMEOUT es 30000 milisegundos (30 segundos). El valor mínimo es 15000 milisegundos (15 segundos) y el valor máximo es 4294967295 milisegundos.  
  
 Solo se admite en la réplica principal.  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** no realiza comprobaciones de estado en el nivel de base de datos.  
  
 DB_FAILOVER  **=**  {ON | {OFF}  
 Especifica la respuesta que se realiza cuando una base de datos en la réplica principal está sin conexión. Cuando se establece en ON, cualquier estado distinto de ONLINE para una base de datos del grupo de disponibilidad desencadena una conmutación por error automática. Cuando esta opción se establece en OFF, solo el estado de la instancia se utiliza para desencadenar la conmutación automática por error.  
 
 Para obtener más información sobre esta configuración, consulte [opción de detección de estado de nivel de base de datos](../../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md) 

 
 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT   
 Se introdujo en SQL Server de 2017. Se usa para establecer un número mínimo de las réplicas secundarias sincrónicas debe confirmar antes de la réplica principal confirma una transacción. Garantiza que las transacciones de SQL Server esperará hasta que se actualizan los registros de transacciones en el número mínimo de las réplicas secundarias. El valor predeterminado es 0, que proporciona el mismo comportamiento que SQL Server 2016. El valor mínimo es 0. El valor máximo es el número de réplicas menos 1. Esta opción se relaciona con las réplicas en el modo de confirmación sincrónica. Cuando las réplicas están en modo de confirmación sincrónica, escrituras en la réplica principal esperan hasta que se escribe en las réplicas secundarias sincrónicas en el registro de transacciones de la base de datos de réplica. Si un servidor SQL Server que hospeda una réplica secundaria sincrónica deja de responder, el servidor SQL Server que hospeda la réplica principal marcará esa réplica secundaria como no SINCRONIZADAS y continuar. Cuando la base de datos que no responden se pone en línea estará en un estado "no sincronizado" y la réplica se marcará como en mal estado hasta que el servidor principal puede ser sincrónico nuevo. Esta configuración garantiza que la réplica principal no continuará hasta que el número mínimo de las réplicas haya confirmado cada transacción. Si el número mínimo de réplicas no está disponible, a continuación, se producirá un error confirmaciones en la réplica principal. Para el tipo de clúster `EXTERNAL` se cambia dicha configuración cuando se agrega el grupo de disponibilidad a un recurso de clúster. Vea [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](../../linux/sql-server-linux-availability-group-ha.md).
  
 Agregar base de datos *database_name*  
 Especifica una lista de una o más bases de datos de usuario que desea agregar al grupo de disponibilidad. Es preciso que estas bases de datos residan en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la réplica principal actual. Puede especificar varias bases de datos para un grupo de disponibilidad, pero cada base de datos puede pertenecer a solo un grupo de disponibilidad. Para obtener información sobre el tipo de bases de datos que puede admitir un grupo de disponibilidad, consulte [requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md). Para averiguar qué bases de datos locales ya pertenecen a un grupo de disponibilidad, consulte el **replica_id** columna en el [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) vista de catálogo.  
  
 Solo se admite en la réplica principal.  
  
> [!NOTE]  
>  Una vez haya creado la disponibilidad del grupo, deberá conectarse a cada instancia del servidor que hospede una réplica secundaria y, posteriormente, preparar cada base de datos secundaria y combinarla con la disponibilidad de grupo. Para obtener más información, vea [Iniciar el movimiento de datos en una base de datos secundaria AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
 Quitar base de datos *database_name*  
 Quita la base de datos principal especificada y las bases de datos secundarias correspondientes del grupo de disponibilidad. Solo se admite en la réplica principal.  
  
 Para obtener información acerca de los pasos recomendados después de quitar una base de datos de disponibilidad de un grupo de disponibilidad, consulte [quitar una base de datos principal de un grupo de disponibilidad &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md).  
  
 ADD REPLICA ON  
 Especifica de una a ocho instancias de SQL Server para que hospeden las réplicas secundarias de un grupo de disponibilidad.  Cada réplica se especifica mediante la dirección de su instancia de servidor seguida de una cláusula WITH (…).  
  
 Solo se admite en la réplica principal.  
  
 Debe unir cada réplica secundaria nueva al grupo de disponibilidad. Para obtener más información, vea la descripción de la opción JOIN, más adelante en esta sección.  
  
 \<server_instance>  
 Especifica la dirección de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que es el host para una réplica. El formato de la dirección depende de si la instancia es la instancia predeterminada o una instancia con nombre y de si es una instancia independiente o una instancia de clúster de conmutación por error (FCI). La sintaxis es la siguiente:  
  
 { '*nombre_sistema*[\\*nombre_instancia*]' | '*nombre_red_FCI*[\\*nombre_instancia*]' }  
  
 Los componentes de esta dirección son los siguientes:  
  
 *nombre_sistema*  
 Es el nombre de NetBIOS del equipo en el que reside la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este equipo debe ser un nodo de WSFC.  
  
 *nombre_red_FCI*  
 Es el nombre de red que se utiliza para tener acceso a un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Utilice este argumento si la instancia de servidor participa como asociado de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ejecución de SELECT [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md) en una FCI instancia del servidor devuelve su totalidad '*nombre_red_fci*[\\*instance_name*]' cadena (que es el nombre de la réplica completa).  
  
 *nombre_instancia*  
 Es el nombre de una instancia de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hospedada por *system_name* o *nombre_red_fci* y que tenga siempre en habilitado. En el caso de una instancia del servidor predeterminada, *nombre_instancia* es opcional. El nombre de la instancia no distingue mayúsculas de minúsculas. En una instancia de servidor independiente, este nombre de valor es el mismo que el valor devuelto por la ejecución de SELECT [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md).  
  
 \  
 Es un separador que se usa solo cuando se especifica *instance_name*, para separarlo de *system_name* o *nombre_red_fci*.  
  
 Para obtener información acerca de los requisitos previos para los nodos WSFC y las instancias de servidor, consulte [requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 ENDPOINT_URL ='TCP://*system-address*:*port*'  
 Especifica la ruta de acceso de dirección URL para el [extremo de reflejo de la base de datos](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md) en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que va a hospedar la réplica de disponibilidad que está agregando o modificando.  
  
 ENDPOINT_URL es obligatorio en la cláusula ADD REPLICA ON y opcional en la cláusula MODIFY REPLICA ON.  Para obtener más información, vea [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
 **'**TCP**://***system-address***:***port***'**  
 Determina una dirección URL para especificar una dirección URL del extremo o una dirección URL de enrutamiento de solo lectura. Los parámetros de la dirección URL son como sigue:  
  
 *system-address*  
 Es una cadena, como un nombre de sistema, un nombre de dominio completo o una dirección IP, que identifica sin ambigüedad el equipo de destino.  
  
 *port*  
 Es un número de puerto que está asociado al extremo de creación de reflejo de la instancia del servidor (para la opción de ENDPOINT_URL) o en el número de puerto que utiliza [!INCLUDE[ssDE](../../includes/ssde-md.md)] de la instancia del servidor (para la opción de READ_ONLY_ROUTING_URL).  
  
 AVAILABILITY_MODE  **=**  {SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY}  
 Especifica si la réplica principal tiene que esperar a que la réplica secundaria confirme la protección (escritura) de los registros en el disco para poder confirmar la transacción en una base de datos principal dada. Las transacciones realizadas en diferentes bases de datos en la misma réplica principal se pueden confirmar de manera independiente.  
  
 SYNCHRONOUS_COMMIT  
 Especifica que la réplica principal esperará a confirmar las transacciones hasta que se hayan protegido en la réplica secundaria (modo de confirmación sincrónica). Puede especificar SYNCHRONOUS_COMMIT hasta para tres réplicas, incluida la réplica principal.  
  
 ASYNCHRONOUS_COMMIT  
 Especifica que la réplica principal confirma las transacciones sin esperar a que esta réplica secundaria proteja el registro (modo de disponibilidad de confirmación sincrónica). Puede especificar ASYNCHRONOUS_COMMIT hasta para cinco réplicas de disponibilidad, incluida la réplica principal.  

 CONFIGURATION_ONLY especifica que la réplica principal sincrónicamente confirmar los metadatos de configuración del grupo de disponibilidad en la base de datos maestra en esta réplica. La réplica no contiene datos de usuario. Esta opción:

- Se pueden hospedar en cualquier edición de SQL Server, incluida la Express Edition.
- Requiere el extremo de reflejo de la réplica CONFIGURATION_ONLY como tipo de datos `WITNESS`.
- No se pueden modificar.
- No es válida cuando `CLUSTER_TYPE = WSFC`. 

   Para obtener más información, consulte [única réplica de configuración](../../linux/sql-server-linux-availability-group-ha.md).
    
 AVAILABILITY_MODE es obligatorio en la cláusula ADD REPLICA ON y opcional en la cláusula MODIFY REPLICA ON. Para obtener más información, vea [Modos de disponibilidad &#40;grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).  
  
 FAILOVER_MODE  **=**  {AUTOMÁTICA | MANUAL}  
 Especifica el modo de conmutación por error de la réplica de disponibilidad que está definiendo.  
  
 AUTOMATIC  
 Habilita la conmutación por error automática. AUTOMATIC solo se admite si se especifica también AVAILABILITY_MODE = SYNCHRONOUS_COMMIT. Puede especificar AUTOMATIC para dos réplicas de disponibilidad, incluida la réplica principal.  
  
> [!NOTE]  
>  Las instancias de clúster de conmutación por error (FCI) de SQL Server no admiten la conmutación automática por error de grupos de disponibilidad, por lo tanto, todas las réplicas de disponibilidad hospedadas por un FCI solo se pueden configurar para la conmutación por error manual.  
  
 MANUAL  
 Habilita la conmutación por error manual o la conmutación por error manual forzada (*conmutación por error forzada*) por el Administrador de base de datos.  
  
 FAILOVER_MODE es obligatorio en la cláusula ADD REPLICA ON y opcional en la cláusula MODIFY REPLICA ON. Existen dos tipos de conmutación por error manual, la conmutación por error manual sin pérdida de datos y la conmutación por error forzada (con pérdida de datos posible), que se admiten en diferentes condiciones.  Para obtener más información, vea [Conmutación por error y modos de conmutación por error &#40;Grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).  
  
 SEEDING_MODE  **=**  {AUTOMÁTICA | MANUAL}  
 Especifica cómo la réplica secundaria inicialmente propagará.  
  
 AUTOMATIC  
 Habilita la propagación directa. Este método va a inicializar la réplica secundaria a través de la red. Este método no requiere una copia de seguridad y restaurar una copia de la base de datos principal en la réplica.  
  
> [!NOTE]  
>  Para la propagación directa, deberá permitir crear base de datos en cada réplica secundaria mediante una llamada a **ALTER AVAILABILITY GROUP** con el **GRANT CREATE ANY DATABASE** opción.  
  
 MANUAL  
 Especifica la propagación manual (valor predeterminado). Este método debe crear una copia de seguridad de la base de datos en la réplica principal y restaurar manualmente la copia de seguridad en la réplica secundaria.  
  
 BACKUP_PRIORITY **=***n*  
 Especifica la prioridad para realizar copias de seguridad en esta réplica en relación con las otras réplicas del mismo grupo de disponibilidad. El valor es un número entero en el intervalo de 0..100. Estos valores tienen los significados siguientes:  
  
-   1..100 indica que la réplica de disponibilidad se podría elegir para realizar copias de seguridad. 1 indica la prioridad mínima y 100 indica la prioridad máxima. Si BACKUP_PRIORITY = 1, la réplica de disponibilidad se elegiría para realizar copias de seguridad solamente si no hay réplicas más prioritarias disponibles actualmente.  
  
-   0 indica que esta réplica de disponibilidad nunca se elegirá para realizar copias de seguridad. Esto es útil, por ejemplo, para una réplica de disponibilidad remota en la que no desee nunca realizar la conmutación por error para las copias de seguridad.  
  
 Para obtener más información, vea [Secundarias activas: copia de seguridad en las réplicas secundarias &#40;Grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).  
  
 SECONDARY_ROLE **(** ... **)**  
 Especifica la configuración específica del rol que se aplicará si esta réplica de disponibilidad posee actualmente el rol secundario (es decir, siempre que sea una réplica secundaria). Dentro de los paréntesis, especifique una o ambas de las opciones de rol secundario. Si se especifican ambas, utilice una lista separada por comas.  
  
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
  
 Para obtener más información acerca de cómo calcular la URL de enrutamiento de solo lectura para una réplica de disponibilidad, consulte [calcular read_only_routing_url para AlwaysOn](http://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-Always%20On.aspx).  
  
> [!NOTE]  
>  En el caso de una instancia con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se debe configurar el agente de escucha de Transact-SQL para que use un puerto específico. Para obtener más información, vea [Configurar un servidor para que escuche en un puerto TCP específico &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
 PRIMARY_ROLE **(** ... **)**  
 Especifica la configuración específica del rol que se aplicará si esta réplica de disponibilidad posee actualmente el rol primario (es decir, siempre que sea la réplica primaria). Dentro de los paréntesis, especifique una o ambas de las opciones de rol primarias. Si se especifican ambas, utilice una lista separada por comas.  
  
 El rol principal de las opciones es el siguiente:  
  
 ALLOW_CONNECTIONS  **=**  {READ_WRITE | ALL}  
 Especifica el tipo de conexión que la base de datos de una réplica de disponibilidad determinada que está realizando el rol principal (es decir, actuando como réplica principal) puede aceptar de los clientes; uno de los tipos de conexión siguientes:  
  
 READ_WRITE  
 No se permiten las conexiones en las que la propiedad de conexión Application Intent esté establecida en **ReadOnly** .  Cuando la propiedad Application Intent está establecida en **ReadWrite** o no tiene ningún valor, se permite la conexión. Para obtener más información sobre propiedad de conexión Application Intent, vea [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 ALL  
 Se permiten todas las conexiones con las bases de datos de la réplica principal. Éste es el comportamiento predeterminado.  
  
 READ_ONLY_ROUTING_LIST  **=**  { **('**\<instancia_de_servidor >**'** [ **,**... *n* ] **)** | NINGUNO}  
 Especifica una lista separada por comas de instancias de servidor que hospedan réplicas de disponibilidad para este grupo de disponibilidad y que cumplen los requisitos siguientes al ejecutarse con el rol secundario:  
  
-   Está configurado para permitir todas las conexiones o las conexiones de solo lectura (vea el argumento ALLOW_CONNECTIONS de la opción SECONDARY_ROLE de más arriba).  
  
-   Tiene definida su dirección URL de enrutamiento de solo lectura (vea el argumento READ_ONLY_ROUTING_URL de la opción de SECONDARY_ROLE de más arriba).  
  
 Estos son los valores de READ_ONLY_ROUTING_LIST:  
  
 \<server_instance>  
 Especifica la dirección de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que es el host para una réplica de disponibilidad que es una réplica secundaria inteligible cuando se ejecuta en el rol secundario.  
  
 Use una lista separada por comas para especificar todas las instancias del servidor que pueden hospedar una réplica secundaria inteligible. El enrutamiento de solo lectura seguirá el orden en que las instancias de servidor se especifican en la lista. Si incluye la instancia del servidor de host de una réplica en la lista de enrutamiento de solo lectura de la réplica, por lo general, resulta recomendable colocar esta instancia del servidor al final de la lista, ya que las conexiones de intención de lectura van a una réplica secundaria, si hay alguna disponible. .  
  
 A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], puede que las solicitudes de lectura de equilibrio de carga entre las réplicas secundarias legibles. Esto se especifica mediante la colocación de las réplicas en un conjunto de paréntesis en la lista de enrutamiento de solo lectura anidado. Para obtener más información y ejemplos, vea [configurar el equilibrio de carga entre réplicas de solo lectura](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing).  
  
 Ninguno  
 Especifica que cuando esta réplica de disponibilidad es la réplica primaria, no se admitirá en el enrutamiento de solo lectura. Éste es el comportamiento predeterminado. Cuando se utiliza con MODIFY REPLICA ON, este valor deshabilita una lista existente, en caso de que la hubiera.  
  
 SESSION_TIMEOUT **= *** segundos*  
 Especifica el período de espera de la sesión en segundos. Si no especifica esta opción, el período equivale a 10 segundos de forma predeterminada. El valor mínimo es de 5 segundos.  
  
> [!IMPORTANT]  
>  Es recomendable que mantenga el período de espera en 10 segundos o más.  
  
 Para obtener más información sobre el período de tiempo de espera de sesión, vea [información general de grupos de disponibilidad AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
 MODIFY REPLICA ON  
 Modifica alguna de las réplicas del grupo de disponibilidad. La lista de réplicas que se van a modificar contiene la dirección de la instancia de servidor y una cláusula WITH (…) para cada réplica.  
  
 Solo se admite en la réplica principal.  
  
 REMOVE REPLICA ON  
 Quita la réplica secundaria especificada del grupo de disponibilidad. La réplica principal actual no se puede quitar de un grupo de disponibilidad. Cuando se quita, la réplica deja de recibir datos. Se quitan sus bases de datos secundarias del grupo de disponibilidad y se activa el estado RESTORING.  
  
 Solo se admite en la réplica principal.  
  
> [!NOTE]  
>  Si quita una réplica mientras no está disponible o está en estado de error, cuando vuelva a conectarla verá que ya no pertenece al grupo de disponibilidad.  
  
 JOIN  
 Hace que la instancia de servidor local hospede una réplica secundaria en el grupo de disponibilidad especificado.  
  
 Solo se admite en una réplica secundaria que no se haya combinado aún con un grupo de disponibilidad.  
  
 Para obtener más información, vea [Join a Secondary Replica to an Availability Group &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
 FAILOVER  
 Inicia una conmutación por error manual del grupo de disponibilidad sin pérdida de datos a la réplica secundaria a la que está conectado. La réplica en la que se escribe un comando de conmutación por error de destino de conmutación por error se conoce como el.  El destino de la conmutación por error asumirá el rol principal y recuperará su copia de cada base de datos y las pondrá en línea como las nuevas bases de datos principales. La réplica principal anterior realiza la transición de forma simultánea al rol secundario y sus bases de datos se convierten en bases de datos secundarias, además quedan suspendidas inmediatamente. Potencialmente, estos roles se pueden alternar mediante una serie de errores.  
  
 Solo se admite en una réplica secundaria de confirmación sincrónica que se sincronice actualmente con la réplica primaria. Tenga en cuenta que para sincronizar réplicas secundarias, la réplica principal también debe ejecutarse en modo de confirmación sincrónica.  
  
> [!NOTE]  
>  Un comando de conmutación por error realiza la devolución en cuanto el destino de la conmutación por error acepte el comando. Sin embargo, la recuperación de la base de datos se produce de forma asincrónica cuando el grupo de disponibilidad ha terminado la conmutación por error.  
  
 Para obtener información acerca de las limitaciones, consulte los requisitos previos y recomendaciones para realizar un manual conmutación por error planeada, [realizar un Manual conmutación por error planeada de un grupo de disponibilidad &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md).  
  
 FORCE_FAILOVER_ALLOW_DATA_LOSS  
 > [!CAUTION]  
>  Forzar la conmutación por error, que podría causar pérdida de datos, es estrictamente un método de recuperación ante desastres. Por lo tanto, es absolutamente recomendable que solo fuerce la conmutación por error si la réplica principal ya no se está ejecutando, si asume el riesgo de perder datos o si debe restaurar el servicio al grupo de disponibilidad inmediatamente.  
  
 Solo se admite en una réplica cuyo rol esté en el estado SECONDARY o RESOLVING. --La réplica en la que se escribe un comando de conmutación por error se conoce como el *destino de conmutación por error*.  
  
 Fuerza la conmutación por error del grupo de disponibilidad, con posible pérdida de datos, al destino de la conmutación por error. El destino de la conmutación por error asumirá el rol principal y recuperará su copia de cada base de datos y las pondrá en línea como las nuevas bases de datos principales. En cualquier réplica secundaria restante, cada base de datos secundaria se suspende hasta que se reanude manualmente. Cuando la réplica principal anterior está disponible, cambiará al rol secundario y sus bases de datos se convertirán en bases de datos secundarias suspendidas.  
  
> [!NOTE]  
>  Un comando de conmutación por error realiza la devolución en cuanto el destino de la conmutación por error acepte el comando. Sin embargo, la recuperación de la base de datos se produce de forma asincrónica cuando el grupo de disponibilidad ha terminado la conmutación por error.  
  
 Para obtener información acerca de las limitaciones, los requisitos previos y las recomendaciones para forzar la conmutación por error y el efecto de una conmutación por error forzada en las bases de datos principales anteriores en el grupo de disponibilidad, vea [realizar un Manual de conmutación por error forzada de una disponibilidad Grupo de &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md).  
  
 ADD LISTENER **‘***dns_name***’(** \<add_listener_option> **)**  
 Define un nuevo agente de escucha para este grupo de disponibilidad. Solo se admite en la réplica principal.  
  
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
>  NetBIOS reconoce solo los 15 primeros caracteres en dns_name. Si tiene dos clústeres de WSFC controlados por la misma instancia de Active Directory e intenta crear agentes de escucha del grupo de disponibilidad en los dos clústeres utilizando nombres con más de 15 caracteres y un prefijo idéntico de 15 caracteres, obtendrá un error notificando que el recurso de nombre de red virtual no se pudo poner en línea. Para obtener información acerca de las reglas de nomenclatura de prefijos para los nombres DNS, vea [Asignación de nombres de dominio](http://technet.microsoft.com/library/cc731265\(WS.10\).aspx).  
  
 UNIR EL GRUPO DE DISPONIBILIDAD EN  
 Se combina con un *grupo de disponibilidad distribuido*. Cuando se crea un grupo de disponibilidad distribuidos, el grupo de disponibilidad en el clúster donde se crea es el grupo de disponibilidad principal. El grupo de disponibilidad que se une al grupo de disponibilidad distribuidos es el grupo de disponibilidad secundaria.  
  
 \<ag_name>  
 Especifica el nombre del grupo de disponibilidad que constituye una mitad del grupo de disponibilidad distribuidos.  
  
 LISTENER **='**TCP**://***system-address***:***port***'**  
 Especifica la ruta de acceso de dirección URL para el agente de escucha asociado al grupo de disponibilidad.  
  
 La cláusula de agente de escucha es obligatoria.  
  
 **'**TCP**://***system-address***:***port***'**  
 Especifica una dirección URL para el agente de escucha asociado al grupo de disponibilidad. Los parámetros de la dirección URL son como sigue:  
  
 *system-address*  
 Es una cadena, como un nombre de sistema, un nombre de dominio completo o una dirección IP, que identifica de forma inequívoca el agente de escucha.  
  
 *port*  
 Es un número de puerto que está asociado con el extremo de reflejo del grupo de disponibilidad. Tenga en cuenta que esto no es el puerto del agente de escucha.  
  
 AVAILABILITY_MODE  **=**  {SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT}  
 Especifica si la réplica principal tiene que esperar para que el grupo de disponibilidad secundaria confirme la protección (escritura) de las entradas del registro en el disco antes de la réplica principal puede confirmar la transacción en una base de datos principal.  
  
 SYNCHRONOUS_COMMIT  
 Especifica que la réplica principal esperará a confirmar las transacciones hasta que se hayan protegido en el grupo de disponibilidad secundaria. Puede especificar SYNCHRONOUS_COMMIT hasta dos grupos de disponibilidad, incluido el grupo de disponibilidad principal.  
  
 ASYNCHRONOUS_COMMIT  
 Especifica que la réplica principal confirma las transacciones sin esperar a este grupo de disponibilidad secundaria proteger el registro. Puede especificar ASYNCHRONOUS_COMMIT hasta dos grupos de disponibilidad, incluido el grupo de disponibilidad principal.  
  
 La cláusula AVAILABILITY_MODE es obligatoria.  
  
 FAILOVER_MODE  **=**  {MANUAL}  
 Especifica el modo de conmutación por error del grupo de disponibilidad distribuidos.  
  
 MANUAL  
 Habilita manual conmutación por error planeada o forzada la conmutación por error manual (suele denominarse *conmutación por error forzada*) por el Administrador de base de datos.  
  
 No se admite la conmutación por error automática al grupo de disponibilidad secundario.  
  
 SEEDING_MODE **=**  {AUTOMÁTICA | MANUAL}  
 Especifica cómo el grupo de disponibilidad secundaria inicialmente propagará.  
  
 AUTOMATIC  
 Habilita la propagación automática. Este método va a inicializar el grupo de disponibilidad secundaria a través de la red. Este método no requiere una copia de seguridad y restaurar una copia de la base de datos principal en las réplicas del grupo de disponibilidad secundaria.  
  
 MANUAL  
 Especifica la propagación manual. Este método debe crear una copia de seguridad de la base de datos en la réplica principal y restaurar manualmente la copia de seguridad en las réplicas del grupo de disponibilidad secundaria.  
  
 MODIFICAR GRUPO DE DISPONIBILIDAD EN  
 Modifica cualquiera de las opciones de grupo de disponibilidad de un grupo de disponibilidad distribuido. La lista de grupos de disponibilidad modificarse contiene el nombre del grupo de disponibilidad y r con cláusula (...) para cada grupo de disponibilidad.  
  
> [!IMPORTANT]  
>  Este comando debe repetirse en el grupo de disponibilidad principal y las instancias de grupo de disponibilidad secundaria.  
  
 GRANT CREAR CUALQUIER BASE DE DATOS  
 Permite que el grupo de disponibilidad para crear bases de datos en nombre de la réplica principal, que es compatible con la propagación directa (SEEDING_MODE = AUTOMATIC). Este parámetro se debe ejecutar en cada réplica secundaria que es compatible con la propagación directa después de esa base de datos secundaria une al grupo de disponibilidad.  Requiere el permiso CREATE ANY DATABASE.  
  
 DENEGAR CREAR CUALQUIER BASE DE DATOS  
 Quita la capacidad del grupo de disponibilidad para crear bases de datos en nombre de la réplica principal.  
  
 \<add_listener_option>  
 ADD LISTENER toma una de las siguientes opciones:  
  
 CON DHCP [ON { **('***four_part_ipv4_address***','***four_part_ipv4_mask***')** }]  
 Especifica que el agente de escucha del grupo de disponibilidad utilizará el protocolo DHCP (Protocolo de configuración dinámica de host).  Opcionalmente, utilice la cláusula ON para identificar la red en la que se creará esta escucha. DHCP está limitado a una sola subred que se usa para cada instancia del servidor que hospeda una réplica de disponibilidad en el grupo de disponibilidad.  
  
> [!IMPORTANT]  
>  No se recomienda DHCP en el entorno de producción. Si hay un tiempo de inactividad y expira la concesión de IP para DHCP, se necesitará más tiempo para registrar la nueva dirección IP de red DHCP que está asociada con el nombre DNS de escucha, lo que puede afectar a la conectividad de cliente. Sin embargo, DHCP es adecuado para configurar el entorno de desarrollo y pruebas para comprobar características básicas de los grupos de disponibilidad y para la integración con las aplicaciones.  
  
 Por ejemplo:  
  
 `WITH DHCP ON ('10.120.19.0','255.255.254.0')`  
  
 WITH IP **(** { **(‘***four_part_ipv4_address***’,‘***four_part_ipv4_mask***’)** | **(‘***ipv6_address***’)** } [ **,** ...*n* ] **)** [ **,** PORT **=***listener_port* ]  
 Especifica que, en lugar de utilizar DHCP, la escucha del grupo de disponibilidad utilizará una o más direcciones IP estáticas. Para crear un grupo de disponibilidad a través de varias subredes, cada subred requiere una dirección IP estática en la configuración de la escucha. Para una subred determinada, la dirección IP estática puede ser una dirección IPv4 o una dirección IPv6. Póngase en contacto con el administrador de red para obtener una dirección IP estática para cada subred que hospeda una réplica de disponibilidad para el nuevo grupo de disponibilidad.  
  
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
  
 MODIFY LISTENER **‘***dns_name***’(** \<modify_listener_option> **)**  
 Modifica el agente de escucha de un grupo de disponibilidad existente para este grupo de disponibilidad. Solo se admite en la réplica principal.  
  
 \<modify_listener_option>  
 MODIFY LISTENER toma una de las siguientes opciones:  
  
 ADD IP { **(‘***four_part_ipv4_address***’,‘***four_part_ipv4_mask***’)** | **(‘**dns_name*ipv6_address***’)** }  
 Agrega la dirección IP especificada para el agente de escucha del grupo de disponibilidad especificado por *dns_name*.  
  
 PUERTO  **=**  *listener_port*  
 Vea la descripción de este argumento anteriormente en esta sección.  
  
 Reinicie el agente de escucha **'***dns_name***'**  
 Reinicia la escucha asociada con el nombre DNS especificado. Solo se admite en la réplica principal.  
  
 Quitar agente de escucha **'***dns_name***'**  
 Quita la escucha asociada con el nombre DNS especificado. Solo se admite en la réplica principal.  
  
 OFFLINE  
 Pone sin conexión un grupo de disponibilidad que está en línea. No se produce ninguna pérdida de datos para las bases de datos con confirmación sincrónica.  
  
 Cuando un grupo de disponibilidad pasa a estar sin conexión, sus bases de datos dejan de estar disponibles para los clientes y no puede volver a poner el grupo de disponibilidad en línea. Por tanto, use la opción OFFLINE solo durante la migración entre clústeres de [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], al migrar recursos de grupo de disponibilidad a un nuevo clúster de WSFC.  
  
 Para obtener más información, vea [poner un grupo de disponibilidad de sin conexión &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/take-an-availability-group-offline-sql-server.md).  
  
## <a name="prerequisites-and-restrictions"></a>Requisitos previos y restricciones  
 Para obtener información acerca de los requisitos previos y restricciones en las réplicas de disponibilidad y en sus equipos y las instancias del servidor host, consulte [requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 Para obtener información acerca de las restricciones en las instrucciones de Transact-SQL AVAILABILITY GROUP, consulte [información general de instrucciones de Transact-SQL para grupos de disponibilidad AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md).  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  También requiere el permiso ALTER ANY DATABASE.   
  
## <a name="examples"></a>Ejemplos  
  
###  <a name="Join_Secondary_Replica"></a> A. Unir una réplica secundaria a un grupo de disponibilidad  
 En el ejemplo siguiente se une al grupo de disponibilidad `AccountsAG` una réplica secundaria a la que está conectado.  
  
```SQL  
ALTER AVAILABILITY GROUP AccountsAG JOIN;  
GO  
```  
  
###  <a name="Force_Failover"></a> B. Forzar la conmutación por error de un grupo de disponibilidad  
 En el ejemplo siguiente se fuerza al grupo de disponibilidad `AccountsAG` a que realice una conmutación por error para la réplica secundaria a la que está conectado.  
  
```SQL
ALTER AVAILABILITY GROUP AccountsAG FORCE_FAILOVER_ALLOW_DATA_LOSS;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear grupo de disponibilidad &#40; Transact-SQL &#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [Quitar grupo de disponibilidad &#40; Transact-SQL &#41;](../../t-sql/statements/drop-availability-group-transact-sql.md)   
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Solucionar problemas de configuración de grupos de disponibilidad &#40; AlwaysOn SQL Server &#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)   
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Agentes de escucha del grupo de disponibilidad, conectividad de cliente y conmutación por error de aplicación &#40; SQL Server &#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  
