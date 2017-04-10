---
title: "Ver el tama&#241;o del archivo disperso de una instant&#225;nea de base de datos (Transact-SQL) | Microsoft Docs"
ms.date: "07/28/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "instantáneas [instantáneas de base de datos de SQL Server], archivos dispersos"
  - "espacio [SQL Server], archivos dispersos"
  - "dispersos, archivos [SQL Server]"
  - "tamaño [SQL Server], archivos dispersos"
  - "tamaño máximo de archivos dispersos"
  - "instantáneas de base de datos [SQL Server], archivos dispersos"
  - "espacio [SQL Server], instantáneas de base de datos"
ms.assetid: 1867c5f8-d57c-46d3-933d-3642ab0a8e24
caps.latest.revision: 41
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 41
---
# Ver el tama&#241;o del archivo disperso de una instant&#225;nea de base de datos (Transact-SQL)
  En este tema se describe cómo usar [!INCLUDE[tsql](../../includes/tsql-md.md)] para comprobar que un archivo de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un archivo disperso y para determinar su tamaño real y máximo. Las instantáneas de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usan archivos dispersos, que son una característica del sistema de archivos NTFS.  
  
> [!NOTE]  
>  Durante la creación de instantáneas de base de datos, se crean archivos dispersos con los nombres de archivo de la instrucción CREATE DATABASE. Estos nombres de archivo se almacenan en la columna **physical_name** de **sys.master_files**. En **sys.database_files**, ya sea en la base de datos de origen o en una instantánea, la columna **physical_name** siempre incluye los nombres de los archivos de la base de datos de origen.  
  
## Comprobar que un archivo de base de datos es un archivo disperso  
  
1.  En la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
     Seleccione la columna **is_sparse** de **sys.database_files** en la instantánea de base de datos o de **sys.master_files**. El valor indica si el archivo es un archivo disperso, de la manera siguiente:  
  
     1 = El archivo es un archivo disperso.  
  
     0 = El archivo no es un archivo disperso.  
  
## Calcular el tamaño real de un archivo disperso  
  
> [!NOTE]  
>  El tamaño de los archivos dispersos aumenta en incrementos de 64 kilobytes (KB), por lo que siempre es un múltiplo de 64 KB.  
  
 Para ver el número de bytes que cada archivo disperso de una instantánea está usando actualmente en el disco, consulte la columna **size_on_disk_bytes** de la vista de administración dinámica [sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para ver el espacio en disco que usa un archivo disperso, haga clic con el botón derecho en el archivo en Microsoft Windows, haga clic en **Propiedades** y consulte el valor de **Tamaño en disco**.  
  
## Calcular el tamaño máximo de un archivo disperso  
 El tamaño máximo de un archivo disperso es el tamaño del archivo de la base de datos de origen correspondiente en el momento de la creación de la instantánea. Para saber cuál es este tamaño, puede usar cualquiera de las alternativas siguientes:  
  
-   Con el símbolo del sistema de Windows:  
  
    1.  Utilice los comandos **dir** de Windows.  
  
    2.  Seleccione el archivo disperso, abra el cuadro de diálogo **Propiedades** del archivo en Windows y consulte el valor de **Tamaño** .  
  
-   En la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
     Seleccione la columna **size** de **sys.database_files** en la instantánea de base de datos o de **sys.master_files**. El valor de la columna **size** refleja el espacio máximo, en páginas SQL, que puede usar la instantánea. Este valor es equivalente al del campo **Tamaño** de Windows, con la diferencia de que se representa en términos de número de páginas SQL del archivo. El tamaño en bytes es el siguiente:  
  
     (*número_de_páginas* * 8192)  

## Ejemplo
El script siguiente mostrará el tamaño del disco en kilobytes de cada archivo disperso.  El script también mostrará el tamaño máximo en megabytes que puede llegar a tener un archivo disperso.  Ejecute el script Transact-SQL en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].

```tsql
SELECT  DB_NAME(sd.source_database_id) AS [SourceDatabase], 
        sd.name AS [Snapshot],
        mf.name AS [Filename], 
        size_on_disk_bytes/1024 AS [size_on_disk (KB)],
        mf2.size/128 AS [MaximumSize (MB)]
FROM sys.master_files mf
JOIN sys.databases sd
    ON mf.database_id = sd.database_id
JOIN sys.master_files mf2
    ON sd.source_database_id = mf2.database_id
    AND mf.file_id = mf2.file_id
CROSS APPLY sys.dm_io_virtual_file_stats(sd.database_id, mf.file_id)
WHERE mf.is_sparse = 1
AND mf2.is_sparse = 0
ORDER BY 1;
```
  
## Vea también  
 [Instantáneas de base de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [sys.fn_virtualfilestats &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  