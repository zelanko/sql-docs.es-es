---
title: "Importar de forma masiva datos de objetos de gran tama&#241;o mediante el proveedor de conjuntos de filas BULK OPENROWSET (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-bulk-import-export"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SINGLE_NCLOB, opción"
  - "proveedores de conjuntos de filas BULK [SQL Server]"
  - "importar en bloque [SQL Server], formatos de archivo"
  - "Función OPENROWSET, importación en bloque de datos grandes"
  - "SINGLE_CLOB, opción"
  - "formatos de datos [SQL Server], datos de objetos grandes"
  - "datos grandes, importaciones en bloque"
  - "SINGLE_BLOB, opción"
ms.assetid: 171cdd5c-1e47-4bd7-b99a-4f0fd4e10526
caps.latest.revision: 16
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Importar de forma masiva datos de objetos de gran tama&#241;o mediante el proveedor de conjuntos de filas BULK OPENROWSET (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  El proveedor de conjuntos de filas BULK OPENROWSET de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite realizar la importación masiva de un archivo de datos como datos de objetos grandes.  
  
 Los tipos de datos de objetos grandes admitidos por el proveedor de conjuntos de filas BULK OPENROWSET son: **varbinary**(max) o **image**, **varchar**(max) o **text**, y **nvarchar**(max) o **ntext**.  
  
> [!NOTE]  
>  Los tipos de datos **image**, **text** y **ntext** han quedado en desuso.  
  
 La cláusula BULK de OPENROWSET admite tres opciones para importar el contenido de un archivo de datos como un conjunto de filas de fila única y columna única. Puede especificar una de estas opciones de objetos grandes en lugar de usar un archivo de formato. Las opciones son las siguientes:  
  
 SINGLE_BLOB  
 Lee el contenido de *data_file* como un archivo de una sola fila y devuelve el contenido como un conjunto de filas de una sola columna del tipo **varbinary(max)**.  
  
 SINGLE_CLOB  
 Lee el contenido del archivo de datos especificado como caracteres y devuelve el contenido como un conjunto de filas de una sola fila y una sola columna del tipo **varchar(max)**, mediante la intercalación de la base de datos actual, como un documento de texto o de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word.  
  
 SINGLE_NCLOB  
 Lee el contenido del archivo de datos especificado como Unicode y devuelve el contenido como un conjunto de filas de una sola fila y una sola columna del tipo **nvarchar(max)**, mediante la intercalación de la base de datos actual.  
  
## Vea también  
 [Importación en bloque de datos mediante las instrucciones BULK INSERT u OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)   
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
  