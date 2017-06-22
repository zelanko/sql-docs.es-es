---
title: "Eliminación de un punto de control de la utilidad de SQL Server (utilidad de SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c048a416-900e-4c77-8243-e0f0d8b94068
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b38f97d5d0dacb8222faf67387c97b33d2dd5de6
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="remove-a-utility-control-point-sql-server-utility"></a>Quitar un punto de control de la utilidad de SQL Server (utilidad de SQL Server)
  En este tema se describe cómo quitar un punto de control de la utilidad (UCP) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para quitar un punto de control de la utilidad, utilizando:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Antes de utilizar este procedimiento para quitar el UCP de la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tenga en cuenta los siguientes requisitos. El procedimiento almacenado ejecutará las comprobaciones de los requisitos previos como parte de la operación.  
  
-   Antes de ejecutar este procedimiento, todas las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se deben quitar del UCP. Tenga en cuenta que el UCP es una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Quitar una instancia de SQL Server de la Utilidad de SQL Server](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md).  
  
-   Este procedimiento se tiene que ejecutar en un equipo que sea un UCP.  
  
-   Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se quitó el UCP tiene un conjunto de recopilación de datos que no es de utilidad, el procedimiento no quitará la base de datos UMDW (sysutility_mdw). Si es así, la base de datos UMDW (sysutility_mdw) se debe quitar de modo manual para poder volver a crear el UCP.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para ejecutar este procedimiento, el usuario debe tener permisos **sysadmin** , los mismos que se necesitan para crear un UCP.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-remove-a-utility-control-point"></a>Para quitar un punto de control de la utilidad  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
```  
EXEC msdb.dbo.sp_sysutility_ucp_remove;  
```  
  
## <a name="see-also"></a>Vea también  
 [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Utilizar el explorador de Utilidad para administrar la utilidad de SQL Server](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [Solucionar problemas de la Utilidad de SQL Server](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
