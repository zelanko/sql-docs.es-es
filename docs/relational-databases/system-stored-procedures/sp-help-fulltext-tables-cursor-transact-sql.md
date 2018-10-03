---
title: sp_help_fulltext_tables_cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables_cursor
- sp_help_fulltext_tables_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_tables_cursor
ms.assetid: 155791eb-8832-4596-8487-7fc70dfba5b9
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 87566a816638e38e9adbf4e2dd6ebfef1f741e3c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47852003"
---
# <a name="sphelpfulltexttablescursor-transact-sql"></a>sp_help_fulltext_tables_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Utiliza un cursor para devolver una lista de las tablas registradas para la indización de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use la nueva **sys.fulltext_indexes** vista de catálogo en su lugar. Para obtener más información, consulte [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_fulltext_tables_cursor [ @cursor_return = ] @cursor_variable OUTPUT   
     [ , [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@cursor_return=** ] *@cursor_variable* SALIDA  
 Es la variable de salida de tipo **cursor**. El cursor es desplazable, dinámico y de solo lectura.  
  
 [  **@fulltext_catalog_name=** ] **'***fulltext_catalog_name***'**  
 Es el nombre del catálogo de texto completo. *fulltext_catalog_name* es **sysname**, su valor predeterminado es null. Si *fulltext_catalog_name* se omite o es NULL, se devuelven todas las tablas indizadas de texto completo asociadas a la base de datos. Si *fulltext_catalog_name* se especifica, pero *table_name* se omite o es NULL, se recupera la información de índice de texto completo para cada tabla indizada de texto completo asociado a este catálogo. Si ambos *fulltext_catalog_name* y *table_name* se especifican, se devuelve una fila si *table_name* está asociado con *fulltext_catalog_name*; en caso contrario, se produce un error.  
  
 [  **@table_name=**] **'***table_name***'**  
 Es el nombre de tabla de una o dos partes para la que se solicitan los metadatos de texto completo. *table_name* es **nvarchar (517)**, su valor predeterminado es null. Si solo *table_name* se especifica, la fila relevante para *table_name* se devuelve.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|Propietario de la tabla. Es el nombre del usuario de la base de datos que ha creado la tabla.|  
|**TABLE_NAME**|**sysname**|Nombre de la tabla.|  
|**FULLTEXT_KEY_INDEX_NAME**|**sysname**|Índice que impone la restricción UNIQUE a la columna designada como columna de clave única.|  
|**FULLTEXT_KEY_COLID**|**int**|Id. de columna del índice único que identifica FULLTEXT_KEY_NAME.|  
|**FULLTEXT_INDEX_ACTIVE**|**int**|Especifica si las columnas de esta tabla marcadas para indización de texto completo pueden utilizarse en consultas:<br /><br /> 0 = Inactivo <br /><br /> 1 = Activo|  
|**FULLTEXT_CATALOG_NAME**|**sysname**|Catálogo de texto completo en el que residen los datos de índice de texto completo.|  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los permisos de ejecución corresponden a los miembros del rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se obtienen los nombres de las tablas con índice de texto completo asociadas al catálogo de texto completo `Cat_Desc`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_tables_cursor @mycursor OUTPUT, 'Cat_Desc';  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END;  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>Vea también  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_fulltext_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [sp_help_fulltext_tables &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
