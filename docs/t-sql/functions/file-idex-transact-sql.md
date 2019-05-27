---
title: FILE_IDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 44cb6fa7f32616f7a1616c334c438b7a752546e3
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65946053"
---
# <a name="fileidex-transact-sql"></a>FILE_IDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Esta función devuelve el número de identificación del archivo (id.) para el nombre lógico especificado de un archivo de datos, registro o texto completo de la base de datos actual. 
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
FILE_IDEX ( file_name )  
```  
  
## <a name="arguments"></a>Argumentos  
 *file_name*  
Una expresión de tipo **sysname** que devuelve el valor de id. de archivo "FILE_IDEX" del nombre del archivo. 
  
## <a name="return-types"></a>Tipos devueltos  
**int**  
  
**NULL** en caso de error  
  
## <a name="remarks"></a>Notas  
*file_name* corresponde al nombre de archivo lógico mostrado en la columna **name** de las vistas de catálogo [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) o [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md).  
  
Utilice `FILE_IDEX` en una lista SELECT, en una cláusula WHERE o en cualquier lugar que admita el uso de una expresión. Para obtener más información, vea [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-retrieving-the-file-id-of-a-specified-file"></a>A. Recuperar el Id. de archivo de un archivo especificado  
Este ejemplo devuelve el id. de archivo para el archivo `AdventureWorks_Data`.  
  
```sql  
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
Este ejemplo devuelve el id. de archivo del archivo de registro `AdventureWorks`. El fragmento de código Transact-SQL (T-SQL) selecciona el nombre de archivo lógico de la vista de catálogo `sys.database_files`, donde el tipo de archivo es igual a `1` (registro).  
  
```sql  
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
Este ejemplo devuelve el id. de archivo de un archivo de texto completo. El fragmento de código T-SQL selecciona el nombre de archivo lógico de la vista de catálogo `sys.database_files`, donde el tipo de archivo es igual a `4` (texto completo). Este código devuelve "NULL" si no existe ningún catálogo de texto completo.
  
```sql  
SELECT FILE_IDEX((SELECT name FROM sys.master_files WHERE type = 4))  
AS 'File_ID';  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones de metadatos &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
