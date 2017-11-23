---
title: sp_addmergearticle (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_addmergearticle
- sp_addmergearticle_TSQL
helpviewer_keywords: sp_addmergearticle
ms.assetid: 0df654ea-24e2-4c61-a75a-ecaa7a140a6c
caps.latest.revision: "69"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd9d9ead2695338116dd3da6a60285756cb433c6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spaddmergearticle-transact-sql"></a>sp_addmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un artículo a una publicación de combinación existente. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addmergearticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @source_object = ] 'source_object'   
    [ , [ @type = ] 'type' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @column_tracking = ] 'column_tracking' ]   
    [ , [ @status = ] 'status' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @subset_filterclause = ] 'subset_filterclause' ]   
    [ , [ @article_resolver = ] 'article_resolver' ]   
    [ , [ @resolver_info = ] 'resolver_info' ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @verify_resolver_signature = ] verify_resolver_signature ]   
    [ , [ @destination_object = ] 'destination_object' ]   
    [ , [ @allow_interactive_resolver = ] 'allow_interactive_resolver' ]   
    [ , [ @fast_multicol_updateproc = ] 'fast_multicol_updateproc' ]   
    [ , [ @check_permissions = ] check_permissions ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @published_in_tran_pub = ] 'published_in_tran_pub' ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @logical_record_level_conflict_detection = ] 'logical_record_level_conflict_detection' ]  
    [ , [ @logical_record_level_conflict_resolution = ] 'logical_record_level_conflict_resolution' ]  
    [ , [ @partition_options = ] partition_options ]  
    [ , [ @processing_order = ] processing_order ]  
    [ , [ @subscriber_upload_options = ] subscriber_upload_options ]  
    [ , [ @identityrangemanagementoption = ] 'identityrangemanagementoption' ]  
    [ , [ @delete_tracking = ] delete_tracking ]  
    [ , [ @compensate_for_errors = ] 'compensate_for_errors' ]   
    [ , [ @stream_blob_columns = ] 'stream_blob_columns' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicación***'**  
 Es el nombre de la publicación que contiene el artículo. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@article=** ] **'***artículo***'**  
 Es el nombre del artículo. El nombre debe ser único en la publicación. *artículo* es **sysname**, no tiene ningún valor predeterminado. *artículo* deben estar en el equipo local que ejecuta [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y debe ajustarse a las reglas para identificadores.  
  
 [  **@source_object=** ] **'***source_object***'**  
 Es el objeto de base de datos que se va a publicar. *source_object* es **sysname**, no tiene ningún valor predeterminado. Para obtener más información acerca de los tipos de objetos que se pueden publicar mediante la replicación de mezcla, vea [publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 [  **@type=** ] **'***tipo***'**  
 Es el tipo de artículo. *tipo de* es **sysname**, su valor predeterminado es **tabla**, y puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**tabla** (valor predeterminado)|Tabla con esquema y datos. La replicación supervisa la tabla para determinar los datos que se van a replicar.|  
|**solo esquema Func**|Función con solo esquema.|  
|**vista indizada** **solo esquema**|Vista indizada con solo esquema.|  
|**solo el esquema de procedimiento**|Procedimiento almacenado con solo esquema.|  
|**solo el esquema de sinónimos**|Sinónimo con solo esquema.|  
|**solo el esquema de vista**|Vista con solo esquema.|  
  
 [  **@description=** ] **'***descripción***'**  
 Es una descripción del artículo. *descripción* es **nvarchar (255)**, su valor predeterminado es null.  
  
 [  **@column_tracking=** ] **'***column_tracking***'**  
 Es el valor del seguimiento de nivel de columna. *column_tracking* es **nvarchar (10)**, con un valor predeterminado es FALSE. **True**activa el seguimiento de columnas. **false** desactiva el seguimiento de columnas y deja la detección de conflictos a nivel de fila. Si la tabla ya está publicada en otras publicaciones de combinación, debe utilizar el mismo valor de seguimiento por columna que utilizan los artículos existentes basados en esta tabla. Este parámetro es específico solamente de los artículos de tabla.  
  
> [!NOTE]  
>  Si se utiliza el seguimiento por fila en la detección de conflictos (valor predeterminado), la tabla base puede incluir un máximo de 1024 columnas, pero en el artículo deben filtrarse las columnas de forma que se publique un máximo de 246 columnas. Si se utiliza el seguimiento por columna, la tabla base puede incluir 246 columnas como máximo.  
  
 [  **@status=** ] **'***estado***'**  
 Es el estado del artículo. *estado* es **nvarchar (10)**, su valor predeterminado es **unsynced**. Si **active**, se ejecuta la secuencia de comandos de procesamiento inicial para publicar la tabla. Si **unsynced**, se ejecuta la secuencia de comandos de procesamiento inicial para publicar la tabla en la próxima vez que se ejecuta el agente de instantáneas.  
  
 [  **@pre_creation_cmd=** ] **'***pre_creation_cmd***'**  
 Especifica qué debe hacer el sistema si la tabla existe en el suscriptor al aplicar la instantánea. *pre_creation_cmd* es **nvarchar (10)**, y puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Ninguno**|Si la tabla ya existe en el suscriptor, no se lleva a cabo ninguna acción.|  
|**eliminar**|Emite una eliminación basada en la cláusula WHERE del filtro de subconjunto.|  
|**quitar** (valor predeterminado)|Quita la tabla antes de volver a crearla. Debe admitir [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] los suscriptores.|  
|**truncar**|Trunca la tabla de destino.|  
  
 [  **@creation_script=** ] **'***creation_script***'**  
 Es la ruta de acceso y el nombre de un script opcional del esquema del artículo que se utiliza para crear el artículo en la base de datos de suscripciones. *creation_script* es **nvarchar (255)**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Los scripts de creación no se ejecutan en suscriptores de [!INCLUDE[ssEW](../../includes/ssew-md.md)].  
  
 [  **@schema_option=** ] *schema_option*  
 Es un mapa de bits de la opción de generación del esquema para el artículo dado. *schema_option* es **binary (8)**y puede ser el [| (OR bit a bit) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) producto de uno o varios de estos valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**0 x 00**|Deshabilita el scripting del agente de instantáneas y utiliza el script anterior a la creación de esquema proporcionado definido en *creation_script*.|  
|**0 x 01**|Genera la creación del objeto (CREATE TABLE, CREATE PROCEDURE, etc.). Este es el valor predeterminado en los artículos de procedimientos almacenados.|  
|**0 x 10**|Genera el índice clúster correspondiente. Aunque esta opción no esté establecida, se generarán índices relacionados con claves principales y restricciones UNIQUE si ya están definidos en una tabla publicada.|  
|**0 x 20**|Convierte los tipos de datos definidos por el usuario (UDT) en tipos de datos base en el suscriptor. Esta opción no se puede utilizar si existe una restricción CHECK o DEFAULT en una columna UDT, si una columna UDT forma parte de la clave principal o si una columna calculada hace referencia a una columna UDT.|  
|**0 x 40**|Genera los índices no clúster correspondientes. Aunque esta opción no esté establecida, se generarán índices relacionados con claves principales y restricciones UNIQUE si ya están definidos en una tabla publicada.|  
|**0 x 80**|Replica las restricciones PRIMARY KEY. También se replican los índices relacionados con la restricción, aunque opciones **0 x 10** y **0 x 40** no están habilitadas.|  
|**0 x 100**|Replica los desencadenadores de usuario en un artículo de tabla, si se han definido.|  
|**0 x 200**|Replica restricciones FOREIGN KEY. Si la tabla a la que se hace referencia no forma parte de una publicación, no se replica ninguna restricción FOREIGN KEY en una tabla publicada.|  
|**0 x 400**|Replica las restricciones CHECK.|  
|**0 x 800**|Replica los valores predeterminados.|  
|**0 x 1000**|Replica la intercalación de columna.|  
|**0 x 2000**|Replica las propiedades extendidas asociadas con el objeto de origen del artículo publicado.|  
|**0 x 4000**|Replica las restricciones UNIQUE. También se replican los índices relacionados con la restricción, aunque opciones **0 x 10** y **0 x 40** no están habilitadas.|  
|**0 x 8000**|Esta opción no es válida para publicadores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versiones posteriores.|  
|**0 x 10000**|Replica las restricciones CHECK como NOT FOR REPLICATION de manera que no se impongan durante la sincronización.|  
|**0 x 20000**|Replica las restricciones FOREIGN KEY como NOT FOR REPLICATION de manera que no se impongan durante la sincronización.|  
|**0 x 40000**|Replica grupos de archivos asociados con un índice o una tabla con particiones.|  
|**0 x 80000**|Replica el esquema de partición de una tabla con particiones.|  
|**0 x 100000**|Replica el esquema de partición de un índice con particiones.|  
|**0 x 200000**|Replica las estadísticas de tabla.|  
|**0 x 400000**|Replica los enlaces predeterminados.|  
|**0 x 800000**|Replica los enlaces de reglas.|  
|**0 x 1000000**|Replica el índice de texto completo.|  
|**0x2000000**|Colecciones de esquemas XML enlazado a **xml** columnas no se replican.|  
|**0x4000000**|Replica índices en **xml** columnas.|  
|**0 x 8000000**|Crea esquemas que no están ya presentes en el suscriptor.|  
|**0 x 10000000**|Convierte **xml** columnas a **ntext** en el suscriptor.|  
|**0 x 20000000**|Convierte los objetos grandes tipos de datos (**nvarchar (max)**, **varchar (max)**, y **varbinary (max)**) introducido en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para tipos de datos que se admiten en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
|**0 x 40000000**|Replica permisos.|  
|**0 x 80000000**|Intenta quitar dependencias a objetos que no forman parte de la publicación.|  
|**0 x 100000000**|Utilice esta opción para replicar el atributo FILESTREAM si se especifica en **varbinary (max)** columnas. No especifique esta opción si replica tablas en suscriptores de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Replicación de tablas que incluyen columnas FILESTREAM en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] no se admiten los suscriptores, sin tener en cuenta cómo se establece esta opción de esquema. Vea la opción relacionada **0 x 800000000**.|  
|**0x200000000**|Convierte los tipos de datos de fecha y hora (**fecha**, **tiempo**, **datetimeoffset**, y **datetime2**) introducido en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a los datos tipos que se admiten en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**0x400000000**|Replica la opción de compresión para los datos y los índices. Para obtener más información, consulte [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
|**0 x 800000000**|Establezca esta opción para almacenar los datos de FILESTREAM en su propio grupo de archivos en el suscriptor. Si no se establece esta opción, los datos de FILESTREAM se almacenan en el grupo de archivos predeterminado. La replicación no crea grupos de archivos; por tanto, si establece esta opción, debe crear el grupo de archivos antes de aplicar la instantánea en el suscriptor. Para obtener más información sobre cómo crear objetos antes de aplicar la instantánea, vea [ejecutar Scripts antes y después de aplicar la instantánea](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).<br /><br /> Vea la opción relacionada **0 x 100000000**.|  
|**0x1000000000**|Convierte tipos common language runtime (CLR) definido por el usuario (UDT) en **varbinary (max)** para que las columnas de tipo UDT se pueden replicar en suscriptores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x2000000000**|Convierte el **hierarchyid** tipo de datos que **varbinary (max)** para que las columnas de tipo **hierarchyid** se pueden replicar en suscriptores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obtener más información sobre cómo usar **hierarchyid** columnas en las tablas replicadas, vea [hierarchyid &#40; Transact-SQL &#41; ](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
|**0x4000000000**|Replica los índices filtrados de la tabla. Para obtener más información sobre los índices filtrados, vea [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).|  
|**0x8000000000**|Convierte el **geography** y **geometry** tipos de datos **varbinary (max)** para que las columnas de estos tipos se pueden replicar en suscriptores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x10000000000**|Replica índices en columnas de tipo **geography** y **geometría**.|  
  
 Si este valor es NULL, el sistema genera automáticamente una opción de esquema válida para el artículo. El **opciones de esquema predeterminadas** tabla en la sección Notas muestra el valor que se elige en función del tipo de artículo. Además, no todos los *schema_option* valores son válidos para todos los tipos de replicación y el tipo de artículo. El **opciones de esquema válidas** tabla en la sección Notas muestra las opciones que se pueden especificar para un tipo de artículo dado.  
  
> [!NOTE]  
>  El *schema_option* parámetro sólo afecta a las opciones de replicación para la instantánea inicial. Una vez que el esquema inicial se ha generado por el agente de instantáneas y aplicados en el suscriptor, la replicación de cambios de esquema de la publicación en el suscriptor se producen según las reglas de replicación de cambios de esquema y la *replicate_ddl* valor del parámetro especificado en [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Para más información, vea [Realizar cambios de esquema en bases de datos de publicaciones](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 [  **@subset_filterclause=** ] **'***subset_filterclause***'**  
 Es una cláusula WHERE que especifica el filtrado horizontal de un artículo de tabla sin la palabra WHERE. *subset_filterclause* es de **nvarchar (1000)**, su valor predeterminado es una cadena vacía.  
  
> [!IMPORTANT]  
>  Por motivos de rendimiento, se recomienda que no aplique funciones a nombres de columnas en las cláusulas de los filtros de fila con parámetros, como `LEFT([MyColumn]) = SUSER_SNAME()`. Si usa [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) en una cláusula de filtro e invalide el valor de HOST_NAME, es posible que deba convertir tipos de datos mediante [convertir](../../t-sql/functions/cast-and-convert-transact-sql.md). Para obtener más información sobre los procedimientos recomendados en este caso, vea la sección "Reemplazar el valor de HOST_NAME ()" en [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 [  **@article_resolver=** ] **'***article_resolver***'**  
 Es el solucionador basado en COM utilizado para solucionar conflictos en el artículo de tabla o en el ensamblado .NET Framework invocado para ejecutar lógica de negocios personalizada en el artículo de tabla. *article_resolver* es **varchar (255)**, su valor predeterminado es null. Los valores disponibles para este parámetro se enumeran en los solucionadores personalizados de [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Si el valor proporcionado no es uno de los solucionadores de [!INCLUDE[msCoName](../../includes/msconame-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el solucionador especificado en lugar del solucionador proporcionado por el sistema. Use **sp_enumcustomresolvers** para enumerar la lista de solucionadores personalizados disponibles. Para obtener más información, consulte [ejecutar lógica de negocios durante la sincronización mezcla](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md) y [Advanced Merge Replication Conflict Detection y la resolución de](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
 [  **@resolver_info=** ] **'***resolver_info***'**  
 Se utiliza para especificar información adicional necesaria para un solucionador personalizado. Algunos de los solucionadores de [!INCLUDE[msCoName](../../includes/msconame-md.md)] requieren que se proporcione una columna como entrada para el solucionador. *resolver_info* es **nvarchar (255)**, su valor predeterminado es null. Para obtener más información, consulte [Solucionadores basados en Microsoft COM](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
 [  **@source_owner=** ] **'***source_owner***'**  
 Es el nombre del propietario de la *source_object*. *source_owner* es **sysname**, su valor predeterminado es null. Si es NULL, se presupone que el usuario actual es el propietario.  
  
 [  **@destination_owner=** ] **'***destination_owner***'**  
 Es el propietario del objeto de la base de datos de suscripciones, si no es 'dbo'. *destination_owner* es **sysname**, su valor predeterminado es null. Si es NULL, se presupone que el propietario es 'dbo'.  
  
 [  **@vertical_partition=** ] **'***column_filter***'**  
 Habilita y deshabilita el filtrado de columnas en un artículo de tabla. *vertical_partition* es **nvarchar (5)** con un valor predeterminado es FALSE.  
  
 **false** indica que no hay ningún filtrado vertical y publica todas las columnas.  
  
 **True** borra todas las columnas excepto la clave principal declarada y las columnas ROWGUID. Las columnas se agregan mediante **sp_mergearticlecolumn**.  
  
 [  **@auto_identity_range=** ] **'***automatic_identity_range***'**  
 Habilita y deshabilita el control automático de rangos de identidad para este artículo en una publicación en el momento que se crea. *auto_identity_range* es **nvarchar (5)**, con un valor predeterminado es FALSE. **True** permite intervalo automático de identidad de control, mientras que **false** lo deshabilita.  
  
> [!NOTE]  
>  *auto_identity_range* ha quedado desusado y se proporciona por compatibilidad con versiones anteriores. Debe usar *identityrangemanagementoption* para especificar opciones de administración de intervalos de identidad. Para más información, vea [Replicar columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@pub_identity_range=** ] *pub_identity_range*  
 Controla el tamaño del intervalo de identidad asignado a un suscriptor con una suscripción de servidor cuando se utiliza la administración automática de intervalos de identidad. Este rango de identidad se reserva para que un suscriptor de republicación pueda realizar asignaciones a sus propios suscriptores. *pub_identity_range* es **bigint**, su valor predeterminado es null. Debe especificar este parámetro si *identityrangemanagementoption* es **automática** o si *auto_identity_range* es **true**.  
  
 [  **@identity_range=** ] *identity_range*  
 Controla el tamaño del rango de identidad asignado al publicador y al suscriptor cuando se utiliza el control automático de rangos de identidad. *identity_range* es **bigint**, su valor predeterminado es null. Debe especificar este parámetro si *identityrangemanagementoption* es **automática** o si *auto_identity_range* es **true**.  
  
> [!NOTE]  
>  *identity_range* controla el tamaño de intervalo de identidad en volver a publicar los suscriptores que utilicen versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [  **@threshold=** ] *umbral*  
 Valor de porcentaje que controla cuándo el Agente de mezcla asigna un nuevo intervalo de identidad. Cuando se especifica el porcentaje de valores en *umbral* es usa, el agente de mezcla crea un nuevo intervalo de identidad. *umbral* es **int**, su valor predeterminado es null. Debe especificar este parámetro si *identityrangemanagementoption* es **automática** o si *auto_identity_range* es **true**.  
  
 [  **@verify_resolver_signature=** ] *verify_resolver_signature*  
 Especifica si una firma digital se comprueba antes de utilizar un solucionador en la replicación de mezcla. *verify_resolver_signature* es **int**, su valor predeterminado es 1.  
  
 **0** especifica que no se comprobará la firma.  
  
 **1** especifica que se comprobará la firma para ver si proviene de un origen de confianza.  
  
 [  **@destination_object=** ] **'***destination_object***'**  
 Es el nombre del objeto creado en la base de datos de suscripciones. *destination_object* es **sysname**, su valor predeterminado es el contenido de  **@source_object** . Este parámetro se puede especificar únicamente si el artículo es de solo esquema, como procedimientos almacenados, vistas y UDF. Si el artículo especificado es un artículo de tabla, el valor de  *@source_object*  invalida el valor de *destination_object*.  
  
 [  **@allow_interactive_resolver=** ] **'***allow_interactive_resolver***'**  
 Habilita o deshabilita el uso del solucionador interactivo en un artículo. *allow_interactive_resolver* es **nvarchar (5)**, con un valor predeterminado es FALSE. **True** habilita el uso de la resolución interactiva en el artículo; **false** lo deshabilita.  
  
> [!NOTE]  
>  El Solucionador interactivo no se admite en suscriptores de [!INCLUDE[ssEW](../../includes/ssew-md.md)].  
  
 [  **@fast_multicol_updateproc=** ] **'***fast_multicol_updateproc***'**  
 Este parámetro ha quedado desusado y solo se mantiene por compatibilidad de scripts con versiones anteriores.  
  
 [  **@check_permissions=** ] *check_permissions*  
 Es un mapa de bits de los permisos de tabla que se comprueba cuando el Agente de mezcla aplica cambios en el publicador. Si la cuenta de inicio de sesión o usuario del publicador que utiliza el proceso de mezcla no dispone de los permisos de tabla correctos, los cambios no válidos se registran como conflictos. *check_permissions* es **int**y puede ser el [| (OR bit a bit) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) producto de uno o varios de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**0 x 00** (valor predeterminado)|Los permisos no se comprueban.|  
|**0 x 10**|Comprueba los permisos en el publicador antes de cargar las operaciones de inserción creadas en un suscriptor.|  
|**0 x 20**|Comprueba los permisos en el publicador antes de cargar las operaciones de actualización creadas en un suscriptor.|  
|**0 x 40**|Comprueba los permisos en el publicador antes de cargar las operaciones de eliminación creadas en un suscriptor.|  
  
 [  **@force_invalidate_snapshot=** ] *force_invalidate_snapshot*  
 Confirma que la acción realizada por este procedimiento almacenado puede invalidar una instantánea existente. *force_invalidate_snapshot* es un **bits**, con un valor predeterminado es 0.  
  
 **0** especifica que el agregar un artículo no invalidarán la instantánea no es válida. Si el procedimiento almacenado detecta que el cambio requiere una nueva instantánea, se producirá un error y no se realizarán cambios.  
  
 **1** especifica que agregar un artículo puede invalidar la instantánea no es válida y, si hay suscripciones existentes que requieran una nueva instantánea, concede permiso para marcar como obsoleta la instantánea existente y generado una nueva. *force_invalidate_snapshot* está establecido en **1** al agregar un artículo a una publicación con una instantánea existente.  
  
 [  **@published_in_tran_pub=** ] **'***published_in_tran_pub***'**  
 Indica que un artículo de una publicación de combinación también se publica en una publicación transaccional. *published_in_tran_pub* es **nvarchar (5)**, con un valor predeterminado es FALSE. **True** especifica que el artículo también se publica en una publicación transaccional.  
  
 [  **@force_reinit_subscription=** ] *force_reinit_subscription*  
 Confirma que la acción realizada por este procedimiento almacenado puede requerir que se reinicialicen las suscripciones existentes. *force_reinit_subscription* es un **bits**, con un valor predeterminado es 0.  
  
 **0** especifica que agregar un artículo no harán que se reinicialice la suscripción. Si el procedimiento almacenado detecta que el cambio requiere la reinicialización de las suscripciones existentes, se producirá un error y no se realizarán cambios.  
  
 **1** significa que los cambios en el artículo de mezcla hacen que se reinicialicen las suscripciones existentes y concede permiso para que se lleve a cabo la reinicialización. *force_reinit_subscription* está establecido en **1** cuando *subset_filterclause* especifica un filtro de fila con parámetros.  
  
 [  **@logical_record_level_conflict_detection=** ] **'***logical_record_level_conflict_detection***'**  
 Especifica el nivel de detección de conflictos para un artículo que es un miembro de un registro lógico. *logical_record_level_conflict_detection* es **nvarchar (5)**, con un valor predeterminado es FALSE.  
  
 **True** especifica que se detectará un conflicto si se realizan cambios en cualquier parte del registro lógico.  
  
 **false** especifica que se utiliza la detección de conflictos predeterminada tal y como especifica *column_tracking*. Para más información, vea [Agrupar cambios en filas relacionadas con registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
> [!NOTE]  
>  Dado que no admite registros lógicos [!INCLUDE[ssEW](../../includes/ssew-md.md)] suscriptores, debe especificar un valor de **false** para *logical_record_level_conflict_detection* para admitir estos suscriptores.  
  
 [  **@logical_record_level_conflict_resolution=** ] **'***logical_record_level_conflict_resolution***'**  
 Especifica el nivel de resolución de conflictos para un artículo que es un miembro de un registro lógico. *logical_record_level_conflict_resolution* es **nvarchar (5)**, con un valor predeterminado es FALSE.  
  
 **True** especifica que el todo registro lógico ganador sobrescribe el registro lógico perdedor.  
  
 **false** especifica que las filas ganadoras no se restringen al registro lógico. Si *logical_record_level_conflict_detection* es **true**, a continuación, *logical_record_level_conflict_resolution* también debe establecerse en **true**. Para más información, vea [Agrupar cambios en filas relacionadas con registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
> [!NOTE]  
>  Dado que no admite registros lógicos [!INCLUDE[ssEW](../../includes/ssew-md.md)] suscriptores, debe especificar un valor de **false** para *logical_record_level_conflict_resolution* para admitir estos suscriptores.  
  
 [  **@partition_options=** ] *partition_options*  
 Define el modo en el que se realiza la partición de los datos en el artículo, lo que permite optimizaciones de rendimiento cuando todas las filas pertenecen solamente a una partición o solamente a una suscripción. *partition_options* es **tinyint**, y puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**0** (valor predeterminado)|El filtrado para el artículo es estático o no produce un único subconjunto de datos para cada partición, es decir, una partición "superpuesta".|  
|**1**|Las particiones se superponen y las actualizaciones del lenguaje de manipulación de datos (DML) realizadas en el suscriptor no pueden cambiar la partición a la que pertenece la fila.|  
|**2**|El filtro para el artículo produce particiones no superpuestas, pero varios suscriptores pueden recibir la misma partición.|  
|**3**|El filtro para el artículo produce particiones no superpuestas que son exclusivas para cada suscripción.|  
  
> [!NOTE]  
>  Si la tabla de origen para un artículo ya está publicada en otra publicación, el valor de *partition_options* debe ser el mismo para ambos artículos.  
  
 [  **@processing_order=** ] *processing_order*  
 Indica el orden de procesamiento de los artículos en una publicación de mezcla. *processing_order* es **int**, con un valor predeterminado es 0. **0** especifica que el artículo está desordenado y cualquier otro valor representa el valor ordinal de la orden de procesamiento de este artículo. Los artículos se procesan en orden desde el valor menor al mayor. Si dos artículos tienen el mismo valor, lo determina el orden de procesamiento de orden del alias del artículo en el [sysmergearticles](../../relational-databases/system-tables/sysmergearticles-transact-sql.md) tabla del sistema. Para más información, vea [Especificar el orden de procesamiento de los artículos de mezcla](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
 [  **@subscriber_upload_options=** ] *subscriber_upload_options*  
 Define las restricciones en actualizaciones realizadas en el suscriptor con una suscripción de cliente. Para más información, vea [Optimizar el rendimiento de la replicación de mezcla con artículos de solo descarga](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md). *subscriber_upload_options* es **tinyint**, y puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**0** (valor predeterminado)|Sin restricciones. Los cambios realizados en el suscriptor se cargan en el publicador.|  
|**1**|Se permiten cambios en el suscriptor, pero éstos no se cargan en el publicador.|  
|**2**|No se permiten cambios en el suscriptor.|  
  
 Cambiar *subscriber_upload_options* requiere la suscripción para reinicializarla mediante una llamada a [sp_reinitmergepullsubscription &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md).  
  
> [!NOTE]  
>  Si la tabla de origen para un artículo ya está publicada en otra publicación, el valor de *subscriber_upload_options* debe ser el mismo para ambos artículos.  
  
 [  **@identityrangemanagementoption=** ] *identityrangemanagementoption*  
 Especifica cómo se controla el rango de identidad para el artículo. *valor de identityrangemanagementoption* es **nvarchar (10)**, y puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Ninguno**|Deshabilita la administración de intervalos de identidad.|  
|**Manual**|Marca la columna de identidad utilizando NOT FOR REPLICATION para habilitar la administración manual de intervalos de identidad.|  
|**Automático**|Especifica la administración automática de intervalos de identidad.|  
|NULL(Default)|Valor predeterminado es **ninguno**cuando el valor de *auto_identity_range* no **true**.|  
  
 Por compatibilidad con versiones anteriores, cuando el valor de *identityrangemanagementoption* es NULL, el valor de *auto_identity_range* está activada. Sin embargo, cuando el valor de *identityrangemanagementoption* no es NULL, entonces el valor de *auto_identity_range* se omite. Para más información, vea [Replicar columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@delete_tracking=** ] **'***delete_tracking***'**  
 Indica si las eliminaciones se replican. *delete_tracking* es **nvarchar (5)**, con un valor predeterminado es TRUE. **false** indica que no se replican las eliminaciones, y **true** indica que las eliminaciones se replican, que es el comportamiento habitual para la replicación de mezcla. Cuando *delete_tracking* está establecido en **false**, filas eliminadas en el suscriptor deben quitarse manualmente en el publicador y filas eliminadas en el publicador deben quitarse manualmente en el suscriptor.  
  
> [!IMPORTANT]  
>  Establecer *delete_tracking* a **false** da como resultado de no convergencia. Si la tabla de origen para un artículo ya está publicada en otra publicación, el valor de *delete_tracking* debe ser el mismo para ambos artículos.  
  
> [!NOTE]  
>  *delete_tracking* opciones no se pueden establecer usando el **Asistente para nueva publicación** o **propiedades de la publicación** cuadro de diálogo.  
  
 [  **@compensate_for_errors=** ] **'***compensate_for_errors***'**  
 Indica si se llevan a cabo acciones de compensación cuando se producen errores durante la sincronización. *compensate_for_errors*s **nvarchar (5)**, con un valor predeterminado es FALSE. Cuando se establece en **true**, cambios que no se puede aplicar en un suscriptor o publicador durante la sincronización siempre dar lugar a acciones de compensación para deshacer el cambio; sin embargo, uno configurado incorrectamente suscriptor que genera un error puede provocar cambios en otros suscriptores y publicadores que se deshagan. **false** deshabilita estas acciones de compensación; sin embargo, los errores siguen registrándose como compensaciones y las mezclas posteriores sigue intentando aplicar los cambios hasta que lo logre.  
  
> [!IMPORTANT]  
>  Aunque parezca que los datos de las filas afectadas no tengan convergencia, en cuanto trate los errores, se podrán aplicar los cambios y los datos convergerán. Si la tabla de origen para un artículo ya está publicada en otra publicación, el valor de *compensate_for_errors* debe ser el mismo para ambos artículos.  
  
 [  **@stream_blob_columns=** ] **'***stream_blob_columns***'**  
 Especifica que se utilice una optimización del flujo de datos al replicar columnas de objetos grandes binarios. *stream_blob_columns* es **nvarchar (5)**, con un valor predeterminado es FALSE. **True** significa que se intentará la optimización. *stream_blob_columns* se establece en true cuando FILESTREAM está habilitado. Esto permite que la replicación de datos FILESTREAM se realice de forma óptima y que se reduzca el uso de memoria. Para forzar que los artículos de tabla FILESTREAM no usen transmisión de datos blob, use **sp_changemergearticle** establecer *stream_blob_columns* en false.  
  
> [!IMPORTANT]  
>  Si se habilita esta optimización de la memoria, el rendimiento del Agente de mezcla podría verse afectado durante la sincronización. Esta opción solo se debe utilizar al replicar columnas que contienen megabytes de datos.  
  
> [!NOTE]  
>  Determinadas funciones de replicación de mezcla, como los registros lógicos, pueden impedir que la optimización de secuencia que se va a utilizar al replicar objetos binarios grandes incluso con *stream_blob_columns* establecido en **true**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addmergearticle** se utiliza en la replicación de mezcla.  
  
 Al publicar objetos, sus definiciones se copian en los suscriptores. Si va a publicar un objeto de base de datos que depende de uno o varios objetos, debe publicar todos los objetos a los que hace referencia. Por ejemplo, si publica una vista que depende de una tabla, también debe publicar la tabla.  
  
 Si especifica un valor de **3** para *partition_options*, puede haber solo una suscripción para cada partición de datos de ese artículo. Si se crea una segunda partición en la que el criterio de filtrado de la nueva suscripción se resuelve en la misma partición que la suscripción existente, se quitará la suscripción existente.  
  
 Al especificar un valor de 3 para *partition_options*, metadatos se limpian siempre que se ejecuta el agente de mezcla y la instantánea con particiones expira más rápidamente. Al utilizar esta opción, debe considerar la habilitación de la instantánea con particiones solicitada por el suscriptor. Para más información, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 Agregar un artículo con un filtro horizontal estático, usar *subset_filterclause*, a una publicación existente con artículos que tienen filtros con parámetros requiere que se reinicialicen las suscripciones.  
  
 Al especificar *processing_order*, se recomienda dejar espacios entre los valores de orden del artículo, lo que facilita establecer nuevos valores en el futuro. Por ejemplo, si tiene tres artículos: artículo1, artículo2 y artículo3, establezca *processing_order* en 10, 20 y 30, en lugar de 1, 2 y 3. Para más información, vea [Especificar el orden de procesamiento de los artículos de mezcla](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
## <a name="default-schema-option-table"></a>Tabla Opciones de esquema predeterminadas  
 Esta tabla describen el valor predeterminado establecido por el procedimiento almacenado si se especifica un valor NULL para *schema_option*, que depende del tipo de artículo.  
  
|Tipo de artículo|Valor de la opción de esquema|  
|------------------|-------------------------|  
|**solo esquema Func**|**0 x 01**|  
|**solo el esquema de vista indizada**|**0 x 01**|  
|**solo el esquema de procedimiento**|**0 x 01**|  
|**table**|**0x0C034FD1**  -  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y más adelante publicaciones compatibles con una instantánea en modo nativo.<br /><br /> **0x08034FF1**  -  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y más adelante publicaciones compatibles con una instantánea en modo de carácter.|  
|**solo el esquema de vista**|**0 x 01**|  
  
> [!NOTE]  
>  Si la publicación es compatible con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la opción de esquema predeterminado para **tabla** es **0x30034FF1**.  
  
## <a name="valid-schema-option-table"></a>Tabla Opciones de esquema válidas  
 La tabla siguiente describen los valores permitidos *schema_option* según el tipo de artículo.  
  
|Tipo de artículo|Valores de las opciones de esquema|  
|------------------|--------------------------|  
|**solo esquema Func**|**0 x 01** y **0 x 2000**|  
|**solo el esquema de vista indizada**|**0 x 01**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 1000000**, y **0 x 200000**|  
|**solo el esquema de procedimiento**|**0 x 01** y **0 x 2000**|  
|**table**|Todas las opciones.|  
|**solo el esquema de vista**|**0 x 01**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 1000000**, y **0 x 200000**|  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-addmergearticle-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol fijo de servidor **sysadmin** o al rol fijo de base de datos **db_owner** .  
  
## <a name="see-also"></a>Vea también  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Replicar columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
