---
title: "MODIFICAR la configuración del servidor (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER SERVER CONFIGURATION
- ALTER_SERVER_CONFIGURATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER CONFIGURATION, ALTER
- process affinity, setting
- ALTER SERVER CONFIGURATION statement
- setting process affinity
ms.assetid: f3059e42-5f6f-4a64-903c-86dca212a4b4
caps.latest.revision: 72
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a4c406824e51b79b74403623a100f2fc355d28bc
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-server-configuration-transact-sql"></a>ALTER SERVER CONFIGURATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica las opciones de configuración global del servidor actual en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ALTER SERVER CONFIGURATION  
SET <optionspec>   
[;]  
  
<optionspec> ::=  
{  
     <process_affinity>  
   | <diagnostic_log>  
   | <failover_cluster_property>  
   | <hadr_cluster_context>  
   | <buffer_pool_extension>  
   | <soft_numa>  
}  
  
<process_affinity> ::=   
   PROCESS AFFINITY   
   {  
     CPU = { AUTO | <CPU_range_spec> }   
   | NUMANODE = <NUMA_node_range_spec>   
   }  
   <CPU_range_spec> ::=   
      { CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]   
  
   <NUMA_node_range_spec> ::=   
      { NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID } [ ,...n ]  
  
<diagnostic_log> ::=   
   DIAGNOSTICS LOG   
   {   
     ON    
   | OFF    
   | PATH = { 'os_file_path' | DEFAULT }    
   | MAX_SIZE = { 'log_max_size' MB | DEFAULT }    
   | MAX_FILES = { 'max_file_count' | DEFAULT }    
   }  
  
<failover_cluster_property> ::=   
   FAILOVER CLUSTER PROPERTY <resource_property>  
   <resource_property> ::=  
      {  
        VerboseLogging = { 'logging_detail' | DEFAULT }    
      | SqlDumperDumpFlags = { 'dump_file_type' | DEFAULT }  
      | SqlDumperDumpPath = { 'os_file_path'| DEFAULT }  
      | SqlDumperDumpTimeOut = { 'dump_time-out' | DEFAULT }  
      | FailureConditionLevel = { 'failure_condition_level' | DEFAULT }  
      | HealthCheckTimeout = { 'health_check_time-out' | DEFAULT }  
      }  
  
<hadr_cluster_context> ::=  
   HADR CLUSTER CONTEXT = { 'remote_windows_cluster' | LOCAL }  
  
<buffer_pool_extension>::=  
    BUFFER POOL EXTENSION   
    { ON ( FILENAME = 'os_file_path_and_name' , SIZE = <size_spec> )   
    | OFF }  
  
    <size_spec> ::=  
        { size [ KB | MB | GB ] }  
  
<soft_numa> ::=  
    SET SOFTNUMA  
    { ON | OFF }  
```  
  
## <a name="arguments"></a>Argumentos  
 **\<process_affinity >:: =**  
  
 PROCESS AFFINITY  
 Permite asociar los subprocesos de hardware a las CPU.  
  
 CPU = {AUTOMÁTICA | \<CPU_range_spec >}  
 Distribuye los subprocesos de trabajo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cada CPU dentro del rango especificado. Las CPU que no pertenezcan al rango especificado no tendrán subprocesos asignados.  
  
 AUTO  
 Especifica que los subprocesos no se asignan a ninguna CPU. El sistema operativo puede mover los subprocesos libremente entre las CPU según la carga de trabajo del servidor. Esta es la configuración predeterminada y recomendada.  
  
 \<CPU_range_spec >:: =  
 Especifica la CPU o el rango de las CPU a las que se asignan los subprocesos.  
  
 { CPU_ID | CPU_ID  TO  CPU_ID } [ ,...n ]  
 Es la lista de una o varias CPU. Identificadores de CPU comienzan en 0 y son **entero** valores.  
  
 NUMANODE = \<NUMA_node_range_spec >  
 Asigna subprocesos a todas las CPU que pertenecen al nodo o rango de nodos NUMA especificado.  
  
 \<NUMA_node_range_spec >:: =  
 Especifica el nodo o rango de nodos NUMA.  
  
 { NUMA_node_ID | NUMA_node_ID  TO NUMA_node_ID } [ ,...n ]  
 Es la lista de uno o varios nodos NUMA. Identificadores de nodos NUMA comienzan en 0 y son **entero** valores.  
  
 **\<diagnostic_log >:: =**  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 DIAGNOSTICS LOG  
 Inicia o detiene el registro de los datos de diagnóstico capturados por el procedimiento sp_server_diagnostics, y establece los parámetros de configuración del registro de SQLDIAG como el recuento de sustitución incremental del archivo de registro, el tamaño del archivo de registro y la ubicación del archivo. Para obtener más información, vea [Ver y leer el registro de diagnósticos de la instancia de clúster de conmutación por error](../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md).  
  
 ON  
 Inicia el registro de datos de diagnóstico de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] en la ubicación especificada en la opción de archivo PATH. Ésta es la opción predeterminada.  
  
 OFF  
 Detiene el registro de datos de diagnóstico.  
  
 PATH = { 'os_file_path' | DEFAULT }  
 Ruta de acceso que indica la ubicación de los registros de diagnóstico. La ubicación predeterminada es \<\MSSQL\Log > dentro de la carpeta de instalación de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia de clúster de conmutación por error.  
  
 MAX_SIZE = { 'log_max_size' MB | DEFAULT }  
 Tamaño máximo en megabytes que cada registro de diagnóstico puede alcanzar. El valor predeterminado es 100 MB.  
  
 MAX_FILES = { 'max_file_count' | DEFAULT }  
 Número máximo de archivos de registro de diagnóstico que pueden almacenarse en el equipo antes de que se reciclen para nuevos registros de diagnóstico.  
  
 **\<failover_cluster_property >:: =**  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 FAILOVER CLUSTER PROPERTY  
 Modifica las propiedades privadas de clúster de conmutación por error de recursos de SQL Server.  
  
 VERBOSE LOGGING = { 'logging_detail' | DEFAULT }  
 Establece el nivel de registro para clústeres de conmutación por error de SQL Server. Se puede activar para proporcionar detalles adicionales en los registros de errores para solucionar problemas.  
  
-   0: el registro está desactivado (valor predeterminado)  
  
-   1: solo errores  
  
-   2: errores y advertencias  
  
SQLDUMPEREDUMPFLAGS  
 Determina el tipo de archivos de volcado generados por la utilidad SQLDumper de SQL Server. El valor predeterminado es 0. Para obtener más información, consulte [artículo de Knowledge Base utilidad de SQL Server volcado](http://go.microsoft.com/fwlink/?LinkId=206173).  
  
 SQLDUMPERDUMPPATH = { 'os_file_path' | DEFAULT }  
 Ubicación donde la utilidad SQLDumper almacena los archivos de volcado. Para obtener más información, consulte [artículo de Knowledge Base utilidad de SQL Server volcado](http://go.microsoft.com/fwlink/?LinkId=206173).  
  
 SQLDUMPERDUMPTIMEOUT = { 'dump_time-out' | DEFAULT }  
 Valor de tiempo de espera en milisegundos para que la utilidad SQLDumper genere un volcado en caso de un error de SQL Server. El valor predeterminado es 0, lo que significa que no hay ningún límite de tiempo para completar el volcado. Para obtener más información, consulte [artículo de Knowledge Base utilidad de SQL Server volcado](http://go.microsoft.com/fwlink/?LinkId=206173).  
  
 FAILURECONDITIONLEVEL = { 'failure_condition_level' | DEFAULT }  
 Condiciones en que la instancia de clúster de conmutación por error de SQL Server debe producir la conmutación por error o reiniciarse. El valor predeterminado es 3, lo que significa que el recurso de SQL Server producirá la conmutación por error o se reiniciará en errores de servidor críticos. Para obtener más información sobre este y otros niveles de condición de error, consulte [configurar los valores de propiedad FailureConditionLevel](../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md).  
  
 HEALTHCHECKTIMEOUT = { 'health_check_time-out' | DEFAULT }  
 Valor de tiempo de espera que establece cuánto tiempo debe la DLL del recurso del motor de base de datos de SQL Server esperar la información de estado del servidor antes de considerar que la instancia de SQL Server no responde. El valor de tiempo de espera se expresa en milisegundos. El valor predeterminado es 60000 milisegundos (o 60 segundos).  
  
 **\<hadr_cluster_context >:: =**  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 CONTEXTO de clúster de HADR  **=**  { **'***remote_windows_cluster***'** | LOCAL}  
 Cambia el contexto de clúster de HADR de la instancia de servidor al clúster especificado de Clústeres de conmutación por error de Windows Server (WSFC). El *contexto de clúster HADR* determina qué clúster de clústeres de conmutación por error de servidor de Windows (WSFC) administra los metadatos para las réplicas de disponibilidad hospedadas por la instancia del servidor. Use la opción SET HADR CLUSTER CONTEXT solo durante una migración entre clústeres de [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] a una instancia de [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] o una versión posterior en un nuevo clúster de WSFC.  
  
 Solo puede cambiar el contexto de clúster de HADR desde el clúster local de WSFC a un clúster remoto y viceversa. El contexto de clúster de HADR se puede cambiar a un clúster remoto solo cuando la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no hospeda ninguna réplica de disponibilidad.  
  
 Un contexto de clúster de HADR remoto se puede volver a cambiar al clúster local en cualquier momento. Sin embargo, el contexto no se puede cambiar de nuevo si la instancia de servidor hospeda réplicas de disponibilidad.  
  
 Para identificar el clúster de destino, especifique uno de los valores siguientes:  
  
 *windows_cluster*  
 Nombre de objeto de clúster (CON) de un clúster de WSFC. Puede especificar el nombre corto o el nombre de dominio completo. Para buscar la dirección IP de destino de un nombre corto, ALTER SERVER CONFIGURATION usa la resolución de DNS. En algunos casos, un nombre corto puede producir confusiones y DNS podría devolver la dirección IP errónea. Por tanto, se recomienda especificar el nombre de dominio completo.  
  
 LOCAL  
 Clúster local de WSFC.  
  
 Para obtener más información, vea [cambiar el contexto de clúster de HADR de instancia servidor &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md).  
  
 **\<buffer_pool_extension >:: =**  
  
**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ON  
 Habilita la opción de extensión del grupo de búferes. Esta opción extiende el tamaño del grupo de búferes con almacenamiento no volátil como unidades de estado sólido (SSD) para conservar las páginas de datos limpias en el grupo. Para obtener más información sobre esta característica, consulte [Buffer Pool Extension](../../database-engine/configure-windows/buffer-pool-extension.md). La extensión del grupo de búferes no está disponible en cada edición de SQL Server. Para obtener más información, consulte [ediciones y características admitidas en SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 FILENAME = 'os_file_path_and_name'  
 Define la ruta de acceso al directorio y el nombre del archivo de la memoria caché de la extensión del grupo de búferes. La extensión de archivo se debe especificar como .BPE. Debe desactivar BUFFER POOL EXTENSION para poder modificar FILENAME.  
  
 TAMAÑO = *tamaño* [ **KB** | MB | GB]  
 Define el tamaño de la memoria caché. La especificación de tamaño predeterminado es KB. El tamaño mínimo es el de la Memoria de servidor máxima. El límite máximo es 32 veces el tamaño de Memoria de servidor máxima. Para obtener más información acerca de la memoria de servidor máxima, vea [sp_configure &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 Debe desactivar BUFFER POOL EXTENSION para poder modificar el tamaño del archivo. Para especificar un tamaño menor que el actual, la instancia de SQL Server debe reiniciarse para reclamar memoria. De lo contrario, el tamaño especificado debe ser igual o mayor que el actual.  
  
 OFF  
 Deshabilita la opción de extensión del grupo de búferes. Debe deshabilitar la opción de extensión del grupo de búferes antes de modificar los parámetros asociados como el tamaño o el nombre de archivo. Cuando esta opción está deshabilitada, toda la información de configuración relacionada se quita del Registro.  
  
> [!WARNING]  
>  Deshabilitar la extensión del grupo de búferes puede tener un impacto negativo en el rendimiento del servidor porque el tamaño del grupo de búferes se reduce significativamente.  
  
 **\<soft_numa >**  

**Se aplica a**: desde [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ON  
 Permite la creación automática de particiones dividir grandes nodos NUMA de hardware en los nodos NUMA más pequeños. Cambiar el valor de ejecución, requiere un reinicio del motor de base de datos.  
  
 OFF  
 Deshabilita el software automática creación de particiones de gran tamaño nodos NUMA de hardware en nodos NUMA más pequeños. Cambiar el valor de ejecución, requiere un reinicio del motor de base de datos.  

> [!WARNING]  
> Existen problemas conocidos con el comportamiento de la instrucción ALTER SERVER CONFIGURATION con la opción de NUMA de software y el Agente SQL Server.  La siguiente es la secuencia recomendada de operaciones:  
> 1) Detenga la instancia del Agente SQL Server.  
> 2) Ejecute la opción ALTER NUMA de software de servidor los.  
> 3) Vuelva a iniciar la instancia de SQL Server.  
> 4) Inicie la instancia del Agente SQL Server.  
  
**Obtener más información:** si se ejecuta una configuración de servidor ALTER con el comando SET SOFTNUMA antes de que se reinicie el servicio de SQL Server, a continuación, cuando se detiene el servicio Agente SQL Server, ejecutará un comando RECONFIGURE de T-SQL que se restablecerá la Configuración de SOFTNUMA a su estado original antes de ALTER SERVER CONFIGURATION. 
  
## <a name="general-remarks"></a>Notas generales  
 Esta instrucción no requiere un reinicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a menos que establezca explícitamente lo contrario. En el caso de una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no se requiere un reinicio del recurso de clúster de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Esta instrucción no admite desencadenadores DDL.  
  
## <a name="permissions"></a>Permissions  
 Necesita permisos ALTER SETTINGS para la opción de afinidad de proceso. Se necesitan permisos ALTER SETTINGS y VIEW SERVER STATE para las opciones de propiedad de clúster de conmutación por error y registro de diagnóstico, y el permiso CONTROL SERVER para la opción de contexto de clúster de HADR.  
  
 Requiere el permiso ALTER SERVER STATE para la opción de entension del grupo de búferes.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] recurso DLL se ejecuta bajo la cuenta Sistema Local. Por tanto, la cuenta de sistema local debe tener acceso de lectura y escritura a la ruta de acceso especificada en la opción de registro de diagnóstico.  
  
## <a name="examples"></a>Ejemplos  
  
|Categoría|Elementos de sintaxis ofrecidos|  
|--------------|------------------------------|  
|[Establecer afinidad de proceso](#Affinity)|CPU • NUMANODE • AUTO|  
|[Establecer las opciones del registro de diagnóstico](#Diagnostic)|ON • OFF • PATH • MAX_SIZE|  
|[Establecer propiedades de clúster de conmutación por error](#Failover)|HealthCheckTimeout|  
|[Cambiar el contexto de clúster de una réplica de disponibilidad](#ChangeClusterContextExample)|**'** *windows_cluster* **'**|  
|[Establecer la extensión del grupo de búferes](#BufferPoolExtension)|BUFFER POOL EXTENSION|  
  
###  <a name="Affinity"></a>Establecer afinidad de proceso  
 En los ejemplos de esta sección se muestra cómo establecer la afinidad de proceso en las CPU y nodos NUMA. En los ejemplos se supone que el servidor contiene 256 CPU organizadas en cuatro grupos de 16 nodos NUMA cada una. Los subprocesos no se asignan a ningún nodo NUMA ni a ninguna CPU.  
  
-   Grupo 0: nodos NUMA del 0 al 3, CPU de la 0 a la 63  
-   Grupo 1: Nodos NUMA del 4 al 7, CPUs 64 a 127  
-   Grupo 2: Nodos NUMA del 8 al 12, CPUs 128 a 191  
-   Grupo 3: nodos NUMA del 13 al 16, CPU de la 192 a la 255  
  
#### <a name="a-setting-affinity-to-all-cpus-in-groups-0-and-2"></a>A. Establecer la afinidad en todas las CPU de los grupos 0 y 2  
 En el ejemplo siguiente se establece la afinidad en todas las CPU de los grupos 0 y 2.  
  
```  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=0 TO 63, 128 TO 191;  
```  
  
#### <a name="b-setting-affinity-to-all-cpus-in-numa-nodes-0-and-7"></a>B. Establecer la afinidad en todas las CPU de los nodos NUMA 0 y 7  
 En el ejemplo siguiente únicamente se establece la afinidad de las CPU con los nodos `0` y `7`.  
  
```  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY NUMANODE=0, 7;  
```  
  
#### <a name="c-setting-affinity-to-cpus-60-through-200"></a>C. Establecer la afinidad en las CPU comprendidas entre la 60 y la 200  
 En el ejemplo siguiente se establece la afinidad de las CPU comprendidas entre la 60 y la 200.  
  
```  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=60 TO 200;  
```  
  
#### <a name="d-setting-affinity-to-cpu-0-on-a-system-that-has-two-cpus"></a>D. Establecer la afinidad en la CPU 0 para un sistema que tiene dos CPU  
 En el ejemplo siguiente se establece la afinidad en `CPU=0` para un equipo que tiene dos CPU. Antes de que se ejecute la instrucción siguiente, la máscara de bits de afinidad interna es 00.  
  
```  
ALTER SERVER CONFIGURATION SET PROCESS AFFINITY CPU=0;  
```  
  
#### <a name="e-setting-affinity-to-auto"></a>E. Establecer la afinidad en AUTO  
 En el siguiente ejemplo se establece la afinidad en `AUTO`.  
  
```  
ALTER SERVER CONFIGURATION  
SET PROCESS AFFINITY CPU=AUTO;  
```  
  
###  <a name="Diagnostic"></a> Setting diagnostic log options  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 En los ejemplos de esta sección se muestra cómo establecer los valores para la opción de registro de diagnóstico.  
  
#### <a name="a-starting-diagnostic-logging"></a>A. Iniciar el registro de diagnóstico  
 En el ejemplo siguiente se inicia el registro de los datos de diagnóstico.  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG ON;  
```  
  
#### <a name="b-stopping-diagnostic-logging"></a>B. Detener el registro de diagnóstico  
 En el ejemplo siguiente se detiene el registro de los datos de diagnóstico.  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG OFF;  
```  
  
#### <a name="c-specifying-the-location-of-the-diagnostic-logs"></a>C. Especificar la ubicación de los registros de diagnóstico  
 En el ejemplo siguiente se establece la ubicación de los registros de diagnóstico en la ruta de acceso de archivo especificada.  
  
```  
ALTER SERVER CONFIGURATION  
SET DIAGNOSTICS LOG PATH = 'C:\logs';  
```  
  
#### <a name="d-specifying-the-maximum-size-of-each-diagnostic-log"></a>D. Especificar el tamaño máximo de cada registro de diagnóstico  
 En el ejemplo siguiente se establece el tamaño máximo de cada registro de diagnóstico en 10 megabytes.  
  
```  
ALTER SERVER CONFIGURATION   
SET DIAGNOSTICS LOG MAX_SIZE = 10 MB;  
```  
  
###  <a name="Failover"></a>Establecer propiedades de clúster de conmutación por error  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 En el ejemplo siguiente se muestra la forma de establecer los valores de las propiedades de recurso de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
#### <a name="a-specifying-the-value-for-the-healthchecktimeout-property"></a>A. Especificar el valor de la propiedad HealthCheckTimeout  
 En el ejemplo siguiente se establece la opción `HealthCheckTimeout` en 15.000 milisegundos (15 segundos).  
  
```  
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
###  <a name="ChangeClusterContextExample"></a> B. Cambiar el contexto de clúster de una réplica de disponibilidad  
 En el ejemplo siguiente se cambia el contexto de clúster de HADR de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para especificar el clúster de destino de WSFC, `clus01`, el ejemplo especifica el nombre de objeto completo del clúster, `clus01.xyz.com`.  
  
```  
ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = 'clus01.xyz.com';  
```  
  
### <a name="setting-buffer-pool-extension-options"></a>Establecer las opciones de extensión del grupo de búferes  
  
####  <a name="BufferPoolExtension"></a> A. Establecer la opción de extensión del grupo de búferes  
  
**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 En el siguiente ejemplo se habilita la opción de extensión del grupo de búferes y se especifica un nombre de archivo y un tamaño.  
  
```  
ALTER SERVER CONFIGURATION   
SET BUFFER POOL EXTENSION ON  
    (FILENAME = 'F:\SSDCACHE\Example.BPE', SIZE = 50 GB);  
```  
  
#### <a name="b-modifying-buffer-pool-extension-parameters"></a>B. Modificar parámetros de extensión del grupo de búferes  
 En el ejemplo siguiente se modifica el tamaño de un archivo de extensión del grupo de búferes. La opción de extensión del grupo de búferes debe deshabilitarse antes de que se modifique alguno de los parámetros.  
  
```  
ALTER SERVER CONFIGURATION   
SET BUFFER POOL EXTENSION OFF;  
GO  
EXEC sp_configure 'max server memory (MB)', 12000;  
GO  
RECONFIGURE;  
GO  
ALTER SERVER CONFIGURATION  
SET BUFFER POOL EXTENSION ON  
    (FILENAME = 'F:\SSDCACHE\Example.BPE', SIZE = 60 GB);  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Soft-NUMA &#40; SQL Server &#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)   
 [Cambiar el contexto de clúster HADR de la instancia del servidor &#40; SQL Server &#41;](../../database-engine/availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md)   
 [Sys.DM_OS_SCHEDULERS &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)   
 [Sys.dm_os_memory_nodes &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md)   
 [Sys.dm_os_buffer_pool_extension_configuration &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql.md)   
 [Extensión del grupo de búferes](../../database-engine/configure-windows/buffer-pool-extension.md)  
  
  

