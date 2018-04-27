---
title: Definir las opciones de pasos de trabajo de Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: b2a47057-f6fb-432b-a7b6-5d61f33a5d9c
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7296a4a32491dd49af5b4d5ad49ba7ee70655181
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="define-transact-sql-job-step-options"></a>Define Transact-SQL Job Step Options
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo definir las opciones de pasos de trabajo de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] de [!INCLUDE[tsql](../../includes/tsql_md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] u Objetos de administración de SQL Server.  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para definir las opciones de pasos de trabajo de Transact-SQL con:** ,  
  
    [SQL Server Management Studio](#SSMS)  
  
    [objetos de administración de SQL Server](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usar SQL Server Management Studio  
  
#### <a name="to-define-transact-sql-job-step-options"></a>Para definir opciones de pasos de trabajo de Transact-SQL  
  
1.  En el **Explorador de objetos**, expanda **Agente SQL Server**, expanda **Trabajos**, haga clic con el botón derecho en el trabajo que desee editar y, luego, haga clic en **Propiedades**.  
  
2.  Haga clic en la página **Pasos** , seleccione un paso de trabajo y, a continuación, haga clic en **Modificar**.  
  
3.  En el cuadro de diálogo **Propiedades de paso de trabajo** , confirme que el tipo de trabajo es **Script de Transact-SQL (TSQL)** y seleccione la página **Opciones avanzadas** .  
  
4.  Especifique la acción para llevar a cabo en caso de que el trabajo sea correcto. Para ello, selecciónela de la lista **Acción en caso de éxito** .  
  
5.  Especifique el número de reintentos escribiendo un número comprendido entre 0 y 9999 en el cuadro **Número de reintentos** .  
  
6.  Especifique el intervalo de reintento escribiendo un número de minutos comprendido entre 0 y 9999 en el cuadro **Intervalo de reintento** .  
  
7.  En la lista **Acción en caso de error** , elija la acción que se llevará a cabo en caso de que el trabajo genere un error.  
  
8.  Si el trabajo es un script de [!INCLUDE[tsql](../../includes/tsql_md.md)] , puede elegir una de las siguientes opciones:  
  
    -   Escriba el nombre de un **archivo de salida**. De forma predeterminada, el archivo se sobrescribe cada vez que se ejecuta el paso de trabajo. Si no desea que se sobrescriba el archivo de salida, active la casilla **Anexar salida al archivo existente**. Esta opción solo está disponible para los miembros del rol fijo de servidor **sysadmin** . Tenga en cuenta que [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] no permite a los usuarios ver archivos arbitrarios del sistema de archivos, por lo que no se puede utilizar [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] para ver los registros de los pasos de trabajo que se escriben en el sistema de archivos.  
  
    -   Active la casilla **Registro en tabla** si desea registrar el paso de trabajo en una tabla de bases de datos. De forma predeterminada, el contenido de la tabla se sobrescribe cada vez que se ejecuta el paso de trabajo. Si no desea que se sobrescriba el contenido, active la casilla **Anexar salida a la entrada existente de la tabla**. Una vez ejecutado el paso de trabajo ya puede verse el contenido de la tabla haciendo clic en **Ver**.  
  
    -   Active la casilla **Incluir salida de paso en historial** si desea que la salida se incluya en el historial de pasos. La salida solo se mostrará si no hubo errores. Asimismo, la salida puede aparecer truncada.  
  
9. Si es miembro del rol fijo de servidor **sysadmin** y desea ejecutar este paso de trabajo con otro inicio de sesión de SQL, seleccione el inicio de sesión de SQL en la lista **Ejecutar como usuario** .  
  
## <a name="SMO"></a>Usar Objetos de administración de SQL Server  
**Para definir opciones de pasos de trabajo de Transact-SQL**  
  
Use la clase **JobStep** mediante un lenguaje de programación de su elección, como Visual Basic, Visual C# o PowerShell.  
  
