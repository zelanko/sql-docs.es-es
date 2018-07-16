---
title: Eliminación de una base de datos | Microsoft Docs
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
- database removal [SQL Server], SQL Server Management Studio
- removing databases
- deleting databases
- dropping databases
- databases [SQL Server], dropping
- database removal [SQL Server]
ms.assetid: 1fd8c0f5-03e1-449a-af45-b8cacb479d9c
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4c07c4a12f0e9f873266ba7862a7f291cc374151
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37274321"
---
# <a name="delete-a-database"></a>Eliminar una base de datos
  En este tema se describe cómo eliminar una base de datos definida por el usuario en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Requisitos previos](#Prerequisites)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para eliminar una base de datos, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Follow Up:**  [After deleting a database](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Las bases de datos del sistema no se pueden eliminar.  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Elimine las instantáneas de bases de datos que existan en la base de datos. Para obtener más información, vea [Eliminar una instantánea de base de datos &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md).  
  
-   Si la base de datos interviene en el trasvase de registros, elimínelo.  
  
-   Si la base de datos se publica para la replicación transaccional, o se publica o suscribe para la replicación de mezcla, elimine la replicación de la base de datos.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Tenga en cuenta la posibilidad de realizar una copia de seguridad completa de la base de datos. Una base de datos eliminada solo puede volver a crearse si se restaura una copia de seguridad.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Para ejecutar DROP DATABASE, el usuario debe tener, como mínimo, el permiso CONTROL en la base de datos.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-delete-a-database"></a>Para eliminar una base de datos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, a continuación, expándala.  
  
2.  Expanda **Bases de datos**, haga clic con el botón derecho en la base de datos que quiera eliminar y, luego, haga clic en **Eliminar**.  
  
3.  Confirme que ha seleccionado la base de datos correcta y haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-delete-a-database"></a>Para eliminar una base de datos  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. El ejemplo quita las bases de datos `Sales` y `NewSales` .  
  
```tsql  
USE master ;  
GO  
DROP DATABASE Sales, NewSales ;  
GO  
```  
  
##  <a name="FollowUp"></a> Seguimiento: Después de eliminar una base de datos  
 Hacer una copia de seguridad de la base de datos **maestra** . Si es necesario restaurar la base de datos **maestra** , cualquier base de datos que se haya eliminado después de la última copia de seguridad **maestra** seguirá teniendo referencias en las vistas del catálogo del sistema y puede dar lugar a la aparición de mensajes de error.  
  
## <a name="see-also"></a>Vea también  
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
