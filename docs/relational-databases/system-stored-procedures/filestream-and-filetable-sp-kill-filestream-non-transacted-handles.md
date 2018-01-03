---
title: sp_kill_filestream_non_transacted_handles (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_kill_filestream_non_transacted_handles_TSQL
- sp_kill_filestream_non_transacted_handles
dev_langs: TSQL
helpviewer_keywords: sp_kill_filestream_non_transacted_handles
ms.assetid: 7188353e-ab29-49a0-8f25-7fb8ab122589
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d06550f0a9cd322e26acfa8f29890833c15f947
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="filestream-and-filetable---spkillfilestreamnontransactedhandles"></a>FileStream y FileTable - sp_kill_filestream_non_transacted_handles
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cierra los identificadores de archivos no transaccionales para datos de FileTable.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
sp_kill_filestream_non_transacted_handles [[ @table_name = ] ‘table_name’, [[ @handle_id = ] @handle_id]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *table_name*  
 El nombre de la tabla en la que se van a cerrar los identificadores no transaccionales.  
  
 Puede pasar *table_name* sin *handle_id* para cerrar todos los identificadores no transaccionales del abiertos para la FileTable.  
  
 Puede pasar NULL para el valor de *table_name* para cerrar todos los abiertos identificadores no transaccionales para todas las FileTables en la base de datos actual. NULL es el valor predeterminado.  
  
 *handle_id*  
 El Id. opcional del identificador individual que se cerrará. Puede obtener el *handle_id* desde el [sys.dm_filestream_non_transacted_handles &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md) vista de administración dinámica. Cada Id. es único en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si especifica *handle_id*, también tiene que proporcionar un valor para *table_name*.  
  
 Puede pasar NULL para el valor de *handle_id* para cerrar todos los identificadores no transaccionales del abiertos para el objeto FileTable especificado por *table_name*. NULL es el valor predeterminado.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-set"></a>Conjunto de resultados  
 Ninguno.  
  
## <a name="general-remarks"></a>Notas generales  
 El *handle_id* requiere **sp_kill_filestream_non_transacted_handles** no está relacionado con el objeto session_id o la unidad de trabajo que se utiliza en otras **kill** comandos.  
  
 Para obtener más información, vea [Administrar FileTables](../../relational-databases/blob/manage-filetables.md).  
  
## <a name="metadata"></a>Metadatos  
 Para obtener información acerca de los identificadores de archivos no transaccionales abiertos, consulte la vista de administración dinámica [sys.dm_filestream_non_transacted_handles &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md).  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Debe tener **VIEW DATABASE STATE** permiso para obtener los identificadores de archivos desde el **sys.dm_FILESTREAM_non_transacted_handles** vista de administración dinámica y ejecutar **sp_kill_filestream_non_ transacted_handles**.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran cómo llamar a **sp_kill_filestream_non_transacted_handles** para cerrar identificadores de archivos no transaccionales para datos de FileTable.  
  
```sql  
-- Close all open handles in the current database.  
sp_kill_filestream_non_transacted_handles  
  
-- Close all open handles in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = ’myFileTable’  
  
-- Close a specific handle in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = ’myFileTable’, @handle_id = 0xFFFAAADD  
```  
  
 En el ejemplo siguiente se muestra cómo usar un script para obtener un *handle_id* y ciérrelo.  
  
```sql  
DECLARE @handle_id varbinary(16);  
DECLARE @table_name sysname;  
  
SELECT TOP 1 @handle_id = handle_id, @table_name = Object_name(table_id)  
FROM sys.dm_FILESTREAM_non_transacted_handles;  
  
EXEC sp_kill_filestream_non_transacted_handles @dbname, @table_name, @handle_id;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Administrar FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
