---
title: FILE_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILE_ID
- FILE_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IDs [SQL Server], files
- file IDs [SQL Server]
- FILE_ID function
- names [SQL Server], files
- identification numbers [SQL Server], files
- file names [SQL Server], FILE_ID
ms.assetid: 6a7382cf-a360-4d62-b9d2-5d747f56f076
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 63744a6731e7c57a21a821ce7ab65cb49e095e67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071532"
---
# <a name="fileid-transact-sql"></a>FILE_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Para el nombre lógico dado de un archivo de componente de la base de datos actual, esta función devuelve el número de identificación (id.) del archivo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
FILE_ID ( file_name )  
```  
  
## <a name="arguments"></a>Argumentos  
*file_name*  
Una expresión de tipo **sysname**, que representa el nombre lógico del archivo cuyo valor de identificador de archivo `FILE_ID` va a devolver.  
  
## <a name="return-types"></a>Tipos devueltos  
**smallint**  
  
## <a name="remarks"></a>Notas  
*file_name* corresponde al nombre de archivo lógico mostrado en la columna name de las vistas de catálogo sys.master_files o sys.database_files.  

`FILE_ID` devuelve `NULL` si *file_name* no corresponde al nombre lógico de un archivo de componente de la base de datos actual.
  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el número de identificación de archivo asignado a los catálogos de texto completo excede 32767. Como la función `FILE_ID` tiene un tipo de devolución **smallint**, `FILE_ID` no admitirá los archivos de texto completo. Use [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md) en su lugar.  
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se devuelve el valor de identificador de archivo del archivo `AdventureWorks_Data`, un archivo de componente de la base de datos `ADVENTUREWORKS2012`.  

```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_ID('AdventureWorks2012_Data')AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
1  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte también  
 [Características desusadas del motor de base de datos de SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [FILE_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/file-name-transact-sql.md)   
 [Funciones de metadatos &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
