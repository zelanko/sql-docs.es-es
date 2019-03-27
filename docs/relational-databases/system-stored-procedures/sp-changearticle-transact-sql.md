---
title: sp_changearticle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changearticle
- sp_changearticle_TSQL
helpviewer_keywords:
- sp_changearticle
ms.assetid: 24c33ca5-f03a-4417-a267-131ca5ba6bb5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cbfbb923a831901bd42724759372f8b1f7ccbc0c
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493457"
---
# <a name="spchangearticle-transact-sql"></a>sp_changearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de un artículo en una publicación transaccional o de instantáneas. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changearticle [ [@publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es el nombre de la publicación que contiene el artículo. *publicación* es **sysname**, su valor predeterminado es null.  
  
`[ @article = ] 'article'` Es el nombre del artículo cuya propiedad se va a cambiar. *artículo* es **sysname**, su valor predeterminado es null.  
  
`[ @property = ] 'property'` Es una propiedad de artículo para cambiar. *propiedad* es **nvarchar (100)**.  
  
`[ @value = ] 'value'` Es el nuevo valor de la propiedad de artículo. *valor* es **nvarchar (255)**.  
  
 En esta tabla se describen las propiedades de los artículos y los valores de esas propiedades.  
  
|Property|Valores|Descripción|  
|--------------|------------|-----------------|  
|**creation_script**||Ruta de acceso y nombre de un script de esquema del artículo que se utiliza para crear tablas de destino. El valor predeterminado es NULL.|  
|**del_cmd**||Instrucción DELETE que se va a ejecutar; de lo contrario, se genera a partir del registro.|  
|**description**||Nueva entrada descriptiva del artículo.|  
|**dest_object**||Se proporciona para mantener la compatibilidad con versiones anteriores. Use **dest_table**.|  
|**dest_table**||Nueva tabla de destino.|  
|**destination_owner**||Nombre del propietario del objeto de destino.|  
|**filter**||Nuevo procedimiento almacenado para filtrar la tabla (filtrado horizontal). El valor predeterminado es NULL. No se puede cambiar para las publicaciones de replicación punto a punto.|  
|**fire_triggers_on_snapshot**|**true**|Los desencadenadores de usuario replicados se ejecutan cuando se aplica la instantánea inicial.<br /><br /> Nota: Para los desencadenadores que replicarse, el valor de máscara de bits de *schema_option* debe incluir el valor **0 x 100**.|  
||**False**|Los desencadenadores de usuario replicados no se ejecutan cuando se aplica la instantánea inicial.|  
|**identity_range**||Controla el tamaño de los intervalos de identidad asignados en el suscriptor. No se admite para la replicación punto a punto.|  
|**ins_cmd**||Instrucción INSERT que se ejecuta; de lo contrario, se crea a partir del registro.|  
|**pre_creation_cmd**||Comando de creación previa que puede quitar, eliminar o truncar la tabla de destino antes de que se aplique la sincronización.|  
||**Ninguno**|No usa ningún comando.|  
||**drop**|Quita la tabla de destino.|  
||**delete**|Elimina la tabla de destino.|  
||**truncate**|Trunca la tabla de destino.|  
|**pub_identity_range**||Controla el tamaño de los intervalos de identidad asignados en el suscriptor. No se admite para la replicación punto a punto.|  
|**schema_option**||Especifica el mapa de bits de la opción de generación del esquema para el artículo especificado. *schema_option* es **binary (8)**. Para obtener más información, vea la sección Comentarios más adelante en este tema.|  
||**0x00**|Deshabilita el scripting del Agente de instantáneas.|  
||**0x01**|Genera la creación del objeto (CREATE TABLE, CREATE PROCEDURE, etc.).|  
||**0x02**|Genera los procedimientos almacenados que propagan los cambios del artículo, si se han definido.|  
||**0x04**|Las columnas de identidad se incluyen en los scripts con la propiedad IDENTITY.|  
||**0x08**|Replicar **timestamp** columnas. Si no se establece, **timestamp** columnas se replican como **binario**.|  
||**0x10**|Genera el índice clúster correspondiente.|  
||**0x20**|Convierte los tipos de datos definidos por el usuario (UDT) en tipos de datos base en el suscriptor. Esta opción no se puede utilizar si existe una restricción CHECK o DEFAULT en una columna UDT, si una columna UDT forma parte de la clave principal o si una columna calculada hace referencia a una columna UDT. No es compatible con publicadores de Oracle.|  
||**0x40**|Genera los índices no clúster correspondientes.|  
||**0x80**|Incluye la integridad referencial declarada para las claves principales.|  
||**0x100**|Replica los desencadenadores de usuario en un artículo de tabla, si se han definido.|  
||**0x200**|Replica restricciones FOREIGN KEY. Si la tabla a la que se hace referencia no forma parte de una publicación, no se replica ninguna restricción FOREIGN KEY en una tabla publicada.|  
||**0x400**|Replica las restricciones CHECK.|  
||**0x800**|Replica los valores predeterminados.|  
||**0x1000**|Replica la intercalación de columna.|  
||**0x2000**|Replica las propiedades extendidas asociadas con el objeto de origen del artículo publicado.|  
||**0x4000**|Replica las claves únicas si están definidas en un artículo de tabla.|  
||**0x8000**|Replica la clave principal y las claves únicas de un artículo de tabla como restricciones mediante instrucciones ALTER TABLE.<br /><br /> Nota: Esta opción ha quedado desusada. Use **0 x 80** y **0 x 4000** en su lugar.|  
||**0x10000**|Replica las restricciones CHECK como NOT FOR REPLICATION de manera que no se impongan durante la sincronización.|  
||**0x20000**|Replica las restricciones FOREIGN KEY como NOT FOR REPLICATION de manera que no se impongan durante la sincronización.|  
||**0x40000**|Replica grupos de archivos asociados con un índice o una tabla con particiones.|  
||**0x80000**|Replica el esquema de partición de una tabla con particiones.|  
||**0x100000**|Replica el esquema de partición de un índice con particiones.|  
||**0x200000**|Replica las estadísticas de tabla.|  
||**0x400000**|Enlaces predeterminados|  
||**0x800000**|Enlaces de reglas|  
||**0x1000000**|Índice de texto completo|  
||**0x2000000**|Colecciones de esquemas XML enlazado a **xml** columnas no se replican.|  
||**0x4000000**|Replica índices en **xml** columnas.|  
||**0x8000000**|Crea esquemas que aún no existen en el suscriptor.|  
||**0x10000000**|Convierte **xml** columnas a **ntext** en el suscriptor.|  
||**0x20000000**|Convierte objetos grandes tipos de datos (**nvarchar (max)**, **varchar (max)**, y **varbinary (max)**) que se introdujeron en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a tipos de datos que son compatibles en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
||**0x40000000**|Replica permisos.|  
||**0x80000000**|Intenta quitar dependencias a objetos que no forman parte de la publicación.|  
||**0x100000000**|Use esta opción para replicar el atributo FILESTREAM si se especifica en **varbinary (max)** columnas. No especifique esta opción si replica tablas en suscriptores de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Replicación de tablas que incluyen columnas FILESTREAM en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] no es compatible con suscriptores, independientemente de cómo se establece esta opción de esquema.<br /><br /> Vea la opción relacionada **0 x 800000000**.|  
||**0x200000000**|Convierte los tipos de datos de fecha y hora (**fecha**, **tiempo**, **datetimeoffset**, y **datetime2**) que se introdujeron en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tipos de datos que se admiten en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**0x400000000**|Replica la opción de compresión para los datos y los índices. Para obtener más información, consulte [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
||**0x800000000**|Establezca esta opción para almacenar los datos de FILESTREAM en su propio grupo de archivos en el suscriptor. Si no se establece esta opción, los datos de FILESTREAM se almacenan en el grupo de archivos predeterminado. La replicación no crea grupos de archivos; por tanto, si establece esta opción, debe crear el grupo de archivos antes de aplicar la instantánea en el suscriptor. Para obtener más información sobre cómo crear objetos antes de aplicar la instantánea, vea [ejecutar Scripts antes y después de aplicar la instantánea](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).<br /><br /> Vea la opción relacionada **0 x 100000000**.|  
||**0x1000000000**|Convierte los tipos common language runtime (CLR) definido por el usuario (UDT) más de 8.000 bytes para **varbinary (max)** para que las columnas de tipo UDT se pueden replicar en suscriptores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x2000000000**|Convierte el **hierarchyid** tipo de datos que **varbinary (max)** para que las columnas de tipo **hierarchyid** se pueden replicar en suscriptores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obtener más información sobre cómo usar **hierarchyid** columnas en las tablas replicadas, vea [hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
||**0x4000000000**|Replica los índices filtrados de la tabla. Para obtener más información sobre los índices filtrados, vea [crear índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md).|  
||**0x8000000000**|Convierte el **geography** y **geometría** tipos de datos **varbinary (max)** para que las columnas de estos tipos se pueden replicar en suscriptores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x10000000000**|Replica índices en columnas de tipo **geography** y **geometría**.|  
||**0x20000000000**|Replica el atributo SPARSE para las columnas. Para obtener más información acerca de este atributo, vea [usar columnas dispersas](../../relational-databases/tables/use-sparse-columns.md).|  
||**0x40000000000**|Habilite los scripts mediante el agente de instantáneas para crear la tabla optimizada en memoria en el suscriptor.|  
||**0x80000000000**|Convierte el índice agrupado para un índice no agrupado para artículos con optimización para memoria.|  
|**status**||Especifica el nuevo estado de la propiedad.|  
||**particiones horizontales de DTS**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
||**incluir nombres de columna**|Los nombres de columnas se incluyen en la instrucción INSERT replicada.|  
||**No hay nombres de columna**|Los nombres de columnas no se incluyen en la instrucción INSERT replicada.|  
||**No hay particiones horizontales de dts**|La partición horizontal del artículo no se define mediante una suscripción transformable.|  
||**Ninguno**|Borra todas las opciones de estado en el [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md) de tabla y marca el artículo como inactivo.|  
||**parameters**|Los cambios se propagan al suscriptor mediante comandos con parámetros. Es el valor predeterminado para los artículos nuevos.|  
||**Literales de cadena**|Los cambios se propagan al suscriptor mediante valores literales de cadena.|  
|**sync_object**||Nombre de la tabla o vista utilizada para generar un archivo de salida de sincronización. El valor predeterminado es NULL. No es compatible con publicadores de Oracle.|  
|**tablespace**||Identifica el espacio de tablas utilizado por la tabla de registro de un artículo publicado desde una base de datos Oracle. Para más información, vea [Manage Oracle Databases](../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md) (Administrar bases de datos de Oracle).|  
|**threshold**||Valor de porcentaje que controla cuándo el Agente de distribución asigna un nuevo intervalo de identidad. No se admite para la replicación punto a punto.|  
|**Tipo**||No es compatible con publicadores de Oracle.|  
||**logbased**|Artículo basado en registro.|  
||**logbased manualboth**|Artículo basado en registro con filtro manual y vista manual. Esta opción requiere que el *sync_object* y *filtro* también se pueden establecer las propiedades. No es compatible con publicadores de Oracle.|  
||**logbased manualfilter**|Artículo basado en registro con filtro manual. Esta opción requiere que el *sync_object* y *filtro* también se pueden establecer las propiedades. No es compatible con publicadores de Oracle.|  
||**logbased manualview**|Artículo basado en registro con vista manual. Esta opción requiere que el *sync_object* propiedad también se pueden establecer. No es compatible con publicadores de Oracle.|  
||**indexed viewlogbased**|Artículo de vista indizada basado en registro. No es compatible con publicadores de Oracle. En este tipo de artículo, no es necesario que la tabla base se publique por separado.|  
||**manualboth viewlogbased indizada**|Artículo de vista indizada basado en registro con filtro manual y vista manual. Esta opción requiere que el *sync_object* y *filtro* también se pueden establecer las propiedades. En este tipo de artículo, no es necesario que la tabla base se publique por separado. No es compatible con publicadores de Oracle.|  
||**indexed viewlogbased manualfilter**|Artículo de vista indizada basado en registro con filtro manual. Esta opción requiere el *sync_object* y *filtro* también se pueden establecer las propiedades. En este tipo de artículo, no es necesario que la tabla base se publique por separado. No es compatible con publicadores de Oracle.|  
||**indexed viewlogbased manualview**|Artículo de vista indizada basado en registro con vista manual. Esta opción requiere que el *sync_object* propiedad también se pueden establecer. En este tipo de artículo, no es necesario que la tabla base se publique por separado. No es compatible con publicadores de Oracle.|  
|**upd_cmd**||Instrucción UPDATE que se va a ejecutar; de lo contrario, se genera a partir del registro.|  
|NULL|NULL|Devuelve una lista con las propiedades del artículo que se pueden cambiar.|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` Confirma que la acción realizada por este procedimiento almacenado puede invalidar una instantánea existente. *force_invalidate_snapshot* es un **bit**, su valor predeterminado es **0**.  
  
 **0** especifica que los cambios en el artículo no invalidarán la instantánea no es válido. Si el procedimiento almacenado detecta que el cambio requiere una nueva instantánea, se producirá un error y no se realizarán cambios.  
  
 **1** especifica que los cambios en el artículo pueden invalidar la instantánea no es válido y si hay suscripciones existentes que requieran una nueva instantánea, concede permiso para marcar como obsoleta la instantánea existente y una nueva instantánea generada.  
  
 Vea en la sección de Notas las propiedades que, si se cambian, requieren que se genere una instantánea nueva.  
  
`[ @force_reinit_subscription = ]force_reinit_subscription_` Confirma que la acción realizada por este procedimiento almacenado puede requerir la reinicialización de las suscripciones existentes. *force_reinit_subscription* es un **bit** con un valor predeterminado de **0**.  
  
 **0** especifica que los cambios en el artículo no invalidarán la suscripción para reinicializarla. Si el procedimiento almacenado detecta que el cambio requiere la reinicialización de las suscripciones existentes, se producirá un error y no se realizarán cambios.  
  
 **1** especifica que los cambios en el artículo que se reinicialicen las suscripciones existentes y concede permiso para que se produzca la reinicialización de suscripción.  
  
 Vea en la sección de Notas las propiedades que, si se cambian, requieren que se reinicialicen todas las suscripciones existentes.  
  
`[ @publisher = ] 'publisher'` Especifica que no es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *publicador* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *publicador* no debe usarse cuando se cambia las propiedades del artículo en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changearticle** se utiliza en la replicación de instantáneas y transaccional.  
  
 Cuando un artículo pertenece a una publicación que admite la replicación transaccional punto a punto, sólo se puede cambiar el **descripción**, **ins_cmd**, **upd_cmd**y **del_cmd** propiedades.  
  
 Si se cambia cualquiera de las siguientes propiedades que se genera una nueva instantánea, y debe especificar un valor de **1** para el *force_invalidate_snapshot* parámetro:  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **ins_cmd**  
  
-   **pre_creation_cmd**  
  
-   **schema_options**  
  
-   **upd_cmd**  
  
 Si se cambia cualquiera de las siguientes propiedades requiere existentes se reinicialicen las suscripciones, y debe especificar un valor de **1** para el *force_reinit_subscription* parámetro.  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **filter**  
  
-   **ins_cmd**  
  
-   **status**  
  
-   **upd_cmd**  
  
 Dentro de una publicación existente, puede usar **sp_changearticle** para cambiar un artículo sin tener que quitar y volver a crear toda la publicación.  
  
> [!NOTE]  
>  Al cambiar el valor de *schema_option*, el sistema no lleva a cabo una actualización bit a bit. Esto significa que al establecer *schema_option* mediante **sp_changearticle**existente puede desactivarse la configuración de bits. Para conservar la configuración existente, debe realizar [| (OR bit a bit) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) entre el valor que se está estableciendo y el valor actual de *schema_option*, que se puede determinar mediante la ejecución de [sp_helparticle](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md).  
  
## <a name="valid-schema-options"></a>Opciones de esquema válidas  
 La tabla siguiente describen los valores permitidos de *schema_option* basado en el tipo de replicación (se muestra en la parte superior) y el tipo de artículo (que se muestra la primera columna).  
  
|Tipo de artículo|Tipo de replicación||  
|------------------|----------------------|------|  
||Transaccional|Snapshot|  
|**logbased**|Todas las opciones|Todas las opciones, pero **0 x 02**|  
|**logbased manualfilter**|Todas las opciones|Todas las opciones, pero **0 x 02**|  
|**logbased manualview**|Todas las opciones|Todas las opciones, pero **0 x 02**|  
|**logbased vista indizada**|Todas las opciones|Todas las opciones, pero **0 x 02**|  
|**vista indizada logbased manualfilter**|Todas las opciones|Todas las opciones, pero **0 x 02**|  
|**vista indizada logbased manualview**|Todas las opciones|Todas las opciones, pero **0 x 02**|  
|**vista indizada base logarítmica manualboth**|Todas las opciones|Todas las opciones, pero **0 x 02**|  
|**proc exec**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|  
|**serializable proc exec**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|  
|**solo esquema de procedimiento**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|  
|**solo esquema de vista**|**0 x 01**, **0 x 010**, **0 x 020**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 100000**, **0x200000**, **0 x 400000**, **0 x 800000**,  **0x2000000**, **0 x 8000000**, **0 x 40000000**, y **0 x 80000000**|**0 x 01**, **0 x 010**, **0 x 020**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 100000**, **0x200000**, **0 x 400000**, **0 x 800000**,  **0x2000000**, **0 x 8000000**, **0 x 40000000**, y **0 x 80000000**|  
|**solo esquema Func**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|**0 x 01**, **0 x 20**, **0 x 2000**, **0 x 400000**, **0 x 800000**, **0x2000000**, **0 x 8000000**, **0 x 10000000**, **0 x 20000000**, **0 x 40000000**, y **0 x 80000000**|  
|**solo esquema de vista indizada**|**0 x 01**, **0 x 010**, **0 x 020**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 100000**, **0x200000**, **0 x 400000**, **0 x 800000**,  **0x2000000**, **0 x 8000000**, **0 x 40000000**, y **0 x 80000000**|**0 x 01**, **0 x 010**, **0 x 020**, **0 x 040**, **0 x 0100**, **0 x 2000**, **0 x 40000**, **0 x 100000**, **0x200000**, **0 x 400000**, **0 x 800000**,  **0x2000000**, **0 x 8000000**, **0 x 40000000**, y **0 x 80000000**|  
  
> [!NOTE]
>  Para las publicaciones de actualización en cola, el *schema_option* valor **0 x 80** debe estar habilitada. Admitidos *schema_option* valores para que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicaciones son: **0 x 01**, **0 x 02**, **0 x 10**, **0 x 40**, **0 x 80**, **0 x 1000** y  **0 x 4000**.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_changetranarticle](../../relational-databases/replication/codesnippet/tsql/sp-changearticle-transac_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_changearticle**.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del artículo](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)  
  
  
