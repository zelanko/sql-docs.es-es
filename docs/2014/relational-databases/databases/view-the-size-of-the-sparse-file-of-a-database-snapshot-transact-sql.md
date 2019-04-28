---
title: Ver el tamaño del archivo disperso de una instantánea de base de datos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server database snapshots], sparse files
- space [SQL Server], sparse files
- sparse files [SQL Server]
- size [SQL Server], sparse files
- maximum sparse file size
- database snapshots [SQL Server], sparse files
- space [SQL Server], database snapshots
ms.assetid: 1867c5f8-d57c-46d3-933d-3642ab0a8e24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c2a7e507e45d8429312834911b7bef5ae1e784c8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62870884"
---
# <a name="view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql"></a>Ver el tamaño del archivo disperso de una instantánea de base de datos (Transact-SQL)
  En este tema se describe cómo usar [!INCLUDE[tsql](../../includes/tsql-md.md)] para comprobar que un archivo de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un archivo disperso y para determinar su tamaño real y máximo. Las instantáneas de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usan archivos dispersos, que son una característica del sistema de archivos NTFS.  
  
> [!NOTE]  
>  Durante la creación de instantáneas de base de datos, se crean archivos dispersos con los nombres de archivo de la instrucción CREATE DATABASE. Estos nombres de archivo se almacenan en la columna **physical_name** de **sys.master_files** . En **sys.database_files** , ya sea en la base de datos de origen o en una instantánea, la columna **physical_name** siempre incluye los nombres de los archivos de la base de datos de origen.  
  
## <a name="verify-that-a-database-file-is-a-sparse-file"></a>Comprobar que un archivo de base de datos es un archivo disperso  
  
1.  En la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
     Seleccione la columna **is_sparse** de **sys.database_files** en la instantánea de base de datos o de **sys.master_files**. El valor indica si el archivo es un archivo disperso, de la manera siguiente:  
  
     1 = El archivo es un archivo disperso.  
  
     0 = El archivo no es un archivo disperso.  
  
## <a name="find-out-the-actual-size-of-a-sparse-file"></a>Calcular el tamaño real de un archivo disperso  
  
> [!NOTE]  
>  El tamaño de los archivos dispersos aumenta en incrementos de 64 kilobytes (KB), por lo que siempre es un múltiplo de 64 KB.  
  
 Para ver el número de bytes que cada archivo disperso de una instantánea está usando actualmente en el disco, consulte la columna **size_on_disk_bytes** de la vista de administración dinámica [sys.dm_io_virtual_file_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para ver el espacio en disco que usa un archivo disperso, haga clic con el botón derecho en el archivo en Microsoft Windows, haga clic en **Propiedades** y consulte el valor de **Tamaño en disco**.  
  
## <a name="find-out-the-maximum-size-of-a-sparse-file"></a>Calcular el tamaño máximo de un archivo disperso  
 El tamaño máximo de un archivo disperso es el tamaño del archivo de la base de datos de origen correspondiente en el momento de la creación de la instantánea. Para saber cuál es este tamaño, puede usar cualquiera de las alternativas siguientes:  
  
-   Con el símbolo del sistema de Windows:  
  
    1.  Utilice los comandos **dir** de Windows.  
  
    2.  Seleccione el archivo disperso, abra el cuadro de diálogo **Propiedades** del archivo en Windows y consulte el valor de **Tamaño** .  
  
-   En la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
     Seleccione la columna **size** de **sys.database_files** en la instantánea de base de datos o de **sys.master_files**. El valor de la columna **size** refleja el espacio máximo, en páginas SQL, que puede usar la instantánea. Este valor es equivalente al del campo **Tamaño** de Windows, con la diferencia de que se representa en términos de número de páginas SQL del archivo. El tamaño en bytes es el siguiente:  
  
     (*número_de_páginas* * 8192)  
  
## <a name="see-also"></a>Vea también  
 [Instantáneas de bases de datos &#40;SQL Server&#41;](database-snapshots-sql-server.md)   
 [sys.fn_virtualfilestats &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql)   
 [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
  
