---
title: Eliminar una categoría de trabajo
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- deleting job category
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- removing job category
ms.assetid: 47a7640b-20b3-4639-ab37-b6fc73575e6c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 445f3818a1b59004cea558f8631aba85a3f1e8d9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85690976"
---
# <a name="delete-a-job-category"></a>Eliminar una categoría de trabajo
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo eliminar una categoría de trabajo del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] u Objetos de administración de SQL Server.  
  
Las categorías de trabajo le ayudan a organizar los trabajos para poder filtrarlos y agruparlos fácilmente. Por ejemplo, puede organizar todos los trabajos de copia de seguridad de las bases de datos en la categoría Mantenimiento de bases de datos.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitaciones y restricciones  
Al eliminar una categoría de trabajo definida por el usuario, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le solicita que vuelva a asignar los trabajos asignados a ella a otra categoría de trabajo. Solo puede eliminar categorías de trabajo definidas por el usuario.  
  
### <a name="security"></a><a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>Usar SQL Server Management Studio  
  
#### <a name="to-delete-a-job-category"></a>Para eliminar una categoría de trabajo  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que desea eliminar una categoría de trabajo.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en la carpeta **Trabajos** y seleccione **Administrar categorías de trabajos**.  
  
4.  En el cuadro de diálogo **Administrar categorías de trabajos**_nombre\_servidor_, seleccione la categoría de trabajo que quiera eliminar.  
  
5.  Haga clic en **Eliminar**.  
  
6.  En el cuadro de diálogo **Categorías de trabajo** , haga clic en **Sí**.  
  
7.  Cierre el cuadro de diálogo **Administrar categorías de trabajos**_nombre\_servidor_.  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>Usar Transact-SQL  
  
#### <a name="to-delete-a-job-category"></a>Para eliminar una categoría de trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
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
  
Para más información, consulte [sp_delete_category (Transact-SQL)](https://msdn.microsoft.com/63ea7d0d-a567-456e-a778-bee99e21d16c).  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usar Objetos de administración de SQL Server  
**Para eliminar una categoría de trabajo**  
  
Llame a la clase **JobCategory** mediante un lenguaje de programación de su elección, como Visual Basic, Visual C# o PowerShell.  
  
