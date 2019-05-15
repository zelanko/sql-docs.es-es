---
title: Movimiento de una base de datos habilitada para FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], moving a FILESTREAM-enabled database
ms.assetid: dd4d270d-9283-431a-aa6b-e571fced1893
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 57a5984aebfc2261c5b6f524dd111e8ba786733a
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65094148"
---
# <a name="move-a-filestream-enabled-database"></a>Mover una base de datos habilitada para FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se muestra cómo mover una base de datos habilitada para FILESTREAM.  
  
> [!NOTE]  
>  Los ejemplos de este tema requieren la base de datos Archive que se crea en [Crear una base de datos habilitada para FILESTREAM](../../relational-databases/blob/create-a-filestream-enabled-database.md).  
  
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
 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
  
