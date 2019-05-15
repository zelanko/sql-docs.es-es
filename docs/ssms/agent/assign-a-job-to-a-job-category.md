---
title: Asignar un trabajo a una categoría de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4947751be0d3ed2c0d10cfce774f1fa9cec35a38
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65097561"
---
# <a name="assign-a-job-to-a-job-category"></a>Asignar un trabajo a una categoría de trabajo
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo asignar trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a categorías de trabajo en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] u Objetos de administración de SQL Server.  
  
Las categorías de trabajo le ayudan a organizar los trabajos para poder filtrarlos y agruparlos fácilmente. Por ejemplo, puede organizar todos los trabajos de copia de seguridad de las bases de datos en la categoría Mantenimiento de bases de datos. Puede asignar trabajos a las categorías de trabajo integradas o puede crear una categoría de trabajo definida por el usuario y, después, asignarle trabajos.  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para asignar un trabajo a una categoría de trabajo, utilizando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [objetos de administración de SQL Server](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usar SQL Server Management Studio  
  
#### <a name="to-assign-a-job-to-a-job-category"></a>Para asignar un trabajo a una categoría de trabajo  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que desea asignar un trabajo a una categoría de trabajo.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic en el signo más para expandir la carpeta **Trabajos** .  
  
4.  Haga clic con el botón derecho en el trabajo que desee editar y seleccione **Propiedades**.  
  
5.  En el cuadro de diálogo **Propiedades del trabajo** _nombre\_trabajo_, en la lista **Categoría**, seleccione la categoría de trabajo que quiere asignar al trabajo.  
  
6.  Haga clic en **Aceptar**.  
  
## <a name="TSQL"></a>Usar Transact-SQL  
  
#### <a name="to-assign-a-job-to-a-job-category"></a>Para asignar un trabajo a una categoría de trabajo  
  
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
**Para asignar un trabajo a una categoría de trabajo**  
  
Use la clase **JobCategory** mediante un lenguaje de programación de su elección, como Visual Basic, Visual C# o PowerShell.  
  
