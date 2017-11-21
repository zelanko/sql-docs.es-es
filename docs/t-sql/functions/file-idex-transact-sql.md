---
title: FILE_IDEX (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FILE_IDEX
- FILE_IDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILE_IDEX function
- IDs [SQL Server], files
- file IDs [SQL Server]
- names [SQL Server], files
- identification numbers [SQL Server], files
- file names [SQL Server], FILE_IDEX
ms.assetid: 7532fea5-ee5e-4edd-b98b-111a7ba56c8e
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 9a65a49a1e6d8c23a28b117fc90b0276ce185556
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="fileidex-transact-sql"></a>FILE_IDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Devuelve el número de identificación del archivo (Id.) para el nombre del archivo lógico de datos, registro o texto completo de la base de datos actual.  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
FILE_IDEX ( file_name )  
```  
  
## <a name="arguments"></a>Argumentos  
 *file_name*  
 Es una expresión de tipo **sysname** que representa el nombre del archivo para el que se va a devolver el identificador de archivo.  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
 **NULL** en caso de error  
  
## <a name="remarks"></a>Comentarios  
 *file_name* se corresponde con el nombre de archivo lógico mostrado en el **nombre** columna en el [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) o [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) vistas de catálogo.  
  
 FILE_IDEX se puede utilizar en una lista de selección, en una cláusula WHERE o en cualquier lugar en el que se permita una expresión. Para obtener más información, vea [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-retrieving-the-file-id-of-a-specified-file"></a>A. Recuperar el Id. de archivo de un archivo especificado  
El siguiente ejemplo devuelve el Id. de archivo para el archivo `AdventureWorks_Data`.  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX('AdventureWorks2012_Data') AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
1  
(1 row(s) affected)  
```  
  
### <a name="b-retrieving-the-file-id-when-the-file-name-is-not-known"></a>B. Recuperar el Id. de archivo cuando se desconoce el nombre del archivo  
En el ejemplo siguiente se devuelve el identificador de archivo de la `AdventureWorks` archivo de registro, seleccione el nombre de archivo lógico de la `sys.database_files` donde el tipo de archivo es igual a la vista de catálogo `1` (registro).  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX((SELECT TOP (1) name FROM sys.database_files WHERE type = 1)) AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
2  
```  
  
### <a name="c-retrieving-the-file-id-of-a-full-text-catalog-file"></a>C. Recuperar el Id. de archivo de un archivo de catálogo de texto completo  
En el ejemplo siguiente se devuelve el identificador de archivo de un archivo de texto completo seleccionando el nombre de archivo lógico de la `sys.database_files` donde el tipo de archivo es igual a la vista de catálogo `4` (texto). En este ejemplo se devuelve NULL si no existe ningún catálogo de texto completo.  
  
```tsql  
SELECT FILE_IDEX((SELECT name FROM sys.master_files WHERE type = 4))  
AS 'File_ID';  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de metadatos &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  

