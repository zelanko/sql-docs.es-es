---
title: sp_catalogs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_catalogs_TSQL
- sp_catalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sp_catalogs
ms.assetid: ebb29ee2-be65-4e09-9c53-e3c6d12633e1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b760e27d7a0b320c0e911a1a485d1e5e9033146a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824860"
---
# <a name="sp_catalogs-transact-sql"></a>sp_catalogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve la lista de catálogos del servidor vinculado que se haya especificado. Esto equivale a las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_catalogs [ @server_name = ] 'linked_svr'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @server_name = ] 'linked_svr'`Es el nombre de un servidor vinculado. *linked_svr* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Catalog_name**|**nvarchar (** 128 **)**|Nombre del catálogo|  
|**Descripción**|**nvarchar (** 4000 **)**|Descripción del catálogo.|  
  
## <a name="permissions"></a>Permisos  
 Es necesario contar con un permiso de tipo SELECT sobre el esquema.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelve información acerca del catálogo para el servidor vinculado denominado `OLE DB ODBC Linked Server #3`.  
  
> [!NOTE]  
>  Para que **sp_catalogs** proporcione información útil, el `OLE DB ODBC Linked Server #3` ya debe existir.  
  
```  
USE master;  
GO  
EXEC sp_catalogs 'OLE DB ODBC Linked Server #3';  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_addlinkedserver &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_columns_ex &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [sp_column_privileges &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_primarykeys &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_tables_ex &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
