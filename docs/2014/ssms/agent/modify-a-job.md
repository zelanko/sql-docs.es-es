---
title: Modificar un trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
ms.assetid: dd5e5f20-20c4-4ab9-a19a-db87577dcd43
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0d25830ad119a1f5f344a4dcf318c35bee5f86ca
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062186"
---
# <a name="modify-a-job"></a>Modify a Job
  En este tema se describe cómo cambiar las propiedades de los [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajos del agente en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , [!INCLUDE[tsql](../../includes/tsql-md.md)] o objetos de administración de SQL Server.  
  
 **En este tema**  
  
-   **Antes de empezar:** ,  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para modificar un trabajo, utilizando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [objetos de administración de SQL Server](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
 No se puede destinar un trabajo principal del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a servidores locales y remotos.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
 A menos que sea miembro del rol fijo de servidor **sysadmin** , solo podrá modificar los trabajos de su propiedad. Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-modify-a-job"></a>Para modificar un trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Expanda **Agente SQL Server**, expanda **Trabajos**, haga clic con el botón derecho en el trabajo que desee modificar y haga clic en **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades del trabajo** , actualice las propiedades, los pasos, la programación, las alertas y las notificaciones del trabajo desde las páginas correspondientes.  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-modify-a-job"></a>Para modificar un trabajo  
  
1.  En el Explorador de objetos, conéctese a una instancia del Motor de base de datos y, a continuación, expándala.  
  
2.  En la barra de herramientas, haga clic en **Nueva consulta**.  
  
3.  En la ventana de consulta, use los siguientes procedimientos almacenados del sistema para modificar un trabajo.  
  
    -   Ejecute [sp_update_job &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql) para cambiar los atributos de un trabajo.  
  
    -   Ejecute [sp_update_schedule &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql) para cambiar los detalles de la programación de una definición de trabajo.  
  
    -   Ejecute [sp_add_jobstep &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql) para agregar nuevos pasos de trabajo.  
  
    -   Ejecute [sp_update_jobstep &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql) para cambiar los pasos de trabajo ya existentes.  
  
    -   Ejecute [sp_delete_jobstep &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql) para quitar un paso de trabajo de un trabajo.  
  
    -   Procedimientos almacenados adicionales para modificar cualquier trabajo maestro del Agente SQL Server:  
  
        -   Ejecute [sp_delete_jobserver &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql) para eliminar un servidor asociado actualmente a un trabajo.  
  
        -   Ejecute [sp_add_jobserver &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql) para asociar un servidor al trabajo actual.  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usar Objetos de administración de SQL Server  
 **Para modificar un trabajo**  
  
 Utilice la clase `Job` mediante un lenguaje de programación que elija, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
  
