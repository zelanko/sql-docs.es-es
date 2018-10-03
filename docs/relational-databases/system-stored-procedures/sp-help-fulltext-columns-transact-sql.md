---
title: sp_help_fulltext_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_columns
- sp_help_fulltext_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_columns
ms.assetid: 92c8656b-f7fd-4904-9796-acc9ffed4106
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0ad479171b0fc2bf252b9f12a8b993fa7b69baa6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47630579"
---
# <a name="sphelpfulltextcolumns-transact-sql"></a>sp_help_fulltext_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve las columnas diseñadas para la indización de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use la [sys.fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) vista de catálogo en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_fulltext_columns [ [ @table_name = ] 'table_name' ] ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@table_name=**] **'***table_name***'**  
 Es el nombre de tabla de una o dos partes para la que se solicita información de índice de texto completo. *table_name* es **nvarchar (517)**, su valor predeterminado es null. Si *table_name* se omite, se recupera información de columna de índice de texto completo para cada tabla indizada de texto completo.  
  
 [  **@column_name=**] **'***column_name***'**  
 Es el nombre de la columna cuyos metadatos de índice de texto completo se solicitan. *column_name* es **sysname**, su valor predeterminado es null. Si *column_name* se omite o es NULL, se devuelve información de columna de texto completo para cada columna de índice de texto completo para *table_name*. Si *table_name* también se omite o es NULL, se devuelve información de columna de índice de texto completo para cada columna de índice de texto completo de todas las tablas de la base de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|Propietario de la tabla. Es el nombre del usuario de la base de datos que ha creado la tabla.|  
|**TABLE_ID**|**int**|Id. de la tabla.|  
|**TABLE_NAME**|**sysname**|Nombre de la tabla.|  
|**FULLTEXT_COLUMN_NAME**|**sysname**|Columna de una tabla con índice de texto completo que está designada para su indización.|  
|**FULLTEXT_COLID**|**int**|Id. de columna de la columna de índice de texto completo.|  
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|Columna de una tabla con índice de texto completo que especifica el tipo de documento de la columna de índice de texto completo. Este valor solo es aplicable cuando la columna indizada de texto completo es un **varbinary (max)** o **imagen** columna.|  
|**FULLTEXT_BLOBTP_COLID**|**int**|Id. de la columna de tipo de documento. Este valor solo es aplicable cuando la columna indizada de texto completo es un **varbinary (max)** o **imagen** columna.|  
|**FULLTEXT_LANGUAGE**|**sysname**|Lenguaje utilizado para la búsqueda de texto completo de la columna.|  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los permisos de ejecución corresponden a los miembros del rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 Este ejemplo devuelve información acerca de las columnas que se han designado para la indización de texto completo en la tabla `Document`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_columns 'Production.Document';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
