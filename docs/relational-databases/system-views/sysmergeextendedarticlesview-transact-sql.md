---
title: sysmergeextendedarticlesview (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergeextendedarticlesview
- sysmergeextendedarticlesview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeextendedarticlesview view
ms.assetid: bd5c8414-5292-41fd-80aa-b55a50ced7e2
author: stevestein
ms.author: sstein
ms.openlocfilehash: dd7e15e6e0a1a4097cbc79535ffec968f6776db4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910074"
---
# <a name="sysmergeextendedarticlesview-transact-sql"></a>sysmergeextendedarticlesview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **sysmergeextendedarticlesview** expone información del artículo de vista. Esta vista se almacena en el publicador de la base de datos de publicación y en el suscriptor de la base de datos de suscripciones.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|El nombre del artículo.|  
|**type**|**tinyint**|Indica el tipo de artículo, que puede ser uno de los siguientes:<br /><br /> **10** = tabla.<br /><br /> **32** = solamente esquema de procedimiento.<br /><br /> **64** = view schema only o solo el esquema de vista indizada.<br /><br /> **128** = solamente esquema de función.<br /><br /> **160** = solamente esquema de sinónimo.|  
|**objid**|**int**|Identificador del objeto de publicador.|  
|**sync_objid**|**int**|Identificador de la vista que representa el conjunto de datos sincronizado.|  
|**view_type**|**tinyint**|Tipo de vista:<br /><br /> **0** = no es una vista; usar todo el objeto base.<br /><br /> **1** = vista permanente.<br /><br /> **2** = vista temporal.|  
|**artid**|**uniqueidentifier**|El número de identificación único del artículo indicado.|  
|**description**|**nvarchar(255)**|Descripción breve del artículo.|  
|**pre_creation_command**|**tinyint**|La acción predeterminada que se realizará cuando se crea el artículo en la base de datos de suscripción:<br /><br /> **0** = none: si la tabla ya existe en el suscriptor, se realiza ninguna acción.<br /><br /> **1** = drop: quita la tabla antes de volver a crearla.<br /><br /> **2** = delete: realiza una eliminación basada en la cláusula WHERE del filtro de subconjunto.<br /><br /> **3** = Truncate: igual que 2, pero elimina páginas en lugar de filas. Sin embargo, no precisa la cláusula WHERE.|  
|**pubid**|**uniqueidentifier**|Id. de la publicación a la que pertenece el artículo actual.|  
|**alias**|**int**|Alias asignado para la identificación del artículo.|  
|**column_tracking**|**int**|Indica si se ha implementado el seguimiento de columnas en el artículo.|  
|**status**|**tinyint**|Indica el estado del artículo, que puede ser uno de los siguientes:<br /><br /> **1** = Unsynced - el script de procesamiento inicial para publicar la tabla se ejecutará la próxima vez que se ejecuta el agente de instantáneas.<br /><br /> **2** = active - se ha ejecutado el script de procesamiento inicial para publicar la tabla.<br /><br /> **5** = New_inactive - va a agregar.<br /><br /> **6** = New_active - va a agregar.|  
|**conflict_table**|**sysname**|Nombre de la tabla local que contiene los registros en conflicto del artículo actual. Esta tabla solo tiene fines informativos y su contenido puede ser modificado o eliminado con rutinas de resolución de conflictos personalizadas, o directamente por el administrador.|  
|**creation_script**|**nvarchar(255)**|Script de creación de este artículo.|  
|**conflict_script**|**nvarchar(255)**|Script de conflicto de este artículo.|  
|**article_resolver**|**nvarchar(255)**|Solucionador de conflictos personalizado en el nivel de filas de este artículo.|  
|**ins_conflict_proc**|**sysname**|El procedimiento utilizado para escribir conflictos en **conflict_table**.|  
|**insert_proc**|**sysname**|Procedimiento que utiliza el solucionador de conflictos predeterminado para insertar filas durante la sincronización.|  
|**update_proc**|**sysname**|Procedimiento que utiliza el solucionador de conflictos predeterminado para actualizar filas durante la sincronización.|  
|**select_proc**|**sysname**|Nombre de un procedimiento almacenado generado automáticamente que utiliza el Agente de mezcla para llevar a cabo el bloqueo y buscar columnas y filas de un artículo.|  
|**schema_option**|**binary (8)**|Para los valores admitidos de *schema_option*, consulte [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**destination_object**|**sysname**|Nombre de la tabla creada en el suscriptor.|  
|**resolver_clsid**|**nvarchar(50)**|Identificador del solucionador de conflictos personalizado.|  
|**subset_filterclause**|**nvarchar(1000)**|Cláusula de filtro de este artículo.|  
|**missing_col_count**|**int**|Número de columnas que faltan.|  
|**missing_cols**|**varbinary(128)**|Mapa de bits de las columnas que faltan.|  
|**columns**|**varbinary(128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**resolver_info**|**nvarchar(255)**|Almacenamiento para la información adicional que necesitan los solucionadores de conflictos personalizados.|  
|**view_sel_proc**|**nvarchar(290)**|Nombre de un procedimiento almacenado que utiliza el Agente de mezcla para llenar por primera vez un artículo en una publicación filtrada dinámicamente y para enumerar las filas que han cambiado en cualquier publicación filtrada.|  
|**gen_cur**|**int**|Número de generación para los cambios locales de la tabla base de un artículo.|  
|**excluded_cols**|**varbinary(128)**|Mapa de bits de las columnas excluidas del artículo cuando se envía al suscriptor.|  
|**excluded_col_count**|**int**|Número de columnas excluidas.|  
|**vertical_partition**|**int**|Especifica si está habilitado el filtrado de columnas en un artículo de una tabla. **0** indica que no hay ningún filtrado vertical y publica todas las columnas.|  
|**identity_support**|**int**|Especifica si se habilita el control automático del intervalo de identidad. **1** significa que está habilitado el control de intervalo de identidad, y **0** significa que no hay ninguna identidad de intervalo de soporte técnico.|  
|**destination_owner**|**sysname**|Nombre del propietario del objeto de destino.|  
|**before_image_objid**|**int**|Identificador de objeto de la tabla de seguimiento. Esta contiene algunos valores de columna de clave cuando una publicación se configura para habilitar las optimizaciones de los cambios de partición.|  
|**before_view_objid**|**int**|Id. del objeto de una tabla de vistas. La vista está en una tabla que mantiene un seguimiento de si una fila pertenecía a un suscriptor concreto antes de que se eliminara o actualizara. Se aplica solo cuando se crea una publicación con *@keep_partition_changes*  =  **true**.|  
|**verify_resolver_signature**|**int**|Especifica si una firma digital se comprueba antes de utilizar un solucionador en la replicación de mezcla:<br /><br /> **0** = no se comprueba la firma.<br /><br /> **1** = firma se comprueba para ver si proviene de un origen de confianza.|  
|**allow_interactive_resolver**|**bit**|Especifica si está habilitado el uso del Solucionador interactivo en un artículo. **1** especifica que se utiliza el solucionador interactivo en el artículo.|  
|**fast_multicol_updateproc**|**bit**|Especifica si se ha habilitado el Agente de mezcla para aplicar cambios a varias columnas de la misma fila en una instrucción UPDATE.<br /><br /> **0** = problemas cambiada una actualización independiente para cada columna.<br /><br /> **1** = emitido en la instrucción UPDATE que lleva a cabo actualizaciones en varias columnas en una sola instrucción.|  
|**check_permissions**|**int**|El mapa de bits de los permisos de nivel de tabla que se comprobarán cuando el agente de mezcla aplique cambios en el publicador. *check_permissions* puede tener uno de estos valores:<br /><br /> **0 x 00** = no se comprueban los permisos.<br /><br /> **0 x 10** = comprueba los permisos en el publicador antes de poder cargar los INSERT creado en un suscriptor.<br /><br /> **0 x 20** = comprueba los permisos en el publicador antes de poder cargar los UPDATE creados en un suscriptor.<br /><br /> **0 x 40** = comprueba los permisos en el publicador antes de poder cargar los DELETE creados en un suscriptor.|  
|**maxversion_at_cleanup**|**int**|El valor más alto de generación para el cual se limpian los metadatos.|  
|**processing_order**|**int**|Indica el orden de procesamiento de artículos en una publicación de combinación; el valor **0** indica que el artículo está desordenado y artículos se procesan en orden de menor a mayor valor. Si existen dos artículos que tienen el mismo valor, se procesan al mismo tiempo. Para más información, vea [Specify merge replication properties](../../relational-databases/replication/merge/specify-merge-replication-properties.md) (Especificación de propiedades de replicación de mezcla).|  
|**published_in_tran_pub**|**bit**|Indica que un artículo de una publicación de combinación también se publica en una publicación transaccional.<br /><br /> **0** = artículo no está publicado en un artículo transaccional.<br /><br /> **1** = artículo también está publicado en un artículo transaccional.|  
|**upload_options**|**tinyiny**|Define si es posible realizar cambios en el suscriptor o cargarlos desde él. Puede se uno de los siguientes valores.<br /><br /> **0** = no hay ninguna restricción en las actualizaciones realizadas en el suscriptor; todos los cambios se cargan en el publicador.<br /><br /> **1** = se permiten realizar cambios en el suscriptor, pero no se cargan en el publicador.<br /><br /> **2** = no se permiten cambios en el suscriptor.|  
|**ligero**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**delete_proc**|**sysname**|Procedimiento que utiliza el solucionador de conflictos predeterminado para eliminar filas durante la sincronización.|  
|**before_upd_view_objid**|**int**|Id. de la vista de una tabla antes de las actualizaciones.|  
|**delete_tracking**|**bit**|Indica si las eliminaciones se replican.<br /><br /> **0** = no se replican las eliminaciones.<br /><br /> **1** = las eliminaciones se replican, que es el comportamiento predeterminado para la replicación de mezcla.<br /><br /> Cuando el valor de *delete_tracking* es **0**, las filas eliminadas en el suscriptor deben quitarse manualmente en el publicador y las filas eliminadas en el publicador deben quitarse manualmente en el suscriptor.<br /><br /> Nota: Un valor de **0** da como resultado una falta de convergencia.|  
|**compensate_for_errors**|**bit**|Indica si se llevan a cabo acciones de compensación cuando se producen errores durante la sincronización.<br /><br /> **0** = compensación se deshabilitan las acciones.<br /><br /> **1** = los cambios que no se puede aplicar a acciones de compensación para deshacer estos cambios, que es el comportamiento predeterminado para la replicación de mezcla en el suscriptor o publicador siempre.<br /><br /> Nota: Un valor de **0** da como resultado una falta de convergencia.|  
|**pub_range**|**bigint**|Tamaño del intervalo de identidad del publicador.|  
|**intervalo**|**bigint**|Tamaño de los valores de identidad consecutivos que podrían asignarse a los suscriptores en un ajuste.|  
|**threshold**|**int**|Porcentaje de umbral del intervalo de identidad.|  
|**metadata_select_proc**|**sysname**|Nombre del procedimiento almacenado, y generado automáticamente, utilizado para obtener acceso a los metadatos en las tablas del sistema de replicación de mezcla.|  
|**stream_blob_columns**|**bit**|Especifica si se utiliza una optimización del flujo de datos al replicar columnas de objetos grandes binarios. **1** significa que se intentará la optimización.|  
|**preserve_rowguidcol**|**bit**|Indica si la replicación utiliza una columna rowguid existente. Un valor de **1** significa que se utiliza una columna ROWGUIDCOL existente. **0** significa que la replicación agregará la columna ROWGUIDCOL.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [sysmergearticles &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergearticles-transact-sql.md)  
  
  
