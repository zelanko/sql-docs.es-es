---
title: sp_syscollector_update_collection_item (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collection_item
- sp_syscollector_update_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_update_collection_item
ms.assetid: 7a0d36c8-c6e9-431d-a5a4-6c1802bce846
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 07a19b6f4d3d80c615bc1193f3b8af9950c97f96
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spsyscollectorupdatecollectionitem-transact-sql"></a>sp_syscollector_update_collection_item (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Se usa para modificar las propiedades de un elemento de recopilación definido por el usuario o para cambiar el nombre de un elemento de recopilación definido por el usuario.  
  
 
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syscollector_update_collection_item   
      [ [ @collection_item_id = ] collection_item_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @new_name = ] 'new_name' ]  
    , [ [ @frequency = ] frequency ]  
    , [ [ @parameters = ] 'parameters' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @collection_item_id =] *collection_item_id*  
 Es el identifer único que identifica el elemento de recopilación. *collection_item_id* es **int** con un valor predeterminado es NULL. *collection_item_id* debe tener un valor si *nombre* es NULL.  
  
 [ @name =] '*nombre*'  
 Es el nombre del elemento de colección. *nombre* es **sysname** con un valor predeterminado es NULL. *nombre* debe tener un valor si *collection_item_id* es NULL.  
  
 [ @new_name =] '*new_name*'  
 Es el nuevo nombre del elemento de recopilación. *new_name* es **sysname**, y si se utiliza, no puede ser una cadena vacía.  
  
 *new_name* deben ser únicos. Para obtener una lista de los nombres de elementos de recopilación actuales, consulte la vista del sistema syscollector_collection_items.  
  
 [ @frequency =] *frecuencia*  
 Es la frecuencia (en segundos) con que este elemento de recopilación recopila los datos. *frecuencia* es **int**, su valor predeterminado es 5, el valor mínimo que se pueden especificar.  
  
 [ @parameters =] '*parámetros*'  
 Parámetros de entrada para el elemento de recopilación. *parámetros de* es **xml** con un valor predeterminado es NULL. El *parámetros* esquema debe coincidir con el esquema de parámetros del tipo de recopilador.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Si el conjunto de recopilación se establece en modo sin almacenamiento en caché, se omite el cambio de la frecuencia porque este modo hace que la recopilación de datos y la carga se produzcan en la programación especificada para el conjunto de recopilación. Para ver el estado del conjunto de recopilación, ejecute la consulta siguiente. Reemplace `<collection_item_id>` con el identificador del elemento de recopilación que se va a actualizar.  
  
```  
USE msdb;  
GO  
SELECT cs.collection_set_id, collection_set_uid, cs.name   
    ,'is running' = CASE WHEN is_running =  0 THEN 'No' ELSE 'Yes' END  
    ,'cache mode' = CASE WHEN collection_mode = 0 THEN 'Cached mode' ELSE 'Non-cached mode' END  
FROM syscollector_collection_sets AS cs  
JOIN syscollector_collection_items AS ci   
ON ci.collection_set_id = cs.collection_set_id  
WHERE collection_item_id = <collection_item_id>;  
```  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia a un rol fijo de base de datos dc_admin o dc_operator (con permiso EXECUTE) para ejecutar este procedimiento. Aunque dc_operator puede ejecutar este procedimiento almacenado, las propiedades que pueden cambiar los miembros de este rol son limitadas. Las propiedades siguientes solo puede cambiarlas dc_admin:  
  
-   @new_name  
  
-   @parameters  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes se basan en el elemento de colección creado en el ejemplo definido en [sp_syscollector_create_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md).  
  
### <a name="a-changing-the-collection-frequency"></a>A. Cambiar la frecuencia de la recopilación  
 En el ejemplo siguiente se cambia la frecuencia de recopilación para el elemento de recopilación especificado.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@frequency = 3000;  
GO  
```  
  
### <a name="b-renaming-a-collection-item"></a>B. Cambiar el nombre de un elemento de recopilación  
 En el ejemplo siguiente se cambia el nombre de un elemento de recopilación.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@new_name = N'My modified TSQL item';  
GO  
```  
  
### <a name="c-changing-the-parameters-of-a-collection-item"></a>C. Cambiar los parámetros de un elemento de recopilación  
 En el ejemplo siguiente se cambian los parámetros asociados al elemento de recopilación. Se cambia la instrucción definida dentro del atributo `<Value>` y el atributo `UseSystemDatabases` está establecido en false. Para ver los parámetros actuales para este elemento, consulte la columna de parámetros en la vista del sistema syscollector_collection_items. Puede que necesite modificar el valor de `@collection_item_id`.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@collection_item_id = 9,   
@parameters = '  
    \<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
        <Query>  
            <Value>SELECT * FROM sys.dm_db_index_usage_stats</Value>  
            <OutputTable>MyOutputTable</OutputTable>  
        </Query>  
        <Databases>  
            <Database> UseSystemDatabases = "false"   
                       UseUserDatabases = "true"</Database>  
        </Databases>  
    \</ns:TSQLQueryCollector>';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_create_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)   
 [syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
