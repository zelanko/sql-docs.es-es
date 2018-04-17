---
title: sp_addarticle (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_addarticle
- sp_addarticle_TSQL
helpviewer_keywords:
- sp_addarticle
ms.assetid: 0483a157-e403-4fdb-b943-23c1b487bef0
caps.latest.revision: 108
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bc5ed5d56541436e80eeafdccb1b1cdfe3ec6c9c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spaddarticle-transact-sql"></a>sp_addarticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un artículo y lo agrega a una publicación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addarticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
    [ , [ @source_table = ] 'source_table' ]  
    [ , [ @destination_table = ] 'destination_table' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @type = ] 'type' ]   
    [ , [ @filter = ] 'filter' ]   
    [ , [ @sync_object= ] 'sync_object' ]   
        [ , [ @ins_cmd = ] 'ins_cmd' ]   
    [ , [ @del_cmd = ] 'del_cmd' ]   
        [ , [ @upd_cmd = ] 'upd_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @filter_clause = ] 'filter_clause' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @status = ] status ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @sync_object_owner = ] 'sync_object_owner' ]   
    [ , [ @filter_owner = ] 'filter_owner' ]   
    [ , [ @source_object = ] 'source_object' ]   
    [ , [ @artid = ] article_ID  OUTPUT ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @use_default_datatypes = ] use_default_datatypes  
    [ , [ @identityrangemanagementoption = ] identityrangemanagementoption ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @fire_triggers_on_snapshot = ] 'fire_triggers_on_snapshot' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicación***'**  
 Es el nombre de la publicación que contiene el artículo. El nombre debe ser único en la base de datos. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@article =** ] **'***artículo***'**  
 Es el nombre del artículo. El nombre debe ser único en la publicación. *artículo* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@source_table =** ] **'***source_table***'**  
 Este parámetro está en desuso; usar *source_object* en su lugar.  
  
 *Este parámetro no se admite en publicadores de Oracle.*  
  
 [  **@destination_table =** ] **'***destination_table***'**  
 Es el nombre de la tabla de destino (suscripción), si es diferente de *source_table*o el procedimiento almacenado. *destination_table* es **sysname**, su valor predeterminado es null, lo que significa que *source_table* es igual a *destination_table **.*  
  
 [  **@vertical_partition =** ] **'***vertical_partition***'**  
 Habilita y deshabilita el filtrado de columnas en un artículo de tabla. *vertical_partition* es **nchar(5)**, con un valor predeterminado es FALSE.  
  
 **false** indica que no hay ningún filtrado vertical y publica todas las columnas.  
  
 **True** borra todas las columnas excepto la clave principal declarada, las columnas que aceptan valores NULL no tiene ningún valor predeterminado y columnas de clave única. Las columnas se agregan con [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md).  
  
 [  **@type =** ] **'***tipo***'**  
 Es el tipo de artículo. *tipo de* es **sysname**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**solo esquema agregado**|Función de agregado con solo esquema.|  
|**solo esquema Func**|Función con solo esquema.|  
|**logbased de vista indizada**|Artículo de vista indizada basado en registro. No es compatible con publicadores de Oracle. En este tipo de artículo, no es necesario que la tabla base se publique por separado.|  
|**vista indizada logbased manualboth**|Artículo de vista indizada basado en registro con filtro manual y vista manual. Esta opción requiere que especifique los *sync_object* y *filtro* parámetros. En este tipo de artículo, no es necesario que la tabla base se publique por separado. No es compatible con publicadores de Oracle.|  
|**vista indizada logbased manualfilter**|Artículo de vista indizada basado en registro con filtro manual. Esta opción requiere que especifique los *sync_object* y *filtro* parámetros. En este tipo de artículo, no es necesario que la tabla base se publique por separado. No es compatible con publicadores de Oracle.|  
|**vista indizada logbased manualview**|Artículo de vista indizada basado en registro con vista manual. Esta opción requiere que se especifique la *sync_object* parámetro. En este tipo de artículo, no es necesario que la tabla base se publique por separado. No es compatible con publicadores de Oracle.|  
|**solo el esquema de vista indizada**|Vista indizada con solo esquema. En este tipo de artículo también debe publicarse la tabla base.|  
|**logbased** (valor predeterminado)|Artículo basado en registro.|  
|**logbased manualboth**|Artículo basado en registro con filtro manual y vista manual. Esta opción requiere que especifique los *sync_object* y *filtro* parámetros. No es compatible con publicadores de Oracle.|  
|**logbased manualfilter**|Artículo basado en registro con filtro manual. Esta opción requiere que especifique los *sync_object* y *filtro* parámetros. No es compatible con publicadores de Oracle.|  
|**logbased manualview**|Artículo basado en registro con vista manual. Esta opción requiere que se especifique la *sync_object* parámetro. No es compatible con publicadores de Oracle.|  
|**proc exec**|Replica la ejecución del procedimiento almacenado a todos los suscriptores del artículo. No es compatible con publicadores de Oracle. Se recomienda que utilice la opción **serializable proc exec** en lugar de **proc exec**. Para obtener más información, vea la sección "Tipos de almacena artículos de procedimientos ejecución" en [Publishing Stored Procedure Execution en la replicación transaccional](../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md). No disponible cuando la captura de datos modificados está habilitada.|  
|**solo el esquema de procedimiento**|Procedimiento con solo esquema. No es compatible con publicadores de Oracle.|  
|**serializable proc exec**|Replica la ejecución del procedimiento almacenado solo si éste se ejecuta dentro del contexto de una transacción serializable. No es compatible con publicadores de Oracle.<br /><br /> El procedimiento también se debe ejecutar dentro de una transacción explícita para la ejecución del procedimiento se repliquen.|  
|**solo el esquema de vista**|Vista con solo esquema. No es compatible con publicadores de Oracle. Si se utiliza esta opción, también debe publicarse la tabla base.|  
  
 [  **@filter =** ] **'***filtro***'**  
 Es el procedimiento almacenado (creado con FOR REPLICATION) que se usa para filtrar la tabla horizontalmente. *filtro* es **nvarchar (386)**, su valor predeterminado es null. [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) y [sp_articlefilter](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) se deben ejecutar manualmente para crear la vista y procedimiento almacenado de filtro. Si no es NULL, el procedimiento de filtro no se crea (se presupone que el procedimiento almacenado se crea manualmente).  
  
 [  **@sync_object =** ] **'***sync_object***'**  
 Es el nombre de la tabla o vista utilizada para generar el archivo de datos usado para representar la instantánea de este artículo. *sync_object* es **nvarchar (386)**, su valor predeterminado es null. Si es NULL, [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) se llama para crear automáticamente la vista utilizada para generar el archivo de salida. Esto se produce después de agregar las columnas con [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md). Si no es NULL, no se crea la vista (se presupone que la vista se crea manualmente).  
  
 [  **@ins_cmd =** ] **'***ins_cmd***'**  
 Es el comando de replicación utilizado al replicar inserciones para este artículo. *ins_cmd* es **nvarchar (255)**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**NONE**|No se realiza ninguna acción.|  
|**Sp_MSins_ de llamada**<br /> ***tabla*** (valor predeterminado)<br /><br /> -O bien-<br /><br /> **Llamar a custom_stored_procedure_name**|Llama a un procedimiento almacenado que se ejecutará en el suscriptor. Para utilizar este método de replicación, utilice *schema_option* para especificar la creación automática del procedimiento almacenado o crear el procedimiento almacenado especificado en la base de datos de destino de cada suscriptor del artículo. *custom_stored_procedure* es el nombre de un procedimiento almacenado creado por el usuario. **sp_MSins_ * tabla*** contiene el nombre de la tabla de destino en lugar de la *_table* parte del parámetro. Cuando *destination_owner* se especifica, se antepone al nombre de la tabla de destino. Por ejemplo, para la **ProductCategory** tabla pertenece a la **producción** esquema en el suscriptor, el parámetro sería `CALL sp_MSins_ProductionProductCategory`. Para un artículo en una topología de replicación punto a punto, *_table* se anexa con un valor GUID. Especificar *custom_stored_procedure* no se admite para suscriptores de actualización.|  
|**SQL** o NULL|Replica una instrucción INSERT. La instrucción INSERT recibe valores para todas las columnas publicadas en el artículo. Este comando se replica con las inserciones:<br /><br /> `INSERT INTO <table name> VALUES (c1value, c2value, c3value, ..., cnvalue)`|  
  
 Para obtener más información, vea [Transactional Articles - Specify How Changes Are Propagated](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md) (Artículos transaccionales: Especificar cómo se propagan los cambios).  
  
 [  **@del_cmd =**] **'***del_cmd***'**  
 Es el comando de replicación utilizado al replicar eliminaciones para este artículo. *del_cmd* es **nvarchar (255)**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**NONE**|No se realiza ninguna acción.|  
|**CALLsp_MSdel_**<br /> ***tabla*** (valor predeterminado)<br /><br /> -O bien-<br /><br /> **Llamar a custom_stored_procedure_name**|Llama a un procedimiento almacenado que se ejecutará en el suscriptor. Para utilizar este método de replicación, utilice *schema_option* para especificar la creación automática del procedimiento almacenado o crear el procedimiento almacenado especificado en la base de datos de destino de cada suscriptor del artículo. *custom_stored_procedure* es el nombre de un procedimiento almacenado creado por el usuario. **sp_MSdel_ * tabla*** contiene el nombre de la tabla de destino en lugar de la *_table* parte del parámetro. Cuando *destination_owner* se especifica, se antepone al nombre de la tabla de destino. Por ejemplo, para la **ProductCategory** tabla pertenece a la **producción** esquema en el suscriptor, el parámetro sería `CALL sp_MSdel_ProductionProductCategory`. Para un artículo en una topología de replicación punto a punto, *_table* se anexa con un valor GUID. Especificar *custom_stored_procedure* no se admite para suscriptores de actualización.|  
|**XCALL sp_MSdel_**<br /> ***table***<br /><br /> -O bien-<br /><br /> **XCALL custom_stored_procedure_name**|Llama a un procedimiento almacenado con parámetros del estilo XCALL. Para utilizar este método de replicación, utilice *schema_option* para especificar la creación automática del procedimiento almacenado o crear el procedimiento almacenado especificado en la base de datos de destino de cada suscriptor del artículo. No se permite especificar un procedimiento almacenado creado por el usuario en suscriptores de actualización.|  
|**SQL** o NULL|Replica una instrucción DELETE. La instrucción DELETE recibe todos los valores de las columnas de clave principal. Este comando se replica con las eliminaciones:<br /><br /> `DELETE FROM <table name> WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
 Para obtener más información, vea [Transactional Articles - Specify How Changes Are Propagated](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md) (Artículos transaccionales: Especificar cómo se propagan los cambios).  
  
 [  **@upd_cmd =**] **'***upd_cmd***'**  
 Es el comando de replicación utilizado al replicar actualizaciones para este artículo. *upd_cmd* es **nvarchar (255)**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**NONE**|No se realiza ninguna acción.|  
|**Sp_MSupd_ de llamada**<br /> ***table***<br /><br /> -O bien-<br /><br /> **Llamar a custom_stored_procedure_name**|Llama a un procedimiento almacenado que se ejecutará en el suscriptor. Para utilizar este método de replicación, utilice *schema_option* para especificar la creación automática del procedimiento almacenado o crear el procedimiento almacenado especificado en la base de datos de destino de cada suscriptor del artículo.|  
|**MCALL sp_MSupd_**<br /> ***table***<br /><br /> -O bien-<br /><br /> **MCALL custom_stored_procedure_name**|Llama a un procedimiento almacenado con parámetros del estilo MCALL. Para utilizar este método de replicación, utilice *schema_option* para especificar la creación automática del procedimiento almacenado o crear el procedimiento almacenado especificado en la base de datos de destino de cada suscriptor del artículo. *custom_stored_procedure* es el nombre de un procedimiento almacenado creado por el usuario. **sp_MSupd_ * tabla*** contiene el nombre de la tabla de destino en lugar de la *_table* parte del parámetro. Cuando *destination_owner* se especifica, se antepone al nombre de la tabla de destino. Por ejemplo, para la **ProductCategory** tabla pertenece a la **producción** esquema en el suscriptor, el parámetro sería `MCALL sp_MSupd_ProductionProductCategory`. Para un artículo en una topología de replicación punto a punto, *_table* se anexa con un valor GUID. No se permite especificar un procedimiento almacenado creado por el usuario en suscriptores de actualización.|  
|**SCALL sp_MSupd_**<br /> ***tabla*** (valor predeterminado)<br /><br /> -O bien-<br /><br /> **SCALL custom_stored_procedure_name**|Llama a un procedimiento almacenado con parámetros del estilo SCALL. Para utilizar este método de replicación, utilice *schema_option* para especificar la creación automática del procedimiento almacenado o crear el procedimiento almacenado especificado en la base de datos de destino de cada suscriptor del artículo. *custom_stored_procedure* es el nombre de un procedimiento almacenado creado por el usuario. **sp_MSupd_ * tabla*** contiene el nombre de la tabla de destino en lugar de la *_table* parte del parámetro. Cuando *destination_owner* se especifica, se antepone al nombre de la tabla de destino. Por ejemplo, para la **ProductCategory** tabla pertenece a la **producción** esquema en el suscriptor, el parámetro sería `SCALL sp_MSupd_ProductionProductCategory`. Para un artículo en una topología de replicación punto a punto, *_table* se anexa con un valor GUID. No se permite especificar un procedimiento almacenado creado por el usuario en suscriptores de actualización.|  
|**Sp_MSupd_ XCALL**<br /> ***table***<br /><br /> -O bien-<br /><br /> **XCALL custom_stored_procedure_name**|Llama a un procedimiento almacenado con parámetros del estilo XCALL. Para utilizar este método de replicación, utilice *schema_option* para especificar la creación automática del procedimiento almacenado o crear el procedimiento almacenado especificado en la base de datos de destino de cada suscriptor del artículo. No se permite especificar un procedimiento almacenado creado por el usuario en suscriptores de actualización.|  
|**SQL** o NULL|Replica una instrucción UPDATE. La instrucción UPDATE está disponible en todos los valores de columna y los valores de las columnas de clave principal. Este comando se replica con las actualizaciones:<br /><br /> `UPDATE <table name> SET c1 = c1value, SET c2 = c2value, SET cn = cnvalue WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
> [!NOTE]  
>  La sintaxis CALL, MCALL, SCALL y XCALL varía la cantidad de datos propagados al suscriptor. La sintaxis CALL pasa todos los valores de todas las columnas insertadas y eliminadas. La sintaxis SCALL solo pasa los valores de las columnas afectadas. La sintaxis XCALL pasa los valores de todas las columnas, tanto si han cambiado como si no, incluido el valor anterior de la columna. Para obtener más información, vea [Transactional Articles - Specify How Changes Are Propagated](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md) (Artículos transaccionales: Especificar cómo se propagan los cambios).  
  
 [  **@creation_script =**] **'***creation_script***'**  
 Es la ruta de acceso y el nombre de un script opcional del esquema del artículo que se utiliza para crear el artículo en la base de datos de suscripciones. *creation_script* es **nvarchar (255)**, su valor predeterminado es null.  
  
 [  **@description =**] **'***descripción***'**  
 Es una entrada descriptiva del artículo. *descripción* es **nvarchar (255)**, su valor predeterminado es null.  
  
 [  **@pre_creation_cmd =**] **'***pre_creation_cmd***'**  
 Especifica lo que debería hacer el sistema si detecta un objeto existente con el mismo nombre en el suscriptor cuando se aplica la instantánea para este artículo. *pre_creation_cmd* es **nvarchar (10)**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**Ninguno**|No usa ningún comando.|  
|**delete**|Elimina datos de la tabla de destino antes de aplicar la instantánea. Cuando el artículo se filtra horizontalmente, solo se eliminan los datos en las columnas especificadas en la cláusula de filtro. No se admite en publicadores de Oracle si se ha definido un filtro horizontal.|  
|**quitar** (valor predeterminado)|Quita la tabla de destino.|  
|**truncate**|Trunca la tabla de destino. No es válido para los suscriptores de ODBC o de OLE DB.|  
  
 [  **@filter_clause=**] **'***filter_clause***'**  
 Es una cláusula de restricción (WHERE) que define un filtro horizontal. Al especificar la cláusula de restricción, omita la palabra clave WHERE. *filter_clause* es **ntext**, su valor predeterminado es null. Para obtener más información, vea [Filtrar datos publicados](../../relational-databases/replication/publish/filter-published-data.md).  
  
 [  **@schema_option =**] *schema_option*  
 Es una máscara de bits de la opción de generación del esquema para el artículo dado. *schema_option* es **binary (8)**y puede ser el [| (OR bit a bit) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) producto de uno o varios de estos valores:  
  
> [!NOTE]  
>  Si este valor es NULL, el sistema genera automáticamente una opción de esquema válida para el artículo dependiendo de las propiedades del artículo. El **opciones de esquema predeterminadas** tabla en la sección Notas muestra el valor que se elegirá según la combinación del tipo de artículo y el tipo de replicación.  
  
|Value|Description|  
|-----------|-----------------|  
|**0 x 00**|Deshabilita el scripting del agente de instantáneas y utiliza *creation_script*.|  
|**0 x 01**|Genera el script de creación del objeto (CREATE TABLE, CREATE PROCEDURE, etc.). Este valor es el predeterminado en los artículos de procedimientos almacenados.|  
|**0 x 02**|Genera los procedimientos almacenados que propagan los cambios del artículo, si se han definido.|  
|**0 x 04**|Las columnas de identidad se incluyen en los scripts con la propiedad IDENTITY.|  
|**0 x 08**|Replicar **timestamp** columnas. Si no se establece, **timestamp** las columnas se replican como **binario**.|  
|**0 x 10**|Genera el índice clúster correspondiente. Incluso si no se establece esta opción, los índices relacionados con las claves principales y las restricciones unique se generan si ya están definidos en una tabla publicada.|  
|**0 x 20**|Convierte los tipos de datos definidos por el usuario (UDT) en tipos de datos base en el suscriptor. Esta opción no se puede utilizar si existe una restricción CHECK o DEFAULT en una columna UDT, si una columna UDT forma parte de la clave principal o si una columna calculada hace referencia a una columna UDT. *No se admite en publicadores de Oracle*.|  
|**0 x 40**|Genera los índices no clúster correspondientes. Incluso si no se establece esta opción, los índices relacionados con las claves principales y las restricciones unique se generan si ya están definidos en una tabla publicada.|  
|**0 x 80**|Replica las restricciones de clave principal. También se replican los índices relacionados con la restricción, aunque opciones **0 x 10** y **0 x 40** no están habilitadas.|  
|**0 x 100**|Replica los desencadenadores de usuario en un artículo de tabla, si se han definido. *No se admite en publicadores de Oracle*.|  
|**0 x 200**|Replica las restricciones de clave externa. Si la tabla a la que se hace referencia no forma parte de una publicación, no se replica ninguna restricción de clave externa de una tabla publicada. *No se admite en publicadores de Oracle*.|  
|**0 x 400**|Replica las restricciones CHECK. *No se admite en publicadores de Oracle*.|  
|**0 x 800**|Replica los valores predeterminados. *No se admite en publicadores de Oracle*.|  
|**0 x 1000**|Replica la intercalación de columna.<br /><br /> **Nota:** esta opción debe establecerse para que los publicadores de Oracle habilitar las comparaciones entre mayúsculas y minúsculas.|  
|**0 x 2000**|Replica las propiedades extendidas asociadas con el objeto de origen del artículo publicado. *No se admite en publicadores de Oracle*.|  
|**0 x 4000**|Replica las restricciones UNIQUE. También se replican los índices relacionados con la restricción, aunque opciones **0 x 10** y **0 x 40** no están habilitadas.|  
|**0 x 8000**|Esta opción no es válida para publicadores de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0 x 10000**|Replica las restricciones CHECK como NOT FOR REPLICATION de manera que no se impongan durante la sincronización.|  
|**0 x 20000**|Replica las restricciones FOREIGN KEY como NOT FOR REPLICATION de manera que no se impongan durante la sincronización.|  
|**0 x 40000**|Replica grupos de archivos asociados con un índice o una tabla con particiones.|  
|**0 x 80000**|Replica el esquema de partición de una tabla con particiones.|  
|**0 x 100000**|Replica el esquema de partición de un índice con particiones.|  
|**0 x 200000**|Replica las estadísticas de tabla.|  
|**0 x 400000**|Enlaces predeterminados|  
|**0 x 800000**|Enlaces de reglas|  
|**0 x 1000000**|Índice de texto completo|  
|**0x2000000**|Colecciones de esquemas XML enlazado a **xml** columnas no se replican.|  
|**0x4000000**|Replica índices en **xml** columnas.|  
|**0 x 8000000**|Crea esquemas que aún no existen en el suscriptor.|  
|**0 x 10000000**|Convierte **xml** columnas a **ntext** en el suscriptor.|  
|**0 x 20000000**|Convierte los objetos grandes tipos de datos (**nvarchar (max)**, **varchar (max)**, y **varbinary (max)**) introducido en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para tipos de datos que se admiten en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
|**0 x 40000000**|Replica permisos.|  
|**0 x 80000000**|Ha intentado quitar dependencias a objetos que no forman parte de la publicación.|  
|**0 x 100000000**|Utilice esta opción para replicar el atributo FILESTREAM si se especifica en **varbinary (max)** columnas. No especifique esta opción si replica tablas en suscriptores de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Replicación de tablas que incluyen columnas FILESTREAM en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] no se admiten los suscriptores, sin tener en cuenta cómo se establece esta opción de esquema.<br /><br /> Vea la opción relacionada **0 x 800000000**.|  
|**0x200000000**|Convierte los tipos de datos de fecha y hora (**fecha**, **tiempo**, **datetimeoffset**, y **datetime2**) introducido en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a los datos tipos que se admiten en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**0x400000000**|Replica la opción de compresión para los datos y los índices. Para obtener más información, consulte [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
|**0 x 800000000**|Establezca esta opción para almacenar los datos de FILESTREAM en su propio grupo de archivos en el suscriptor. Si no se establece esta opción, los datos de FILESTREAM se almacenan en el grupo de archivos predeterminado. La replicación no crea grupos de archivos; por tanto, si establece esta opción, debe crear el grupo de archivos antes de aplicar la instantánea en el suscriptor. Para obtener más información sobre cómo crear objetos antes de aplicar la instantánea, vea [ejecutar Scripts antes y después de aplicar la instantánea](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).<br /><br /> Vea la opción relacionada **0 x 100000000**.|  
|**0x1000000000**|Convierte tipos common language runtime (CLR) definido por el usuario (UDT) que son mayores de 8.000 bytes en **varbinary (max)** para que las columnas de tipo UDT se pueden replicar en suscriptores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x2000000000**|Convierte el **hierarchyid** tipo de datos que **varbinary (max)** para que las columnas de tipo **hierarchyid** se pueden replicar en suscriptores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obtener más información sobre cómo usar **hierarchyid** columnas en las tablas replicadas, vea [hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
|**0x4000000000**|Replica los índices filtrados de la tabla. Para obtener más información sobre los índices filtrados, vea [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).|  
|**0x8000000000**|Convierte el **geography** y **geometry** tipos de datos **varbinary (max)** para que las columnas de estos tipos se pueden replicar en suscriptores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x10000000000**|Replica índices en columnas de tipo **geography** y **geometría**.|  
|**0x20000000000**|Replica el atributo SPARSE para las columnas. Para obtener más información acerca de este atributo, vea [usar columnas dispersas](../../relational-databases/tables/use-sparse-columns.md).|  
|**0 x 40000000000**|Habilitar scripting del agente de instantáneas para crear la tabla optimizada en memoria en el suscriptor.|  
|**0x80000000000**|Convierte el índice agrupado a un índice no clúster para los artículos con optimización para memoria.|  
|**0x400000000000**|Replica los índices de almacén de columnas no agrupado en la tabla (s)|  
|**0x800000000000**|Replica los índices de almacén de columnas no agrupado flitered en las tablas.|  
|NULL|La replicación establece automáticamente *schema_option* en un valor predeterminado, el valor de los cuales depende de las propiedades del artículo. La tabla "Opciones de esquema predeterminadas" de la sección Notas muestra las opciones de esquema predeterminadas basadas en los tipos de artículo y de replicación.<br /><br /> El valor predeterminado de no -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicaciones es **0x050D3**.|  
  
 No todos los *schema_option* valores son válidos para todos los tipos de replicación y el tipo de artículo. El **opciones de esquema válidas** tabla en la sección Notas muestra las opciones de esquema válidas que se pueden elegir según la combinación del tipo de artículo y el tipo de replicación.  
  
 [  **@destination_owner =**] **'***destination_owner***'**  
 Es el nombre del propietario del objeto de destino. *destination_owner* es **sysname**, su valor predeterminado es null. Cuando *destination_owner* no se especifica, el propietario se especifica automáticamente basándose en las reglas siguientes:  
  
|Condición|Propietario del objeto de destino|  
|---------------|------------------------------|  
|La publicación utiliza una copia masiva en modo nativo para generar la instantánea inicial, que solo admite suscriptores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Valor predeterminado es el valor de *source_owner*.|  
|Publicado desde un publicador que no es de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|El valor predeterminado es el propietario de la base de datos de destino.|  
|La publicación utiliza una copia masiva en modo de carácter para generar la instantánea inicial, que admite suscriptores que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|No asignado.|  
  
 Para que admita no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suscriptores, *destination_owner* debe ser NULL.  
  
 [  **@status=**] *estado*  
 Especifica si el artículo está activo, así como opciones adicionales sobre cómo se propagan los cambios. *estado* es **tinyint**y puede ser el [| (OR bit a bit) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) producto de uno o varios de estos valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|El artículo está activo.|  
|**8**|Incluye el nombre de la columna en las instrucciones INSERT.|  
|**16** (valor predeterminado)|Usa instrucciones con parámetros.|  
|**24**|Incluye el nombre de la columna en las instrucciones INSERT y usa instrucciones con parámetros.|  
|**64**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 Por ejemplo, un artículo activo que utilice instrucciones con parámetros tendrá un valor de 17 en esta columna. Un valor de **0** significa que el artículo está inactivo y no se definen propiedades adicionales.  
  
 [  **@source_owner =**] **'***source_owner***'**  
 Es el nombre del propietario del objeto de origen. *source_owner* es **sysname**, su valor predeterminado es null. *source_owner* debe especificarse para los publicadores de Oracle.  
  
 [  **@sync_object_owner =**] **'***sync_object_owner***'**  
 Es el nombre del propietario de la vista que define el artículo publicado. *sync_object_owner* es **sysname**, su valor predeterminado es null.  
  
 [  **@filter_owner =**] **'***filter_owner***'**  
 Es el propietario del filtro. *filter_owner* es **sysname**, su valor predeterminado es null.  
  
 [  **@source_object =**] **'***source_object***'**  
 Es el objeto de base de datos que se va a publicar. *source_object* es **sysname**, su valor predeterminado es null. Si *source_table* es NULL, *source_object* no puede ser NULL. *source_object* debe usarse en lugar de *source_table*. Para obtener más información acerca de los tipos de objetos que se pueden publicar mediante la replicación transaccional o instantáneas, vea [publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 [  **@artid =** ] *article_ID* **salida**  
 Es el id. del nuevo artículo. *article_ID* es **int** con un valor predeterminado es NULL y es un parámetro de salida.  
  
 [  **@auto_identity_range =** ] **'***auto_identity_range***'**  
 Habilita o deshabilita el control automático de un rango de identidad en una publicación en el momento en que se crea. *auto_identity_range* es **nvarchar (5)**, y puede tener uno de los siguientes valores:  
  
|Value|Description|  
|-----------|-----------------|  
|**true**|Habilita la administración automática de intervalos de identidad|  
|**False**|Deshabilita la administración automática de intervalos de identidad|  
|NULL(Default)|Administración de intervalos de identidad se establece *identityrangemanagementoption*.|  
  
> [!NOTE]  
>  *auto_identity_range* ha quedado desusado y se proporciona por compatibilidad con versiones anteriores. Debe usar *identityrangemanagementoption* para especificar opciones de administración de intervalos de identidad. Para más información, vea [Replicar columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@pub_identity_range =** ] *pub_identity_range*  
 Controla el tamaño del intervalo en el publicador si el artículo tiene *identityrangemanagementoption* establecido en **automática** o *auto_identity_range* establecido en **es true** . *pub_identity_range* es **bigint**, su valor predeterminado es null. *No se admite en publicadores de Oracle*.  
  
 [  **@identity_range =** ] *identity_range*  
 Controla el tamaño del intervalo en el suscriptor si el artículo tiene *identityrangemanagementoption* establecido en **automática** o *auto_identity_range* establecido en **es true** . *identity_range* es **bigint**, su valor predeterminado es null. Se usa cuando *auto_identity_range* está establecido en **true**. *No se admite en publicadores de Oracle*.  
  
 [  **@threshold =** ] *umbral*  
 Es el valor de porcentaje que controla cuándo el Agente de distribución asigna un nuevo intervalo de identidad. Cuando se especifica el porcentaje de valores en *umbral* es usa, el agente de distribución crea un nuevo intervalo de identidad. *umbral* es **bigint**, su valor predeterminado es null. Se usa cuando *identityrangemanagementoption* está establecido en **automática** o *auto_identity_range* está establecido en **true**. *No se admite en publicadores de Oracle*.  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Confirma que la acción realizada por este procedimiento almacenado puede invalidar una instantánea existente. *force_invalidate_snapshot* es un **bits**, con un valor predeterminado es 0.  
  
 **0** especifica que el agregar un artículo no invalidarán la instantánea no es válida. Si el procedimiento almacenado detecta que el cambio requiere una nueva instantánea, se produce un error y no se realizan cambios.  
  
 **1** especifica que agregar un artículo puede invalidar la instantánea no es válida y si existen suscripciones que requieran una nueva instantánea, concede el permiso necesario para marcar como obsoleta la instantánea existente y generar una nueva instantánea.  
  
 [  **@use_default_datatypes =** ] *use_default_datatypes*  
 Indica si se utilizan asignaciones de tipos de datos de columna predeterminadas al publicar un artículo desde un publicador de Oracle. *use_default_datatypes* es de tipo bit, con un valor predeterminado es 1.  
  
 **1** = la columna del artículo de forma predeterminada se usan las asignaciones. Se pueden mostrar las asignaciones de tipos de datos de forma predeterminada mediante la ejecución de [sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md).  
  
 **0** = columnas de artículo personalizadas se definen asignaciones y, por tanto, [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) no llama a **sp_addarticle**.  
  
 Cuando *use_default_datatypes* está establecido en **0**, debe ejecutar [sp_changearticlecolumndatatype](../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md) una vez para cada asignación de columna que se cambia el valor predeterminado. Después de que se han definido todas las asignaciones de columna personalizada, debe ejecutar [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md).  
  
> [!NOTE]  
>  Este parámetro solo debe utilizarse en publicadores de Oracle. Establecer *use_default_datatypes* a **0** para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador genera un error.  
  
 [  **@identityrangemanagementoption =** ] *identityrangemanagementoption*  
 Especifica cómo se controla el rango de identidad para el artículo. *valor de identityrangemanagementoption* es **nvarchar (10)**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**Ninguno**|La replicación no realiza una administración de intervalos de identidad explícita. Se recomienda esta opción solo por compatibilidad con las versiones anteriores de SQL Server. No se permite en la replicación del mismo nivel.|  
|**Manual**|Marca la columna de identidad utilizando NOT FOR REPLICATION para habilitar la administración manual de intervalos de identidad.|  
|**Automático**|Especifica la administración automática de intervalos de identidad.|  
|NULL(Default)|Valor predeterminado es **ninguno** cuando el valor de *auto_identity_range* no **true**. Valor predeterminado es **manual** en un valor predeterminado de la topología punto a punto (*auto_identity_range* se pasa por alto).|  
  
 Por compatibilidad con versiones anteriores, cuando el valor de *identityrangemanagementoption* es NULL, el valor de *auto_identity_range* está activada. Sin embargo, cuando el valor de *identityrangemanagementoption* no es NULL, entonces el valor de *auto_identity_range* se omite.  
  
 Para más información, vea [Replicar columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@publisher =** ] **'***publisher***'**  
 Especifica un publicador que no es de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Publisher* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *Publisher* no debe usarse cuando se agrega un artículo a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
 [  **@fire_triggers_on_snapshot =** ] **'***fire_triggers_on_snapshot***'**  
 Indica si se ejecutan desencadenadores de usuario replicados al aplicar la instantánea inicial. *fire_triggers_on_snapshot* es **nvarchar (5)**, con un valor predeterminado es FALSE. **True** significa que los desencadenadores de usuario en una tabla replicada se ejecutan cuando se aplica la instantánea. En el orden de los desencadenadores se repliquen, el valor de máscara de bits de *schema_option* debe incluir el valor **0 x 100**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addarticle** se utiliza en la replicación de instantáneas o replicación transaccional.  
  
 De forma predeterminada, la replicación no publica columnas en la tabla de origen cuando el tipo de datos de columna no se admite en la replicación. Si tiene que publicar este tipo de columna, debe ejecutar [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) para agregar la columna.  
  
 Al agregar un artículo a una publicación que admite la replicación transaccional punto a punto, se aplican las restricciones siguientes:  
  
-   Deben especificarse instrucciones con parámetros para todos los artículos de tipo logbased. Debe incluir **16** en el *estado* valor.  
  
-   El nombre y el propietario de la tabla de destino deben coincidir con los de la tabla de origen.  
  
-   El artículo no puede filtrarse horizontal ni verticalmente.  
  
-   No se admite la administración automática de intervalos de identidad. Debe especificar un valor de manual de *identityrangemanagementoption*.  
  
-   Si un **timestamp** columna existe en la tabla, se debe incluir 0 x 08 en *schema_option* para replicar la columna como **marca de tiempo**.  
  
-   Un valor de **SQL** no se puede especificar para *ins_cmd*, *upd_cmd*, y *del_cmd*.  
  
 Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 Al publicar objetos, sus definiciones se copian en los suscriptores. Si va a publicar un objeto de base de datos que depende de uno o varios objetos, debe publicar todos los objetos a los que hace referencia. Por ejemplo, si publica una vista que depende de una tabla, también debe publicar la tabla.  
  
 Si *vertical_partition* está establecido en **true**, **sp_addarticle** aplaza la creación de la vista hasta que [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) se denomina (después de la última [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) se agrega).  
  
 Si la publicación permite suscripciones de actualización y la tabla publicada no tiene un **uniqueidentifier** columna, **sp_addarticle** agrega un **uniqueidentifier** columna en la tabla automáticamente.  
  
 Cuando se replican a un suscriptor que no es una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (replicación heterogénea), solo [!INCLUDE[tsql](../../includes/tsql-md.md)] se admiten las instrucciones para **insertar**, **actualización**y **Eliminar** comandos.  
  
 Cuando el agente de registro del LOG se está ejecutando, al agregar un artículo a una publicación punto a punto se puede producir un interbloqueo entre el agente de registro del LOG y el proceso que agrega el artículo. Para evitar este problema, antes de agregar un artículo a la publicación punto a punto, use el Monitor de replicación para detener el agente de registro del LOG en el nodo donde se agrega el artículo. Reinicie el agente de registro del LOG después de agregar el artículo.  
  
 Al establecer `@del_cmd = 'NONE'` o `@ins_cmd = 'NONE'`, la propagación de **actualizar** comandos también podrían verse afectados no enviando esos comandos cuando se produce una actualización enlazada. (Una actualización enlazada es el tipo de instrucción UPDATE del publicador que se replica como un par DELETE/INSERT en el suscriptor).  
  
## <a name="default-schema-options"></a>Opciones de esquema predeterminadas  
 Esta tabla describen el valor predeterminado establecido por la replicación si *schema_options* no se especifica por el usuario, donde este valor depende del tipo de replicación (se muestra en la parte superior) y el tipo de artículo (que se muestra la primera columna).  
  
|Tipo de artículo|Tipo de replicación||  
|------------------|----------------------|------|  
||Transaccional|Snapshot|  
|**solo esquema agregado**|**0 x 01**|**0 x 01**|  
|**solo esquema Func**|**0 x 01**|**0 x 01**|  
|**solo el esquema de vista indizada**|**0 x 01**|**0 x 01**|  
|**logbased de vista indizada**|**0x30F3**|**0x3071**|  
|**vista indizada logbase manualboth**|**0x30F3**|**0x3071**|  
|**vista indizada logbased manualfilter**|**0x30F3**|**0x3071**|  
|**vista indizada logbased manualview**|**0x30F3**|**0x3071**|  
|**logbased**|**0x30F3**|**0x3071**|  
|**logbased manualfilter**|**0x30F3**|**0x3071**|  
|**logbased manualview**|**0x30F3**|**0x3071**|  
|**proc exec**|**0 x 01**|**0 x 01**|  
|**solo el esquema de procedimiento**|**0 x 01**|**0 x 01**|  
|**serializable proc exec**|**0 x 01**|**0 x 01**|  
|**solo el esquema de vista**|**0 x 01**|**0 x 01**|  
  
> [!NOTE]  
>  Si se habilita una publicación de actualización en cola, un *schema_option* valo **0 x 80** se agrega al valor predeterminado se muestra en la tabla. El valor predeterminado *schema_option* para no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicación está **0x050D3**.  
  
## <a name="valid-schema-options"></a>Opciones de esquema válidas  
 Esta tabla describen los valores permitidos de *schema_option* basado en el tipo de replicación (se muestra en la parte superior) y el tipo de artículo (que se muestra la primera columna).  
  
|Tipo de artículo|Tipo de replicación||  
|------------------|----------------------|------|  
||Transaccional|Snapshot|  
|**logbased**|Todas las opciones|Todas las opciones pero **0 x 02**|  
|**logbased manualfilter**|Todas las opciones|Todas las opciones pero **0 x 02**|  
|**logbased manualview**|Todas las opciones|Todas las opciones pero **0 x 02**|  
|**logbased de vista indizada**|Todas las opciones|Todas las opciones pero **0 x 02**|  
|**vista indizada logbased manualfilter**|Todas las opciones|Todas las opciones pero **0 x 02**|  
|**vista indizada logbased manualview**|Todas las opciones|Todas las opciones pero **0 x 02**|  
|**vista indizada logbase manualboth**|Todas las opciones|Todas las opciones pero **0 x 02**|  
|**proc exec**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|  
|**serializable proc exec**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|  
|**solo el esquema de procedimiento**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|  
|**solo el esquema de vista**|**0 x 01**, **0 x 010**, **0 x 020**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 100000**, **0 x 200000**, **0 x 400000**, **0 x 800000**,  **0x2000000**, **0 x 8000000**, **0 x 40000000**, y **0 x 80000000**|**0 x 01**, **0 x 010**, **0 x 020**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 100000**, **0 x 200000**, **0 x 400000**, **0 x 800000**,  **0x2000000**, **0 x 8000000**, **0 x 40000000**, y **0 x 80000000**|  
|**solo esquema Func**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|  
|**solo el esquema de vista indizada**|**0 x 01**, **0 x 010**, **0 x 020**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 100000**, **0 x 200000**, **0 x 400000**, **0 x 800000**,  **0x2000000**, **0 x 8000000**, **0 x 40000000**, y **0 x 80000000**|**0 x 01**, **0 x 010**, **0 x 020**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 100000**, **0 x 200000**, **0 x 400000**, **0 x 800000**,  **0x2000000**, **0 x 8000000**, **0 x 40000000**, y **0 x 80000000**|  
  
> [!NOTE]  
>  Para las publicaciones de actualización en cola, el *schema_option* valores de **0 x 8000** y **0 x 80** debe estar habilitada. Admiten *schema_option* para los valores no son[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicaciones son: **0 x 01**, **0 x 02**, **0 x 10**,  **0 x 40**, **0 x 80**, **0 x 1000**, **0 x 4000** y **0 x 8000**.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-addarticle-transact-sql_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_addarticle**.  
  
## <a name="see-also"></a>Vea también  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_articleview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
