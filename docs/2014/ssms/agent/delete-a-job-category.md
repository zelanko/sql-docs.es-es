---
title: Eliminar una categoría de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, categories
- deleting job category
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- removing job category
ms.assetid: 47a7640b-20b3-4639-ab37-b6fc73575e6c
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 775627f625c3033b3dde94373d43303c8a3d6260
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201519"
---
# <a name="delete-a-job-category"></a>Eliminar una categoría de trabajo
  En este tema se describe cómo eliminar una categoría de trabajo del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] u Objetos de administración de SQL Server.  
  
 Las categorías de trabajo le ayudan a organizar los trabajos para poder filtrarlos y agruparlos fácilmente. Por ejemplo, puede organizar todos los trabajos de copia de seguridad de las bases de datos en la categoría Mantenimiento de bases de datos.  
  

  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Al eliminar una categoría de trabajo definida por el usuario, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le solicita que vuelva a asignar los trabajos asignados a ella a otra categoría de trabajo. Solo puede eliminar categorías de trabajo definidas por el usuario.  
  
###  <a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implement SQL Server Agent Security](implement-sql-server-agent-security.md).  
  

  
##  <a name="SSMS"></a> Usar SQL Server Management Studio  
  
#### <a name="to-delete-a-job-category"></a>Para eliminar una categoría de trabajo  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que desea eliminar una categoría de trabajo.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en la carpeta **Trabajos** y seleccione **Administrar categorías de trabajos**.  
  
4.  En el cuadro de diálogo **Administrar categorías de trabajos***nombre_de_servidor*, seleccione la categoría de trabajo que desea eliminar.  
  
5.  Haga clic en **Eliminar**.  
  
6.  En el cuadro de diálogo **Categorías de trabajo** , haga clic en **Sí**.  
  
7.  Cierre el cuadro de diálogo **Administrar categorías de trabajos***nombre_de_servidor*.  
  

  
##  <a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-delete-a-job-category"></a>Para eliminar una categoría de trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- deletes the job category named AdminJobs.  
    USE msdb ;  
    GO   
    EXEC dbo.sp_delete_category  
        @name = N'AdminJobs',  
        @class = N'JOB' ;  
    GO  
    ```  
  
 Para obtener más información, consulte [sp_delete_category &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-category-transact-sql).  
  

  
##  <a name="SMO"></a> Usar objetos de administración de SQL Server  
 **Para eliminar una categoría de trabajo**  
  
 Llame a la `JobCategory` clase mediante el uso de un lenguaje de programación que desee, como Visual Basic, Visual C# o PowerShell.  
  

  
  
