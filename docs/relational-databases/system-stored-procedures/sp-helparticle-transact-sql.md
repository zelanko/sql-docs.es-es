---
title: sp_helparticle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_helparticle_TSQL
- sp_helparticle
helpviewer_keywords:
- sp_helparticle
ms.assetid: 9c4a1a88-56f1-45a0-890c-941b8e0f0799
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a52ab877f72f8a050e5582756b957e5db30c0ecb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47843425"
---
# <a name="sphelparticle-transact-sql"></a>sp_helparticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información acerca de un artículo. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación. En los publicadores de Oracle, este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helparticle [ @publication = ] 'publication'   
    [ , [ @article = ] 'article' ]  
    [ , [ @returnfilter = ] returnfilter ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @found = ] found OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =**] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@article=**] **'***artículo***'**  
 Es el nombre de un artículo de la publicación. *artículo* es **sysname**, su valor predeterminado es **%**. Si *artículo* no es se proporciona, se devuelve información sobre todos los artículos de la publicación especificada.  
  
 [  **@returnfilter=**] *returnfilter*  
 Especifica si se debe devolver la cláusula de filtro. *returnfilter* es **bit**, su valor predeterminado es **1**, que devuelve la cláusula de filtro.  
  
 [ **@publisher**=] **'***publisher***'**  
 Especifica que no es[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publisher. *publicador* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *publicador* no se debe especificar al solicitar información sobre un artículo publicado por un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
 [  **@found=** ] *encuentra* salida  
 Exclusivamente para uso interno.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Id. de artículo**|**int**|ID. del artículo.|  
|**nombre de artículo**|**sysname**|Nombre del artículo.|  
|**objeto base**|**nvarchar (257)**|Nombre de la tabla subyacente representada por el artículo o el procedimiento almacenado.|  
|**objeto de destino**|**sysname**|Nombre de la tabla de destino (suscripción).|  
|**objeto de sincronización**|**nvarchar (257)**|Nombre de la vista que define el artículo publicado.|  
|**Tipo**|**smallint**|Tipo de artículo:<br /><br /> **1** = basado en registro.<br /><br /> **3** = basado en registro con filtro manual.<br /><br /> **5** = basado en registro con vista manual.<br /><br /> **7** = basado en registro con filtro manual y vista manual.<br /><br /> **8** = ejecución de procedimiento almacenado.<br /><br /> **24** = la ejecución del procedimiento almacenado serializable.<br /><br /> **32** = procedimiento almacenado (solo esquema).<br /><br /> **64** = vista (solo esquema).<br /><br /> **96** = función de agregado (solo esquema).<br /><br /> **128** = function (solo esquema).<br /><br /> **257** = vista indizada basado en registro.<br /><br /> **259** = vista indizada basado en registro con filtro manual.<br /><br /> **261** = vista indizada basado en registro con vista manual.<br /><br /> **263** = vista indizada basado en registro con filtro manual y vista manual.<br /><br /> **320** = vista indizada (solo esquema).<br /><br />|  
|**status**|**tinyint**|Puede ser el [& (AND bit a bit)](../../t-sql/language-elements/bitwise-and-transact-sql.md) resultado de una o más estas propiedades del artículo:<br /><br /> **0 x 00** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **0 x 01** = artículo está activo.<br /><br /> **0 x 08** = incluir el nombre de columna en las instrucciones insert.<br /><br /> **0 x 16** = usar instrucciones con parámetros.<br /><br /> **0 x 32** = usar instrucciones con parámetros e incluir el nombre de columna en las instrucciones insert.|  
|**filter**|**nvarchar (257)**|Procedimiento almacenado utilizado para filtrar la tabla horizontalmente. Este procedimiento almacenado debe haber sido creado mediante la cláusula FOR REPLICATION.|  
|**Descripción**|**nvarchar(255)**|Entrada descriptiva del artículo.|  
|**insert_command**|**nvarchar(255)**|El tipo de comando de replicación utilizado al replicar inserciones con artículos de la tabla. Para más información, vea [Especificar cómo se propagan los cambios para los artículos transaccionales](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**update_command**|**nvarchar(255)**|El tipo de comando de replicación utilizado al replicar actualizaciones con artículos de la tabla. Para más información, vea [Especificar cómo se propagan los cambios para los artículos transaccionales](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**delete_command**|**nvarchar(255)**|El tipo de comando de replicación utilizado al replicar eliminaciones con artículos de la tabla. Para más información, vea [Especificar cómo se propagan los cambios para los artículos transaccionales](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**ruta de acceso de script de creación**|**nvarchar(255)**|Ruta de acceso y nombre de un script de esquema del artículo que se utiliza para crear tablas de destino.|  
|**Particionamiento vertical**|**bit**|Es si está habilitado el particionamiento vertical para el artículo; el valor **1** significa que está habilitado el particionamiento vertical.|  
|**pre_creation_cmd**|**tinyint**|Comando anterior a la creación para DROP TABLE, DELETE TABLE o TRUNCATE TABLE.|  
|**filter_clause**|**ntext**|Cláusula WHERE que especifica el filtrado horizontal.|  
|**schema_option**|**binary (8)**|Mapa de bits de la opción de generación del esquema para el artículo dado. Para obtener una lista completa de **schema_option** valores, vea [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**sysname**|Nombre del propietario del objeto de destino.|  
|**source_owner**|**sysname**|Propietario del objeto de origen.|  
|**unqua_source_object**|**sysname**|Nombre del objeto de origen, sin el nombre del propietario.|  
|**sync_object_owner**|**sysname**|Propietario de la vista que define el artículo publicado .|  
|**unqualified_sync_object**|**sysname**|Nombre de la vista que define el artículo publicado, sin el nombre del propietario.|  
|**filter_owner**|**sysname**|Propietario del filtro.|  
|**unqua_filter**|**sysname**|Nombre del filtro, sin el nombre del propietario.|  
|**auto_identity_range**|**int**|Marca que establece si se activó el control automático del intervalo de identidad en la publicación en el momento en que se creó. **1** significa que el intervalo de identidad automático está habilitado; **0** significa que está deshabilitado.|  
|**publisher_identity_range**|**int**|Rango de tamaño del intervalo de identidad en el publicador si el artículo tiene *identityrangemanagementoption* establecido en **automática** o **auto_identity_range** establecido en  **True**.|  
|**identity_range**|**bigint**|Rango de tamaño del intervalo de identidad en el suscriptor si el artículo tiene *identityrangemanagementoption* establecido en **automática** o **auto_identity_range** establecido en  **True**.|  
|**umbral**|**bigint**|Valor de porcentaje que indica cuándo asigna el Agente de distribución un nuevo intervalo de identidad.|  
|**valor de identityrangemanagementoption**|**int**|Indica la administración de intervalos de identidad controlada del artículo.|  
|**fire_triggers_on_snapshot**|**bit**|Indica si se ejecutan desencadenadores de usuario replicados al aplicar la instantánea inicial.<br /><br /> **1** = se ejecutan desencadenadores de usuario.<br /><br /> **0** = no se ejecutan desencadenadores de usuario.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helparticle** se utiliza en la replicación de instantáneas y transaccional.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor, el **db_owner** rol fijo de base de datos o la lista de acceso de publicación para la publicación actual puede ejecutar **sp_helparticle**.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_helptranarticle](../../relational-databases/replication/codesnippet/tsql/sp-helparticle-transact-_1.sql)]  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del artículo](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
