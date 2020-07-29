---
title: View Job Step Information
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- displaying job step information
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- viewing job step information
ms.assetid: e3f06492-dc86-4e06-b186-ea58aff6d591
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2dc60fb5ef44ff4b94cf8326e97d552f34c3b1c7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729723"
---
# <a name="view-job-step-information"></a>View Job Step Information
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Este tema explica cómo ver detalles de pasos de trabajo en el cuadro de diálogo Propiedades de paso de trabajo. También incluye información sobre cómo ver la salida de pasos de trabajo.  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   **Para ver información de pasos de trabajo, utilizando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitaciones y restricciones  
Si el paso de trabajo está configurado para escribir la salida en una tabla o un archivo y se ha ejecutado el trabajo al menos una vez, puede ver la salida en la página **Avanzadas** del cuadro de diálogo **Propiedades de paso de trabajo** . Cuando se elimina un trabajo o un paso de trabajo, el registro de salida se elimina automáticamente.  
  
### <a name="security"></a><a name="Security"></a>Seguridad  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permisos  
Puede ver únicamente los pasos de trabajo de su propiedad, a menos que sea miembro del rol fijo de servidor **sysadmin** . Los miembros de este rol pueden ver todos los trabajos y detalles de pasos de trabajo.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>Usar SQL Server Management Studio  
  
#### <a name="to-view-job-step-information"></a>Para ver información de pasos de trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] y expándala.  
  
2.  Expanda **Agente SQL Server**, **Trabajos**, haga clic con el botón derecho en el trabajo que contiene el paso de trabajo que desea ver y haga clic en **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades del trabajo** , haga clic en la página **Pasos** .  
  
4.  Haga clic en el paso de trabajo que desea ver y después en **Editar**.  
  
5.  En la página **General** del cuadro de diálogo **Propiedades de paso de trabajo** , puede ver el tipo de paso de trabajo y lo que hace.  
  
6.  Haga clic en la página **Avanzadas** para ver las acciones que realiza el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si el paso de trabajo progresa o no progresa, cuántas veces se debe intentar el paso de trabajo, dónde se escribe la salida del paso de trabajo y el usuario con el que se ejecuta el paso de trabajo.  
  
#### <a name="to-view-job-step-output"></a>Para ver la salida de un paso de trabajo  
  
1.  En el cuadro de diálogo **Propiedades de paso de trabajo** , haga clic en la página **Avanzadas** .  
  
2.  Dependiendo de la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que esté conectado, puede ver el archivo o la tabla de salida del paso de trabajo como se muestra a continuación:  
  
    -   Si está conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o posterior, haga clic en **Ver** solo si está seleccionada la opción **Registro en tabla** . En este caso, la salida del paso de trabajo se escribe en la tabla **sysjobstepslogs** de la base de datos **msdb** .  
  
    -   El botón **Ver** se deshabilita cuando la salida del paso de trabajo se escribe en un archivo. Para ver el archivo de salida de un paso de trabajo, use el Bloc de notas.  
  
