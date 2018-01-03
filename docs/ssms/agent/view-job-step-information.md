---
title: "Ver información de pasos de trabajo | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- displaying job step information
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- viewing job step information
ms.assetid: e3f06492-dc86-4e06-b186-ea58aff6d591
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3a2ec721ed574f1268cea87e2599a93f7c7545aa
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="view-job-step-information"></a>View Job Step Information
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En este tema se describe cómo ver detalles de pasos de trabajo en el cuadro de diálogo Propiedades de paso de trabajo. También incluye información sobre cómo ver la salida de pasos de trabajo.  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   **Para ver información de pasos de trabajo, utilizando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
Si el paso de trabajo está configurado para escribir la salida en una tabla o un archivo y se ha ejecutado el trabajo al menos una vez, puede ver la salida en la página **Avanzadas** del cuadro de diálogo **Propiedades de paso de trabajo** . Cuando se elimina un trabajo o un paso de trabajo, el registro de salida se elimina automáticamente.  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
Puede ver únicamente los pasos de trabajo de su propiedad, a menos que sea miembro del rol fijo de servidor **sysadmin** . Los miembros de este rol pueden ver todos los trabajos y detalles de pasos de trabajo.  
  
## <a name="SSMS"></a>Usar SQL Server Management Studio  
  
#### <a name="to-view-job-step-information"></a>Para ver información de pasos de trabajo  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]y, a continuación, expándala.  
  
2.  Expanda **Agente SQL Server**, **Trabajos**, haga clic con el botón derecho en el trabajo que contiene el paso de trabajo que desea ver y haga clic en **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades del trabajo** , haga clic en la página **Pasos** .  
  
4.  Haga clic en el paso de trabajo que desea ver y después en **Editar**.  
  
5.  En la página **General** del cuadro de diálogo **Propiedades de paso de trabajo** , puede ver el tipo de paso de trabajo y lo que hace.  
  
6.  Haga clic en la página **Avanzadas** para ver las acciones que realiza el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] si el paso de trabajo progresa o no progresa, cuántas veces se debe intentar el paso de trabajo, dónde se escribe la salida del paso de trabajo y el usuario con el que se ejecuta el paso de trabajo.  
  
#### <a name="to-view-job-step-output"></a>Para ver la salida de un paso de trabajo  
  
1.  En el cuadro de diálogo **Propiedades de paso de trabajo** , haga clic en la página **Avanzadas** .  
  
2.  Dependiendo de la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] a la que esté conectado, puede ver el archivo o la tabla de salida del paso de trabajo como se muestra a continuación:  
  
    -   Si está conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o posterior, haga clic en **Ver** solo si está seleccionada la opción **Registro en tabla** . En este caso, la salida del paso de trabajo se escribe en la tabla **sysjobstepslogs** de la base de datos **msdb** .  
  
    -   El botón **Ver** se deshabilita cuando la salida del paso de trabajo se escribe en un archivo. Para ver el archivo de salida de un paso de trabajo, use el Bloc de notas.  
  
