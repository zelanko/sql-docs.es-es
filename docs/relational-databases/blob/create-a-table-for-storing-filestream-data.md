---
title: "Crear una tabla para almacenar datos FILESTREAM | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-blob"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FILESTREAM [SQL Server], almacenamiento de tablas"
ms.assetid: 029c3059-5c83-43e2-a859-9027031b7de1
caps.latest.revision: 16
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 16
---
# Crear una tabla para almacenar datos FILESTREAM
  En este tema se muestra cómo crear una tabla para almacenar datos FILESTREAM.  
  
 Cuando la base de datos tiene un grupo de archivos FILESTREAM, es posible crear o modificar tablas para almacenar datos FILESTREAM. Para especificar que una columna contiene datos FILESTREAM, se debe crear una columna **varbinary(max)** y agregar el atributo FILESTREAM.  
  
### Para crear una tabla para almacenar datos FILESTREAM  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], haga clic en **Nueva consulta** para mostrar el Editor de consultas.  
  
2.  Copie el código [!INCLUDE[tsql](../../includes/tsql-md.md)] del ejemplo siguiente en el Editor de consultas. Este código [!INCLUDE[tsql](../../includes/tsql-md.md)] crea una tabla habilitada para FILESTREAM denominada Records.  
  
3.  Para crear la tabla, haga clic en **Ejecutar**.  
  
## Ejemplo  
 En el siguiente ejemplo de código se muestra cómo crear una tabla denominada `Records`. La columna `Id` es una columna `ROWGUIDCOL` y es necesaria para usar datos FILESTREAM con las API de Win32. La columna `SerialNumber` es una columna `UNIQUE INTEGER`. La columna `Chart` es una columna `FILESTREAM` y se usa para almacenar `Chart` en el sistema de archivos.  
  
> [!NOTE]  
>  En este ejemplo se hace referencia a la base de datos de archivo que se creó en [Crear una base de datos habilitada para FILESTREAM](../../relational-databases/blob/create-a-filestream-enabled-database.md).  
  
 [!code-sql[FILESTREAM#FS_CreateTable](../../relational-databases/blob/codesnippet/tsql/create-a-table-for-stori_1.sql)]  
  
## Vea también  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  