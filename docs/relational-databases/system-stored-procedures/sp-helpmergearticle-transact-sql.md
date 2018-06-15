---
title: sp_helpmergearticle (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_helpmergearticle
- sp_helpmergearticle_TSQL
helpviewer_keywords:
- sp_helpmergearticle
ms.assetid: 0fb9986a-3c33-46ef-87bb-297396ea5a6a
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 46c8751290a1e5c08cb2f77a458aae252ec903c2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33003122"
---
# <a name="sphelpmergearticle-transact-sql"></a>sp_helpmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información acerca de un artículo. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicaciones o en el suscriptor de republicaciones de la base de datos de suscripciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpmergearticle [ [ @publication = ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación de la que se devuelve información. *publicación*es **sysname**, su valor predeterminado es **%**, que devuelve información acerca de todos los artículos de mezcla contenidos en todas las publicaciones de la base de datos actual.  
  
 [  **@article=**] **'***artículo***'**  
 Es el nombre del artículo del que se devuelve información. *artículo*es **sysname**, su valor predeterminado es **%**, que devuelve información acerca de todos los artículos de mezcla de la publicación indicada.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identificador del artículo.|  
|**Nombre**|**sysname**|Nombre del artículo.|  
|**source_owner**|**sysname**|Nombre del propietario del objeto de origen.|  
|**source_object**|**sysname**|Nombre del objeto de origen desde el que se agrega el artículo.|  
|**sync_object_owner**|**sysname**|Nombre del propietario de la vista que define el artículo publicado.|  
|**sync_object**|**sysname**|Nombre del objeto personalizado que se utiliza para establecer los datos iniciales de la partición|  
|**Descripción**|**nvarchar(255)**|Descripción del artículo.|  
|**status**|**tinyint**|Estado del artículo, que puede ser uno de los siguientes:<br /><br /> **1** = inactivo<br /><br /> **2** = activo<br /><br /> **5** = operación pendiente (DDL) de lenguaje de definición de datos<br /><br /> **6** = operación DDL con una instantánea recién generada<br /><br /> Nota: Cuando se reinicializa un artículo, los valores de **5** y **6** se cambian a **2**.|  
|**creation_script**|**nvarchar(255)**|Ruta de acceso y nombre de un script opcional del esquema del artículo que se utiliza para crear el artículo en la base de datos de suscripciones.|  
|**conflict_table**|**nvarchar(270)**|Nombre de la tabla que almacena los conflictos de inserción o actualización.|  
|**article_resolver**|**nvarchar(255)**|Solucionador personalizado para el artículo.|  
|**subset_filterclause**|**nvarchar(1000)**|Cláusula WHERE que especifica el filtrado horizontal.|  
|**pre_creation_command**|**tinyint**|Método anterior a la creación, que puede ser uno de los siguientes:<br /><br /> **0** = ninguno<br /><br /> **1** = quitar<br /><br /> **2** = eliminar<br /><br /> **3** = truncar|  
|**schema_option**|**binary (8)**|Mapa de bits de la opción de generación de esquema para el artículo. Para obtener información acerca de esta opción de mapa de bits, consulte [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) o [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md).|  
|**Tipo**|**smallint**|Tipo de artículo, que puede ser uno de los siguientes:<br /><br /> **10** = tabla<br /><br /> **32** = procedimiento almacenado<br /><br /> **64** = vista o vista indizada<br /><br /> **128** = función definida por el usuario<br /><br /> **160** = solamente esquema de sinónimo|  
|**column_tracking**|**int**|Configuración para el seguimiento de nivel de columna; donde **1** significa que el seguimiento de nivel de columna es on, y **0** significa que el seguimiento de nivel de columna está desactivado.|  
|**resolver_info**|**nvarchar(255)**|Nombre del solucionador del artículo.|  
|**vertical_partition**|**bit**|Si el artículo está dividido verticalmente; donde **1** significa que el artículo está dividido verticalmente y **0** significa que no se encuentra.|  
|**destination_owner**|**sysname**|Propietario del objeto de destino. Aplicable únicamente a procedimientos almacenados de mezcla, vistas y artículos de esquema de funciones definidas por el usuario (UDF).|  
|**identity_support**|**int**|Si está habilitado el control de intervalo de identidad automática; donde **1** está habilitada y **0** está deshabilitado.|  
|**pub_identity_range**|**bigint**|Tamaño del intervalo que se va a utilizar al asignar nuevos valores de identidad. Para obtener más información, vea la sección "Replicación de mezcla" de [replicar las columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**identity_range**|**bigint**|Tamaño del intervalo que se va a utilizar al asignar nuevos valores de identidad. Para obtener más información, vea la sección "Replicación de mezcla" de [replicar las columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**Umbral**|**int**|Valor de porcentaje utilizado para los suscriptores que ejecuten [!INCLUDE[ssEW](../../includes/ssew-md.md)] o versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **umbral** controla cuándo el agente de mezcla asigna un nuevo intervalo de identidad. Si se utiliza el porcentaje de valores especificado en el umbral, el Agente de mezcla crea un nuevo intervalo de identidad. Para obtener más información, vea la sección "Replicación de mezcla" de [replicar las columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**verify_resolver_signature**|**int**|Si una firma digital se comprueba antes de utilizar a un solucionador en la replicación de mezcla; donde **0** significa que no se comprueba la firma, y **1** significa que la firma se comprueba para ver si proviene de un origen de confianza.|  
|**destination_object**|**sysname**|Nombre del objeto de destino. Aplicable únicamente a procedimientos almacenados de mezcla, vistas y artículos de esquema UDF.|  
|**allow_interactive_resolver**|**int**|Si se utiliza el solucionador interactivo en un artículo; donde **1** significa que se utiliza este solucionador y **0** significa que no se utiliza.|  
|**fast_multicol_updateproc**|**int**|Habilita o deshabilita el agente de mezcla para aplicar cambios a varias columnas de la misma fila en una instrucción UPDATE; donde **1** significa que se actualizan varias columnas en una sola instrucción, y **0** significa que separan las instrucciones de actualización es problemas de todas las filas actualizadas.|  
|**check_permissions**|**int**|Valor entero que representa el mapa de bits de los permisos de tabla que se comprueban. Para obtener una lista de valores posibles, consulte [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**processing_order**|**int**|Orden en que se aplican los cambios de datos a los artículos de una publicación.|  
|**upload_options**|**tinyint**|Define las restricciones impuestas a las actualizaciones realizadas en un suscriptor con suscripción de cliente. Pueden tener uno de estos valores:<br /><br /> **0** = no hay restricciones respecto a las actualizaciones realizadas en el suscriptor con una suscripción de cliente; todos los cambios se cargan en el publicador.<br /><br /> **1** = se permiten realizar cambios en el suscriptor con una suscripción de cliente, pero no se cargan en el publicador.<br /><br /> **2** = no se permiten cambios en el suscriptor con una suscripción de cliente.<br /><br /> Para obtener más información, vea [Optimize Merge Replication Performance with Download-Only Articles](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md) (Optimizar el rendimiento de la replicación de mezcla con artículos de solo descarga).|  
|**valor de identityrangemanagementoption**|**int**|Si está habilitado el control de intervalo de identidad automática; donde **1** está habilitada y **0** está deshabilitado.|  
|**delete_tracking**|**bit**|Si las eliminaciones se replican; donde **1** significa que las eliminaciones se replican y **0** significa que no lo son.|  
|**compensate_for_errors**|**bit**|Indica si se realizan las acciones de compensación cuando se producen errores durante la sincronización; donde **1** indica que se realizan las acciones de compensación, y **0** significa que no se realizan las acciones de compensación.|  
|**partition_options**|**tinyint**|Define el modo en el que se realiza la partición de los datos en el artículo, lo que permite optimizaciones de rendimiento cuando todas las filas pertenecen solamente a una partición o solamente a una suscripción. *partition_options* puede ser uno de los siguientes valores.<br /><br /> **0** = el filtro para el artículo es estático o no produce un único subconjunto de datos para cada partición; es decir, es una partición "superpuesta".<br /><br /> **1** = las particiones se superponen y actualizaciones de lenguaje (DML) de manipulación de datos realizadas en el suscriptor no pueden cambiar la partición a la que pertenece una fila.<br /><br /> **2** = el filtro del artículo produce particiones no superpuestas, pero varios suscriptores pueden recibir la misma partición.<br /><br /> **3** = el filtro del artículo produce particiones no superpuestas que son únicas para cada suscripción.|  
|**artid**|**uniqueidentifier**|Identificador que identifica el artículo de manera exclusiva.|  
|**pubid**|**uniqueidentifier**|Identificador que identifica de manera exclusiva la publicación en la que se publica el artículo.|  
|**stream_blob_columns**|**bit**|Indica si se utiliza la optimización del flujo de datos al replicar columnas de objetos binarios grandes. **1** significa que se utiliza la optimización, y **0** significa que no se utiliza la optimización.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpmergearticle** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **db_owner** fijo de base de datos en la base de datos de publicación, la **replmonitor** en la base de datos de distribución o de la lista de acceso de publicación para una publicación pueden ejecutar **sp_helpmergearticle**.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_helpmergearticle](../../relational-databases/replication/codesnippet/tsql/sp-helpmergearticle-tran_1.sql)]  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del artículo](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
