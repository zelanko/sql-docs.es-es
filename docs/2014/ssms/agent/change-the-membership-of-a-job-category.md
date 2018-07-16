---
title: Cambiar la pertenencia de una categoría de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- members [SQL Server], job categories
ms.assetid: 6a18f7f0-eb50-485f-a9c7-df31ae0f994e
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6c430bba54c46572f5d8afdfe5a0606e207d875c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37303495"
---
# <a name="change-the-membership-of-a-job-category"></a>Change the Membership of a Job Category
  En este tema se describe cómo cambiar la pertenencia de la categoría de trabajo en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]u Objetos de administración de SQL Server.  
  
 Las categorías de trabajo le ayudan a organizar los trabajos para poder filtrarlos y agruparlos fácilmente. Puede crear sus propias categorías de trabajo. También puede cambiar la pertenencia de los trabajos del Agente Microsoft SQL Server en categorías de trabajo.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para cambiar la pertenencia a una categoría de trabajo, utilizando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [objetos de administración de SQL Server](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implement SQL Server Agent Security](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usar SQL Server Management Studio  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>Para cambiar la pertenencia a una categoría de trabajo  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que desea editar una categoría de trabajo.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en la carpeta **Trabajos** y seleccione **Administrar categorías de trabajos**.  
  
4.  En el cuadro de diálogo **Administrar categorías de trabajos***nombre_de_servidor*, seleccione la categoría de trabajo que desea editar y, luego, haga clic en **Ver trabajos**.  
  
5.  Active la casilla **Mostrar todos los trabajos** .  
  
6.  Para agregar un trabajo a la categoría, en la cuadrícula principal, active la casilla de la columna **Seleccionar** correspondiente al trabajo. Para quitar un trabajo de la categoría, desactive la casilla. Cuando termine, haga clic en **Aceptar**.  
  
7.  Cierre el cuadro de diálogo **Administrar categorías de trabajos***nombre_de_servidor*.  
  
##  <a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>Para cambiar la pertenencia a una categoría de trabajo  
  
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
 **Para cambiar la pertenencia a una categoría de trabajo**  
  
 Use la `JobCategory` clase mediante el uso de un lenguaje de programación que desee, como Visual Basic, Visual C# o PowerShell.  
  
  
