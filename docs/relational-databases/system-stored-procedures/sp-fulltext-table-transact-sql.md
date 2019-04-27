---
title: sp_fulltext_table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_table_TSQL
- sp_fulltext_table
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_table
ms.assetid: a765f311-07fc-4af3-b74c-e9a027fbecce
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 340d50725a13da4993ade63d890f2300ba38763b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743996"
---
# <a name="spfulltexttable-transact-sql"></a>sp_fulltext_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Marca o quita la marca de una tabla para la indización de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md), [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)y [DROP FULLTEXT INDEX](../../t-sql/statements/drop-fulltext-index-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_fulltext_table   
   [ @tabname= ] 'qualified_table_name'           
   , [ @action= ] 'action'   
   [   
   , [ @ftcat= ] 'fulltext_catalog_name'           
   , [ @keyname= ] 'unique_index_name'   
   ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @tabname = ] 'qualified_table_name'` Es un nombre de tabla de una o dos partes. La tabla debe existir en la base de datos actual. *qualified_table_name* es **nvarchar (517)**, no tiene ningún valor predeterminado.  
  
`[ @action = ] 'action'` Es la acción que se realizará. *acción* es **nvarchar (50)**, no tiene ningún valor predeterminado y puede ser uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Crear**|Crea los metadatos para un índice de texto completo para la tabla al que hace referencia *qualified_table_name* y especifica que los datos del índice de texto completo para esta tabla deben residir en *fulltext_catalog_name*. Esta acción también designa el uso de *unique_index_name* como columna de clave de texto completo. Este índice único ya debe estar presente y debe estar definido en una columna de la tabla.<br /><br /> No se puede realizar ninguna búsqueda de texto completo sobre esta tabla hasta que se rellene el catálogo de texto completo.|  
|**Drop**|Quita los metadatos del índice de texto completo para *qualified_table_name*. Si el índice de texto completo está activo, se desactiva automáticamente antes de quitarlo. No es necesario quitar columnas antes de quitar el índice de texto completo.|  
|**Activate**|Activa la capacidad de los datos de índice de texto completo se recopilen para *qualified_table_name*, una vez que se ha desactivado. Debe haber al menos una columna que participe en el índice de texto completo antes de que se pueda activar.<br /><br /> Un índice de texto completo se convierte automáticamente en activo para su rellenado en el momento en que se agrega la primera columna para la indización. Si se quita la última columna del índice, éste se desactiva. Si está en proceso un seguimiento de cambios, al activar un índice inactivo se inicia otro rellenado.<br /><br /> Tenga en cuenta que esto no realmente rellenar el índice de texto completo, sino que simplemente registra en la tabla en el catálogo de texto completo en el sistema de archivos para que las filas de *qualified_table_name* se puede recuperar durante el siguiente índice de texto completo rellenado.|  
|**Desactivar**|Desactiva el índice de texto completo para *qualified_table_name* para que ya no se pueden recopilar datos de índice de texto completo para la *qualified_table_name*. Los metadatos del índice de texto completo permanecen y se puede volver a activar la tabla.<br /><br /> Si está activo el seguimiento de cambios, desactivar un índice activo inmoviliza el estado del índice: se detiene cualquier rellenado en curso y no se propagan más cambios al índice.|  
|**start_change_tracking**|Inicia un rellenado incremental del índice de texto completo. Si la tabla no incluye marca de tiempo, inicia un rellenado completo del índice de texto completo. Inicia un seguimiento de cambios en la tabla.<br /><br /> Seguimiento de cambios de texto completo no realiza un seguimiento de las operaciones WRITETEXT o UPDATETEXT realizadas en las columnas indizadas de texto completo del tipo **imagen**, **texto**, o **ntext**.|  
|**stop_change_tracking**|Detiene el seguimiento de cambios en la tabla.|  
|**update_index**|Propaga el conjunto actual de cambios de los que se ha realizado el seguimiento al índice de texto completo.|  
|**start_background_updateindex**|Comienza a propagar los cambios de los que se ha realizado el seguimiento al índice de texto completo mientras se producen.|  
|**stop_background_updateindex**|Detiene la propagación de los cambios de los que se ha realizado el seguimiento al índice de texto completo mientras se producen.|  
|**start_full**|Inicia un rellenado completo del índice de texto completo de la tabla.|  
|**start_incremental**|Inicia un rellenado incremental del índice de texto completo de la tabla.|  
|**Detener**|Detiene un rellenado completo o incremental.|  
  
`[ @ftcat = ] 'fulltext_catalog_name'` Es un nombre válido y catálogo de texto completo para una **crear** acción. Para todas las demás acciones, este parámetro debe ser NULL. *fulltext_catalog_name* es **sysname**, su valor predeterminado es null.  
  
`[ @keyname = ] 'unique_index_name'` Es un índice no válido de columna de clave única, único en *qualified_table_name* para un **crear** acción. Para todas las demás acciones, este parámetro debe ser NULL. *unique_index_name* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Después de desactiva un índice de texto completo para una tabla determinada, el índice de texto completo existente permanece vigente hasta el siguiente llenado completo Sin embargo, no se usa este índice porque [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bloquea las consultas sobre tablas desactivadas.  
  
 Si se vuelve a activar la tabla y no se vuelve a llenar el índice, el índice antiguo sigue disponible para las consultas que se realizan sobre las columnas restantes habilitadas para texto completo, pero no sobre las nuevas. Las consultas que especifican una búsqueda en todas las columnas de texto completo encuentran datos de columnas eliminadas.  
  
 Después de una tabla se ha definido para la indización de texto completo, cambiar el texto columna de clave única de un tipo de datos a otro, ya sea cambiando el tipo de datos de esa columna o cambiando la clave única de texto completo de una columna a otro, sin volver a llenar completamente puede producir un error que se produzca durante una consulta posterior y devolver el mensaje de error: "La conversión al tipo *data_type* error para el valor de clave de búsqueda de texto completo *key_value*." Para evitar esto, quite la definición de texto completo de esta tabla utilizando la **drop** acción de **sp_fulltext_table** y definirla con **sp_fulltext_table** y **sp_fulltext_column**.  
  
 La columna de clave de texto completo se debe definir para que tenga 900 bytes o menos. Se recomienda que el tamaño de la columna de clave sea lo más reducido posible por razones de rendimiento.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor **db_owner** y **db_ddladmin** fijo roles de base de datos o un usuario con permisos de referencia en el catálogo de texto completo se puede ejecutar **sp_fulltext_table**.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-enabling-a-table-for-full-text-indexing"></a>A. Habilitar una tabla para la indización de texto completo  
 En el ejemplo siguiente se crean los metadatos de índice de texto completo para la tabla `Document` de la base de datos `AdventureWorks`. `Cat_Desc` es un catálogo de texto completo. `PK_Document_DocumentID` es un índice único de una sola columna de `Document`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'create', 'Cat_Desc', 'PK_Document_DocumentID';  
--Add some columns  
EXEC sp_fulltext_column 'Production.Document','DocumentSummary','add';  
-- Activate the full-text index  
EXEC sp_fulltext_table 'Production.Document','activate';  
GO  
```  
  
### <a name="b-activating-and-propagating-track-changes"></a>b. Activar y propagar los cambios de los que se ha realizado un seguimiento  
 En el ejemplo siguiente se activan y comienzan a propagar los cambios de los que se ha hecho un seguimiento al índice de texto completo mientras se producen.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'Start_change_tracking';  
EXEC sp_fulltext_table 'Production.Document', 'Start_background_updateindex';  
GO  
```  
  
### <a name="c-removing-a-full-text-index"></a>C. Quitar un índice de texto completo.  
 En este ejemplo se quitan los metadatos de índice de texto completo de la tabla `Document` de la base de datos `AdventureWorks`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'drop';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_help_fulltext_tables &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [sp_helpindex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenan de búsqueda de texto completo y la búsqueda semántica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
