---
title: Asignar un trabajo a una categoría de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], assigning
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- SQL Server Agent jobs, assigning
- assigning job to category
ms.assetid: a9ea65a2-1d73-4582-a335-63adeb450cb6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab7695b6a80772ddcd01996e783fffd806447c59
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52786297"
---
# <a name="assign-a-job-to-a-job-category"></a>Asignar un trabajo a una categoría de trabajo
  En este tema se describe cómo asignar trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a categorías de trabajo en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] u Objetos de administración de SQL Server.  
  
 Las categorías de trabajo le ayudan a organizar los trabajos para poder filtrarlos y agruparlos fácilmente. Por ejemplo, puede organizar todos los trabajos de copia de seguridad de las bases de datos en la categoría Mantenimiento de bases de datos. Puede asignar trabajos a las categorías de trabajo integradas o puede crear una categoría de trabajo definida por el usuario y, después, asignarle trabajos.  
  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  
  
  
##  <a name="SSMS"></a> Usar SQL Server Management Studio  
  
#### <a name="to-assign-a-job-to-a-job-category"></a>Para asignar un trabajo a una categoría de trabajo  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que desea asignar un trabajo a una categoría de trabajo.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic en el signo más para expandir la carpeta **Trabajos** .  
  
4.  Haga clic con el botón derecho en el trabajo que desee editar y seleccione **Propiedades**.  
  
5.  En el cuadro de diálogo **Propiedades del trabajo -**_nombre_trabajo_ , en la lista **Categoría** , seleccione la categoría de trabajo que quiere asignar al trabajo.  
  
6.  Haga clic en **Aceptar**.  
  
  
##  <a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-assign-a-job-to-a-job-category"></a>Para asignar un trabajo a una categoría de trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- adding a new job category to the "NightlyBackups" job  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @category_name = N'[Uncategorized (Local)]';  
    GO  
    ```  
  
 Para obtener más información, consulte [sp_update_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql).  
  
  
  
##  <a name="SMO"></a> Usar objetos de administración de SQL Server  
 **Para asignar un trabajo a una categoría de trabajo**  
  
 Utilice la clase `JobCategory` mediante un lenguaje de programación que elija, como Visual Basic, Visual C# o PowerShell.  
  
  
  
  
