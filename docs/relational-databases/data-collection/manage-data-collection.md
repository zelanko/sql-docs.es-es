---
title: Administración de la recopilación de datos | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
keywords:
- Recopilación de datos
helpviewer_keywords:
- data collection [SQL Server]
- data collector [SQL Server], Transact-SQL
- data collector [SQL Server], SQL Server Management Studio
ms.assetid: bc137daa-9f37-4c01-9766-8b7350c75af8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 53869016813d3950f35fa5b926cbba295df63237
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68133609"
---
# <a name="manage-data-collection"></a>Administrar la recopilación de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 Use procedimientos almacenados y funciones de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] para administrar distintos aspectos de la recopilación de datos, como habilitar o deshabilitar la recopilación de datos, cambiar la configuración de un conjunto de recopilación o ver los datos en el almacén de administración de datos.  
  
## <a name="manage-data-collection-using-ssms"></a>Administrar la recopilación de datos con SSMS  
 Realice las siguientes tareas relacionadas con el recopilador de datos usando Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
-   [Configurar el almacén de administración de datos &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
-   [Configurar las propiedades de un recopilador de datos](../../relational-databases/data-collection/configure-properties-of-a-data-collector.md)  
  
-   [Habilitar o deshabilitar la recopilación de datos](../../relational-databases/data-collection/enable-or-disable-data-collection.md)  
  
-   [Iniciar o detener un conjunto de recopilación](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
-   [Usar SQL Server Profiler para crear un conjunto de recopilación de Seguimiento de SQL &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/use-sql-server-profiler-to-create-a-sql-trace-collection-set.md)  
  
-   [Ver los registros del conjunto de recopilación &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-collection-set-logs-sql-server-management-studio.md)  
  
-   [Ver o cambiar las programaciones del conjunto de recopilación &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-or-change-collection-set-schedules-sql-server-management-studio.md)  
  
-   [Ver un informe de conjunto de recopilación &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
## <a name="manage-data-collection-using-transact-sql"></a>Administrar la recopilación de datos con Transact-SQL  
 El recopilador de datos proporciona una recopilación extensa de procedimientos almacenados que puede usar para realizar cualquier tarea relacionada con el recopilador de datos. Por ejemplo, mediante el uso de [!INCLUDE[tsql](../../includes/tsql-md.md)]puede realizar las siguientes tareas:  
  
-   [Configurar parámetros para la recopilación de datos &#40;Transact-SQL&#41;](../../relational-databases/data-collection/configure-data-collection-parameters-transact-sql.md)  
  
-   [Habilitar o deshabilitar la recopilación de datos](../../relational-databases/data-collection/enable-or-disable-data-collection.md)  
  
-   [Iniciar o detener un conjunto de recopilación](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
-   [Crear un conjunto de recopilación personalizado que use el tipo de recopilador de consultas T-SQL genérico &#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)  
  
-   [Agregar un elemento de recopilación a un conjunto de recopilación &#40;Transact-SQL&#41;](../../relational-databases/data-collection/add-a-collection-item-to-a-collection-set-transact-sql.md)  
  
 Además, existen funciones y vistas que puede usar para obtener datos de configuración para las bases de datos de msdb y del almacén de administración de datos, datos de registro de ejecución y datos que se almacenan en el almacén de administración de datos.  
  
 Puede usar los procedimientos almacenados, las funciones y las vistas que se proporcionan para crear sus propios escenarios de recopilación de datos de un extremo a otro.  
  
>**IMPORTANTE:** A diferencia de los procedimientos almacenados normales, los procedimientos almacenados del recopilador usan parámetros con establecimiento estricto de tipos y no admiten la conversión automática de tipos de datos. Si no se llama a estos parámetros con los tipos de datos de parámetros de entrada correctos, según se especifica en la descripción del argumento, el procedimiento almacenado devuelve un error.  
  
 Use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para crear y ejecutar los ejemplos de código que se proporcionan. Para obtener más información, vea [Explorador de objetos](../../ssms/object/object-explorer.md). Como alternativa, puede crear la consulta en cualquier editor y guardarla en un archivo de texto con la extensión de nombre de archivo .sql. Puede ejecutar la consulta desde el símbolo del sistema de Windows mediante la utilidad **sqlcmd** . Para obtener más información, vea [Usar la utilidad sqlcmd](../../relational-databases/scripting/sqlcmd-use-the-utility.md).  
  
### <a name="stored-procedures-and-views"></a>Procedimientos almacenados y vistas  
 **Trabajar con el recopilador de datos**  
  
 La tabla siguiente describe los procedimientos almacenados que puede usar para trabajar con el recopilador de datos.  
  
|Nombre del procedimiento|Descripción|  
|--------------------|-----------------|  
|[sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)|Habilita el recopilador de datos.|  
|[sp_syscollector_disable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)|Deshabilita el recopilador de datos.|  
  
 **Trabajar con conjuntos de recopilación**  
  
 La tabla siguiente describe los procedimientos almacenados que puede usar para trabajar con conjuntos de recopilación.  
  
|Nombre del procedimiento|Descripción|  
|--------------------|-----------------|  
|[sp_syscollector_run_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md)|Ejecuta una conjunto de recopilación a petición.|  
|[sp_syscollector_start_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql.md)|Inicia un conjunto de recopilación.|  
|[sp_syscollector_stop_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md)|Detiene un conjunto de recopilación.|  
|[sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)|Crea un conjunto de recopilación.|  
|[sp_syscollector_delete_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-set-transact-sql.md)|Elimina un conjunto de recopilación.|  
|[sp_syscollector_update_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-set-transact-sql.md)|Cambia la configuración de un conjunto de recopilación.|  
|[sp_syscollector_upload_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-upload-collection-set-transact-sql.md)|Carga los datos del conjunto de recopilación en el almacén de administración de datos. Se trata, de hecho, de una carga a petición.|  
  
 **Trabajar con elementos de recopilación**  
  
 La tabla siguiente describe los procedimientos almacenados que puede usar para trabajar con elementos de recopilación.  
  
|Nombre del procedimiento|Descripción|  
|--------------------|-----------------|  
|[sp_syscollector_create_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)|Crea un elemento de recopilación.|  
|[sp_syscollector_delete_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)|Elimina un elemento de recopilación.|  
|[sp_syscollector_update_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)|Actualiza un elemento de recopilación.|  
  
 **Trabajar con tipos de recopilador**  
  
 La tabla siguiente describe los procedimientos almacenados que puede usar para trabajar con tipos de recopilador.  
  
|Nombre del procedimiento|Descripción|  
|--------------------|-----------------|  
|[sp_syscollector_create_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collector-type-transact-sql.md)|Crea un tipo de recopilador.|  
|[sp_syscollector_update_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collector-type-transact-sql.md)|Actualiza un tipo de recopilador.|  
|[sp_syscollector_delete_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collector-type-transact-sql.md)|Elimina un tipo de recopilador.|  
  
 **Obtener información de configuración**  
  
 La tabla siguiente describe las vistas que puede usar para obtener información de configuración y datos de registro de ejecución.  
  
|Nombre de la vista|Descripción|  
|---------------|-----------------|  
|[syscollector_config_store &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)|Obtiene la configuración del recopilador de datos.|  
|[syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)|Obtenga información del elemento de recopilación.|  
|[syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)|Obtenga información del conjunto de recopilación.|  
|[syscollector_collector_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)|Obtenga información de tipo de recopilador.|  
|[syscollector_execution_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-transact-sql.md)|Obtenga información sobre el conjunto de recopilación y la ejecución del paquete.|  
|[syscollector_execution_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)|Obtenga información sobre la ejecución de la tarea.|  
|[syscollector_execution_log_full &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql.md)|Obtenga información cuando el registro de ejecución está lleno.|  
  
 **Configurar el acceso al almacén de administración de datos**  
  
 La tabla siguiente describe los procedimientos almacenados que puede usar para configurar el acceso al almacén de administración de datos.  
  
|Nombre del procedimiento|Descripción|  
|--------------------|-----------------|  
|[sp_syscollector_set_warehouse_database_name &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)|Especifica el nombre de la base de datos definido en la cadena de conexión para el almacén de administración de datos.|  
|[sp_syscollector_set_warehouse_instance_name &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)|Especifique la instancia definida en la cadena de conexión para el almacén de administración de datos.|  
  
 **Configurar el acceso al almacén de datos de administración**  
  
 La tabla siguiente describe los procedimientos almacenados que puede usar para trabajar con la configuración del almacén de administración de datos.  
  
|Nombre del procedimiento|Descripción|  
|--------------------|-----------------|  
|[core.sp_create_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-create-snapshot-transact-sql.md)|Crea una instantánea de recopilación en el almacén de administración de datos.|  
|[core.sp_update_data_source &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-update-data-source-transact-sql.md)|Actualiza el origen de datos para la recopilación de datos.|  
|[core.sp_add_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-add-collector-type-transact-sql.md)|Agrega un tipo de recopilador al almacén de administración de datos.|  
|[core.sp_remove_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-remove-collector-type-transact-sql.md)|Quita un tipo de recopilador del almacén de administración de datos.|  
|[core.sp_purge_data &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-purge-data-transact-sql.md)|Elimina los datos del almacén de administración de datos.|  
  
 **Trabajar con paquetes de carga**  
  
 La tabla siguiente describe los procedimientos almacenados que puede usar para trabajar con paquetes de carga.  
  
|Nombre del procedimiento|Descripción|  
|--------------------|-----------------|  
|[sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)|Configura el número de intentos de carga de datos.|  
|[sp_syscollector_set_cache_directory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)|Especifica el almacenamiento temporal para los datos entre los intentos de carga.|  
  
 **Trabajar con el registro de ejecución de recopilación de datos**  
  
 La tabla siguiente describe los procedimientos almacenados que puede usar para trabajar con el registro de ejecución de recopilación de datos.  
  
|Nombre del procedimiento|Descripción|  
|--------------------|-----------------|  
|[sp_syscollector_delete_execution_log_tree &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-execution-log-tree-transact-sql.md)|Elimina entradas del conjunto de recopilación del registro de ejecución.|  
  
### <a name="functions"></a>Functions  
 La tabla siguiente describe las funciones que puede usar para obtener información de seguimiento y ejecución.  
  
|Nombre de función|Descripción|  
|-------------------|-----------------|  
|[fn_syscollector_get_execution_details &#40;Transact-SQL&#41;](../../relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql.md)|Obtenga datos del registro de ejecución de [!INCLUDE[ssIS](../../includes/ssis-md.md)] para un paquete concreto.|  
|[fn_syscollector_get_execution_stats &#40;Transact-SQL&#41;](../../relational-databases/system-functions/fn-syscollector-get-execution-stats-transact-sql.md)|Obtenga las estadísticas de ejecución para un paquete o un conjunto de recopilación. Esta información incluye errores que están registrados.|  
|[snapshots.fn_trace_getdata &#40;Transact-SQL&#41;](../../relational-databases/system-functions/snapshots-fn-trace-getdata-transact-sql.md)|Obtenga los eventos que se registran cuando se usa el tipo de recopilador de Seguimiento de SQL genérico para recopilar datos.|  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar un procedimiento almacenado](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)   
 [Usar SQL Server Management Studio](https://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)  
  
  
