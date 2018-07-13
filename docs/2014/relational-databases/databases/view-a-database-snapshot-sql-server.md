---
title: Ver una instantánea de base de datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], viewing
- displaying database snapshots
- viewing database snapshots
ms.assetid: 123f19b2-0850-4033-8507-59ebdfb368ee
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: df4ba0cc720cd7dd98addff076c1400747da3551
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37188632"
---
# <a name="view-a-database-snapshot-sql-server"></a>Ver una instantánea de base de datos (SQL Server)
  En este tema se explica cómo ver una instantánea de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!NOTE]  
>  Para crear, volver a una versión anterior o eliminar una instantánea de base de datos, se debe usar [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Para ver una instantánea de base de datos mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 **Para ver una instantánea de base de datos**  
  
1.  En el Explorador de objetos, conéctese a la instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y, a continuación, expándala.  
  
2.  Expanda **Bases de datos**.  
  
3.  Expanda **Instantáneas de base de datos**y, a continuación, seleccione la instantánea que desee ver.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para ver una instantánea de base de datos**  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Para enumerar las instantáneas de base de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte la columna **source_database_id** de la vista de catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) para ver si hay valores distintos de NULL.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Crear una instantánea de base de datos &#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md)  
  
-   [Revertir una base de datos a una instantánea de base de datos](revert-a-database-to-a-database-snapshot.md)  
  
-   [Eliminar una instantánea de base de datos &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [Instantáneas de bases de datos &#40;SQL Server&#41;](database-snapshots-sql-server.md)  
  
  
