---
title: Cambiar la pertenencia de una categoría de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- members [SQL Server], job categories
ms.assetid: 6a18f7f0-eb50-485f-a9c7-df31ae0f994e
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 389c9345697a2039ae48f737c32e87916eadf681
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106305"
---
# <a name="change-the-membership-of-a-job-category"></a>Change the Membership of a Job Category
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo cambiar la pertenencia de la categoría de trabajo en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]u Objetos de administración de SQL Server.  
  
Las categorías de trabajo le ayudan a organizar los trabajos para poder filtrarlos y agruparlos fácilmente. Puede crear sus propias categorías de trabajo. También puede cambiar la pertenencia de los trabajos del Agente Microsoft SQL Server en categorías de trabajo.  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para cambiar la pertenencia a una categoría de trabajo, utilizando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [objetos de administración de SQL Server](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usar SQL Server Management Studio  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>Para cambiar la pertenencia a una categoría de trabajo  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que desea editar una categoría de trabajo.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en la carpeta **Trabajos** y seleccione **Administrar categorías de trabajos**.  
  
4.  En el cuadro de diálogo **Administrar categorías de trabajos**_nombre_servidor_ , seleccione la categoría de trabajo que desea editar y, luego, haga clic en **Ver trabajos**.  
  
5.  Active la casilla **Mostrar todos los trabajos** .  
  
6.  Para agregar un trabajo a la categoría, en la cuadrícula principal, active la casilla de la columna **Seleccionar** correspondiente al trabajo. Para quitar un trabajo de la categoría, desactive la casilla. Cuando termine, haga clic en **Aceptar**.  
  
7.  En el cuadro de diálogo **Administrar categorías de trabajos**_nombre_servidor_ .  
  
## <a name="TSQL"></a>Usar Transact-SQL  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>Para cambiar la pertenencia a una categoría de trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
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
  
Para más información, consulte [sp_update_job (Transact-SQL)](https://msdn.microsoft.com/cbdfea38-9e42-47f3-8fc8-5978b82e2623).  
  
## <a name="SMO"></a>Usar Objetos de administración de SQL Server  
**Para cambiar la pertenencia a una categoría de trabajo**  
  
Use la clase **JobCategory** mediante un lenguaje de programación de su elección, como Visual Basic, Visual C# o PowerShell.  
  
