---
title: sysmergepartitioninfoview (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sysmergepartitioninfoview
- sysmergepartitioninfoview_TSQL
dev_langs: TSQL
helpviewer_keywords: sysmergepartitioninfoview view
ms.assetid: 714e2935-1bc7-4901-aea2-64b1bbda03d6
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4a6c4dab4fd8f840d4c646bb1b9ec07a38da275a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysmergepartitioninfoview-transact-sql"></a>sysmergepartitioninfoview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **sysmergepartitioninfoview** vista expone información de partición para los artículos de tabla. Esta vista se almacena en el publicador de la base de datos de publicación y en el suscriptor de la base de datos de suscripciones.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|El nombre del artículo.|  
|**tipo**|**tinyint**|Indica el tipo de artículo, que puede ser uno de los siguientes:<br /><br /> **0x0A** = tabla.<br /><br /> **0 x 20** = solamente esquema de procedimiento.<br /><br /> **0 x 40** = view schema only o solo el esquema de vista indizada.<br /><br /> **0 x 80** = solamente esquema de función.|  
|**ObjID**|**int**|El identificador del objeto publicado.|  
|**sync_objid**|**int**|Id. de objeto de la vista que representa el conjunto de datos sincronizado.|  
|**view_type**|**tinyint**|Tipo de vista:<br /><br /> **0** = no es una vista; usar todo el objeto base.<br /><br /> **1** = vista permanente.<br /><br /> **2** = vista temporal.|  
|**artid**|**uniqueidentifier**|El número de identificación único del artículo indicado.|  
|**Descripción**|**nvarchar(255)**|Descripción breve del artículo.|  
|**pre_creation_command**|**tinyint**|La acción predeterminada que se realizará cuando el artículo se crea en la base de datos de suscripción:<br /><br /> **0** = none: si la tabla ya existe en el suscriptor, no se realiza ninguna acción.<br /><br /> **1** = drop: quita la tabla antes de volver a crearla.<br /><br /> **2** = delete: realiza una eliminación basada en la cláusula WHERE del filtro de subconjunto.<br /><br /> **3** = Truncate: igual que 2, pero elimina páginas en lugar de filas. Sin embargo, no precisa la cláusula WHERE.|  
|**pubid**|**uniqueidentifier**|Id. de la publicación a la que pertenece el artículo actual.|  
|**alias**|**int**|Alias asignado para la identificación del artículo.|  
|**column_tracking**|**int**|Indica si está implementado el seguimiento de columnas en el artículo.|  
|**status**|**tinyint**|Indica el estado del artículo, que puede ser uno de los siguientes:<br /><br /> **1** = Unsynced - el script de procesamiento inicial para publicar la tabla se ejecutará la próxima vez que se ejecuta el agente de instantáneas.<br /><br /> **2** = active - se ha ejecutado la secuencia de comandos de procesamiento inicial para publicar la tabla.|  
|**conflict_table**|**sysname**|Nombre de la tabla local que contiene los registros en conflicto del artículo actual. Esta tabla solo tiene fines informativos y su contenido puede ser modificado o eliminado con rutinas de resolución de conflictos personalizadas, o directamente por el administrador.|  
|**creation_script**|**nvarchar(255)**|Script de creación de este artículo.|  
|**conflict_script**|**nvarchar(255)**|Script de conflicto de este artículo.|  
|**article_resolver**|**nvarchar(255)**|El solucionador de conflictos de este artículo.|  
|**ins_conflict_proc**|**sysname**|El procedimiento utilizado para escribir información de conflictos en la tabla de conflictos.|  
|**insert_proc**|**sysname**|El procedimiento utilizado para insertar filas durante la sincronización.|  
|**update_proc**|**sysname**|El procedimiento utilizado para actualizar filas durante la sincronización.|  
|**select_proc**|**sysname**|El nombre de un procedimiento almacenado generado automáticamente que utiliza el Agente de mezcla para llevar a cabo el bloqueo y buscar columnas y filas de un artículo.|  
|**metadata_select_proc**|**sysname**|El nombre de un procedimiento almacenado generado automáticamente utilizado para obtener acceso a los metadatos de las tablas del sistema de replicación de mezcla.|  
|**delete_proc**|**sysname**|El procedimiento utilizado para eliminar filas durante la sincronización.|  
|**schema_option**|**binary (8)**|El mapa de bits de la opción de generación del esquema para el artículo dado. Para obtener información sobre admite *schema_option* valores, vea [sp_addmergearticle &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**destination_object**|**sysname**|Nombre de la tabla creada en el suscriptor.|  
|**destination_owner**|**sysname**|Nombre del propietario del objeto de destino.|  
|**resolver_clsid**|**nvarchar(50)**|Identificador del solucionador de conflictos personalizado. En un controlador de lógica empresarial, este valor es NULL.|  
|**subset_filterclause**|**nvarchar (1000)**|Cláusula de filtro de este artículo.|  
|**missing_col_count**|**int**|El número de columnas publicadas que faltan en el artículo.|  
|**missing_cols**|**varbinary(128)**|El mapa de bits que describe las columnas que faltan en el artículo.|  
|**excluded_cols**|**varbinary(128)**|El mapa de bits de las columnas excluidas del artículo.|  
|**excluded_col_count**|**int**|El número de columnas excluidas del artículo. |  
|**columnas**|**varbinary(128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deleted_cols**|**varbinary(128)**|El mapa de bits que describe las columnas eliminadas del artículo.|  
|**resolver_info**|**nvarchar(255)**|Almacenamiento para la información adicional requerida por los solucionadores de conflictos personalizados.|  
|**view_sel_proc**|**nvarchar(290)**|El nombre de un procedimiento almacenado que utiliza el Agente de mezcla para llenar por primera vez un artículo en una publicación filtrada dinámicamente y para enumerar las filas que han cambiado en cualquier publicación filtrada.|  
|**gen_cur**|**bigint**|Genera el número para los cambios locales de la tabla base de un artículo.|  
|**vertical_partition**|**int**|Especifica si está habilitado el filtrado de columnas en un artículo de una tabla. **0** indica que no hay ningún filtrado vertical y publica todas las columnas.|  
|**identity_support**|**int**|Especifica si se habilita el control automático del intervalo de identidad. **1** significa que está habilitado el control de intervalo de identidad, y **0** significa que no hay ninguna identidad de intervalo de soporte técnico.|  
|**before_image_objid**|**int**|Identificador de objeto de la tabla de seguimiento. La tabla de seguimiento contiene ciertos valores de columna de clave cuando se han habilitado optimizaciones de cambio de particiones para la publicación.|  
|**before_view_objid**|**int**|Id. del objeto de una tabla de vistas. La vista está en una tabla que mantiene un seguimiento de si una fila pertenecía a un suscriptor concreto antes de que se eliminara o actualizara. Se aplica solamente cuando se han habilitado optimizaciones de cambio de particiones en la publicación.|  
|**verify_resolver_signature**|**int**|Especifica si una firma digital se comprueba antes de utilizar un solucionador en la replicación de mezcla:<br /><br /> **0** = no se comprueba la firma.<br /><br /> **1** = firma se comprueba para ver si proviene de un origen de confianza.|  
|**allow_interactive_resolver**|**bit**|Especifica si está habilitado el uso del Solucionador interactivo en un artículo. **1** significa que se puede usar el solucionador interactivo en el artículo.|  
|**fast_multicol_updateproc**|**bit**|Especifica si se ha habilitado el Agente de mezcla para aplicar cambios a varias columnas de la misma fila en una instrucción UPDATE.<br /><br /> **0** = emite una actualización independiente para cada columna cambió.<br /><br /> **1** = emitido en la instrucción UPDATE que lleva a cabo actualizaciones en varias columnas en una sola instrucción.|  
|**check_permissions**|**int**|El mapa de bits de los permisos de nivel de tabla que se comprobarán cuando el agente de mezcla aplique cambios en el publicador. *check_permissions* puede tener uno de estos valores:<br /><br /> **0 x 00** = no se comprueban los permisos.<br /><br /> **0 x 10** = comprueba los permisos del publicador antes de que se realizan inserciones en el suscriptor se pueden cargar.<br /><br /> **0 x 20** = comprueba los permisos en el publicador antes de poder cargar los UPDATE creados en un suscriptor.<br /><br /> **0 x 40** = comprueba los permisos en el publicador antes de poder cargar los DELETE creados en un suscriptor.|  
|**maxversion_at_cleanup**|**int**|La generación máxima que se limpiará la próxima vez que se ejecute el Agente de mezcla.|  
|**processing_order**|**int**|Indica el orden de procesamiento de artículos en una publicación de combinación; un valor de **0** indica que el artículo está desordenado y artículos se procesan por orden, de menor a mayor valor. Si existen dos artículos que tienen el mismo valor, se procesan al mismo tiempo. Para más información, vea [Especificar el orden de procesamiento de los artículos de mezcla](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).|  
|**upload_options**|**tinyint**|Define si es posible realizar cambios en el suscriptor o cargarlos desde él. Puede se uno de los siguientes valores.<br /><br /> **0** = no hay restricciones respecto a las actualizaciones realizadas en el suscriptor; todos los cambios se cargan en el publicador.<br /><br /> **1** = se permiten realizar cambios en el suscriptor, pero no se cargan en el publicador.<br /><br /> **2** = no se permiten cambios en el suscriptor.|  
|**published_in_tran_pub**|**bit**|Indica que un artículo de una publicación de combinación también se publica en una publicación transaccional.<br /><br /> **0** = el artículo no está publicado en un artículo transaccional.<br /><br /> **1** = el artículo también se publica en un artículo transaccional.|  
|**ligero**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**procname_postfix**|**nchar(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**well_partitioned_lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**before_upd_view_objid**|**int**|El Id. de la vista de la tabla antes de las actualizaciones.|  
|**delete_tracking**|**bit**|Indica si las eliminaciones se replican.<br /><br /> **0** = no se replican las eliminaciones.<br /><br /> **1** = las eliminaciones se replican, que es el comportamiento predeterminado para la replicación de mezcla.<br /><br /> Cuando el valor de *delete_tracking* es **0**, filas eliminadas en el suscriptor deben quitarse manualmente en el publicador y filas eliminadas en el publicador deben quitarse manualmente en el suscriptor.<br /><br /> Nota: Un valor de **0** da como resultado de no convergencia.|  
|**compensate_for_errors**|**bit**|Indica si se llevan a cabo acciones de compensación cuando se producen errores durante la sincronización.<br /><br /> **0** = compensación se deshabilitan las acciones.<br /><br /> **1** = cambios que no se pueden aplicar en un suscriptor o publicador siempre conllevan acciones de compensación para deshacer estos cambios, que es el comportamiento predeterminado para la replicación de mezcla.<br /><br /> Nota: Un valor de **0** da como resultado de no convergencia.|  
|**pub_range**|**bigint**|Tamaño del intervalo de identidad del publicador.|  
|**intervalo**|**bigint**|Tamaño de los valores de identidad consecutivos que podrían asignarse a los suscriptores en un ajuste.|  
|**umbral**|**int**|Porcentaje de umbral del intervalo de identidad.|  
|**stream_blob_columns**|**bit**|Indica si se utiliza la optimización de transmisión para columnas de objetos binarios grandes. **1** significa que se intenta realizar la optimización.|  
|**preserve_rowguidcol**|**bit**|Indica si la replicación utiliza una columna rowguid existente. Un valor de **1** significa que se utiliza una columna ROWGUIDCOL existente. **0** significa que la replicación agregará la columna ROWGUIDCOL.|  
|**partition_view_id**|**int**|Identifica la vista que define a una partición del suscriptor.|  
|**repl_view_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**partition_deleted_view_rule**|**sysname**|La instrucción utilizada en un desencadenador de replicación de mezcla para recuperar el Id. de partición de cada fila eliminada o actualizada en función de sus valores de columna antiguos.|  
|**partition_inserted_view_rule**|**Sysname**|La instrucción utilizada en un desencadenador de replicación de mezcla para recuperar el Id. de partición de cada fila insertada o actualizada en función de sus valores de columna nuevos.|  
|**membership_eval_proc_name**|**sysname**|El nombre del procedimiento que se evalúa como el Id. de partición actual de filas de [MSmerge_contents &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/msmerge-contents-transact-sql.md).|  
|**column_list**|**sysname**|Una lista delimitada por comas de las columnas publicadas en un artículo.|  
|**column_list_blob**|**sysname**|Una lista delimitada por comas de las columnas publicadas en un artículo, incluidas las columnas de objetos binarios grandes.|  
|**expand_proc**|**sysname**|El nombre del procedimiento que vuelve a evaluar Id. de todas las filas secundarias de una fila principal recién insertada y de las filas principales que han experimentado un cambio en la partición o se haya eliminado la partición.|  
|**logical_record_parent_nickname**|**int**|El alias del primario de nivel superior de un artículo dado de un registro lógico.|  
|**logical_record_view**|**int**|Una vista que produce el rowguid del artículo primario de nivel superior correspondiente a cada rowguid secundario.|  
|**logical_record_deleted_view_rule**|**sysname**|Similar a **logical_record_view**, excepto en que muestra filas secundarias en la tabla "eliminada" en actualizarán y eliminar los desencadenadores.|  
|**logical_record_level_conflict_detection**|**bit**|Indica si los conflictos se deben detectar en el nivel de registro lógico o en el nivel de fila o de columna.<br /><br /> **0** = o columna de nivel de fila se utiliza la detección de conflictos.<br /><br /> **1** = lógico se utiliza la detección de conflictos de registro, donde un cambio en una fila en el publicador y el cambio en otro fila lógica mismo registro en el suscriptor se trata como un conflicto.<br /><br /> Cuando este valor es 1, solo se puede utilizar la resolución de conflictos de nivel de registro lógico.|  
|**logical_record_level_conflict_resolution**|**bit**|Indica si los conflictos se deben solucionar en el nivel de registro lógico o en el nivel de fila o de columna.<br /><br /> **0** = o columna de nivel de fila se utiliza la resolución.<br /><br /> **1** = en caso de conflicto, el registro lógico completo del ganador sobrescribe el registro lógico completo de la parte perdedora.<br /><br /> Se puede utilizar un valor de 1 tanto con la detección de nivel de registro lógico como con la detección de nivel de fila o de columna.|  
|**partition_options**|**tinyint**|Define el modo en el que se realiza la partición de los datos en el artículo, lo que permite optimizaciones de rendimiento cuando todas las filas pertenecen solamente a una partición o solamente a una suscripción. El *partition_options* puede ser uno de los siguientes valores.<br /><br /> **0** = el filtro del artículo es estático o no produce un único subconjunto de datos para cada partición, es decir, una partición "superpuesta".<br /><br /> **1** = las particiones se superponen y las actualizaciones DML realizadas en el suscriptor no pueden cambiar la partición a la que pertenece una fila.<br /><br /> **2** = el filtro del artículo produce particiones no superpuestas, pero varios suscriptores pueden recibir la misma partición.<br /><br /> **3** = el filtro del artículo produce particiones no superpuestas que son únicas para cada suscripción.|  
|**Nombre**|**sysname**|El nombre de una partición.|  
  
## <a name="see-also"></a>Vea también  
 [Administrar particiones para una publicación de mezcla con filtros con parámetros](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergepartition &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [sp_helpmergepartition &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md)  
  
  
