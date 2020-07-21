---
title: Ver una instantánea de base de datos (SQL Server) | Microsoft Docs
description: Obtenga información sobre cómo ver una instantánea de base de datos de SQL Server mediante SQL Server Management Studio o Transact-SQL.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], viewing
- displaying database snapshots
- viewing database snapshots
ms.assetid: 123f19b2-0850-4033-8507-59ebdfb368ee
author: stevestein
ms.author: sstein
ms.openlocfilehash: a7ba50746752b0c3531d1ae3a0b1b9d4820dea82
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727538"
---
# <a name="view-a-database-snapshot-sql-server"></a>Ver una instantánea de base de datos (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En este tema se explica cómo ver una instantánea de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!NOTE]  
>  Para crear, volver a una versión anterior o eliminar una instantánea de base de datos, se debe usar [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Para ver una instantánea de base de datos mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 **Para ver una instantánea de base de datos**  
  
1.  En el Explorador de objetos, conéctese a la instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y, a continuación, expándala.  
  
2.  Expanda **Bases de datos**.  
  
3.  Expanda **Instantáneas de base de datos**y, a continuación, seleccione la instantánea que desee ver.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para ver una instantánea de base de datos**  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Para enumerar las instantáneas de base de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte la columna **source_database_id** de la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) para ver si hay valores distintos de NULL.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Crear una instantánea de base de datos &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [Revertir una base de datos a una instantánea de base de datos](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)  
  
-   [Eliminar una instantánea de base de datos &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>Consulte también  
 [Instantáneas de bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
