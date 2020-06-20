---
title: Movimiento de una base de datos habilitada para FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], moving a FILESTREAM-enabled database
ms.assetid: dd4d270d-9283-431a-aa6b-e571fced1893
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 79740ee86a89566113650865e3fd6ec54c7cb918
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970866"
---
# <a name="move-a-filestream-enabled-database"></a>Mover una base de datos habilitada para FILESTREAM
  En este tema se muestra cómo mover una base de datos habilitada para FILESTREAM.  
  
> [!NOTE]  
>  Los ejemplos de este tema requieren la base de datos Archive que se crea en [Crear una base de datos habilitada para FILESTREAM](create-a-filestream-enabled-database.md).  
  
### <a name="to-move-a-filestream-enabled-database"></a>Para mover una base de datos habilitada para FILESTREAM  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], haga clic en **Nueva consulta** para abrir el Editor de consultas.  
  
2.  Copie el siguiente script de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el Editor de consultas y, a continuación, haga clic en **Ejecutar**. Este script muestra la ubicación de los archivos de base de datos físicos que usa la base de datos FILESTREAM.  
  
    ```sql  
    USE Archive  
    GO  
    SELECT type_desc, name, physical_name from sys.database_files  
    ```  
  
3.  Copie el siguiente script de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el Editor de consultas y, a continuación, haga clic en **Ejecutar**. Este código pone la base de datos `Archive` sin conexión.  
  
    ```sql  
    USE master  
    EXEC sp_detach_db Archive  
    GO  
    ```  
  
4.  Cree la carpeta `C:\moved_location`y, a continuación, mueva a ella los archivos y carpetas que se enumeran en el paso 2.  
  
5.  Copie el siguiente script de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el Editor de consultas y, a continuación, haga clic en **Ejecutar**. Este script establece la base de datos `Archive` en línea.  
  
    ```sql  
    CREATE DATABASE Archive ON  
    PRIMARY ( NAME = Arch1,  
        FILENAME = 'c:\moved_location\archdat1.mdf'),  
    FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM( NAME = Arch3,  
        FILENAME = 'c:\moved_location\filestream1')  
    LOG ON  ( NAME = Archlog1,  
        FILENAME = 'c:\moved_location\archlog1.ldf')  
    FOR ATTACH  
    GO  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [sp_detach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql)  
  
  
