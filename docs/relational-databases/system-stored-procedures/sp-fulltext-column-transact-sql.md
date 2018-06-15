---
title: sp_fulltext_column (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fulltext_column_TSQL
- sp_fulltext_column
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_column
ms.assetid: a84cc45d-1b50-44af-85df-2ea033b8a6a9
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6c1a53e05eef89584526846c3f3d3c6324164a94
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33259585"
---
# <a name="spfulltextcolumn-transact-sql"></a>sp_fulltext_column (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Especifica si una columna concreta de una tabla participa en la indización de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_fulltext_column [ @tabname= ] 'qualified_table_name' ,   
     [ @colname= ] 'column_name' ,   
     [ @action= ] 'action'   
     [ , [ @language= ] 'language_term' ]   
     [ , [ @type_colname= ] 'type_column_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@tabname=** ] **'***qualified_table_name***'**  
 Se trata de un nombre de tabla con una o dos partes. La tabla debe existir en la base de datos actual. La tabla debe tener un índice de texto completo. *qualified_table_name* es **nvarchar (517)**, sin valor predeterminado.  
  
 [  **@colname=** ] **'***column_name***'**  
 Es el nombre de una columna en *qualified_table_name*. La columna debe ser un carácter, **varbinary (max)** o **imagen** columna y no puede ser una columna calculada. *column_name* es **sysname**, no tiene ningún valor predeterminado.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede crear índices de texto completo de datos de texto almacenados en las columnas de **varbinary (max)** o **imagen** tipo de datos. Las imágenes no se indizan.  
  
 [  **@action=** ] **'***acción***'**  
 Se trata de la acción que se va a realizar. *acción* es **varchar (20)**, no tiene ningún valor predeterminado y puede ser uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**Agregar**|Agrega *column_name* de *qualified_table_name* al índice de texto completo inactivo de la tabla. Esta acción habilita el indizado de texto completo de la columna.|  
|**quitar**|Quita *column_name* de *qualified_table_name* de índice de texto completo inactivo de la tabla.|  
  
 [  **@language=** ] **'***language_term***'**  
 Se trata del idioma de los datos almacenados en la columna. Para obtener una lista de los idiomas incluidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
> [!NOTE]  
>  Use 'Neutral' cuando una columna contiene datos en varios idiomas o en un idioma no admitido. El valor predeterminado se especifica en la opción de configuración 'default full-text language'.  
  
 [  **@type_colname =** ] **'***type_column_name***'**  
 Es el nombre de una columna en *qualified_table_name* que contiene el tipo de documento de *column_name*. Esta columna debe ser **char**, **nchar**, **varchar**, o **nvarchar**. Solo se usa cuando el tipo de datos de *column_name* es de tipo **varbinary (max)** o **imagen**. *type_column_name* es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Si el índice de texto completo está activo, se detiene cualquier llenado en proceso. Además, si una tabla con un índice de texto completo activo tiene habilitado el seguimiento de cambios, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] garantiza que el índice está actualizado. Por ejemplo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detiene cualquier llenado actual de la tabla, quita el índice existente e inicia un nuevo llenado.  
  
 Si está activado el seguimiento de cambios y es necesario agregar o quitar columnas del índice de texto completo sin eliminar éste, la tabla se tiene que desactivar y las columnas apropiadas se tienen que agregar o quitar. Estas acciones bloquean el índice. Se puede activar la tabla más adelante, cuando sea más práctico iniciar un llenado.  
  
## <a name="permissions"></a>Permissions  
 Usuario debe ser un miembro de la **db_ddladmin** rol fijo de base de datos o un miembro de la **db_owner** rol fijo de base de datos o el propietario de la tabla.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se agrega la columna `DocumentSummary` de la tabla `Document` al índice de texto completo de la tabla.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_column 'Production.Document', DocumentSummary, 'add';  
GO  
```  
  
 El ejemplo presupone que ha creado un índice de texto completo en una tabla denominada `spanishTbl`. Para agregar la columna `spanishCol` al índice de texto completo, ejecute el siguiente procedimiento almacenado:   
  
```  
EXEC sp_fulltext_column 'spanishTbl', 'spanishCol', 'add', 0xC0A;  
GO  
```  
  
 Al ejecutar esta consulta:  
  
```  
SELECT *   
FROM spanishTbl   
WHERE CONTAINS(spanishCol, 'formsof(inflectional, trabajar)')  
```  
  
 El conjunto de resultados incluiría filas con diferentes formas de `trabajar`, como `trabajo`, `trabajamos` y `trabajan`.  
  
> [!NOTE]  
>  Todas las columnas mostradas en una única cláusula de función para consulta de texto completo deben usar el mismo idioma.  
  
## <a name="see-also"></a>Vea también  
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_help_fulltext_columns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)   
 [sp_help_fulltext_columns_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [sp_help_fulltext_tables &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenan de búsqueda de texto completo y la búsqueda semántica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
