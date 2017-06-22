---
title: Ejecutar los pasos Windows PowerShell del Agente SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f25f7549-c9b3-4618-85f2-c9a08adbe0e3
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ae35fb3deecc8b77940ab76d1b0f016f00f39e27
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="run-windows-powershell-steps-in-sql-server-agent"></a>Ejecutar los pasos Windows PowerShell del Agente SQL Server
  Use el Agente SQL Server para ejecutar scripts de SQL Server PowerShell en momentos programados.  
  
1.  **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions)  
  
2.  **To run PowerShell from SQL Server Agent, using:**  [PowerShell Job Step](#PShellJob), [Command Prompt Job Step](#CmdExecJob)  
  
## <a name="before-you-begin"></a>Antes de comenzar  
 Hay varios tipos de pasos de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cada tipo se asocia a un subsistema que implementa un entorno concreto, como un agente de replicación o un entorno del símbolo del sistema. Puede codificar scripts de Windows PowerShell y, a continuación, utilizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para incluir los scripts en trabajos que se ejecuten en los momentos programados o como respuesta a eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los scripts de Windows PowerShell pueden ejecutarse mediante un paso de trabajo del símbolo del sistema o un paso de trabajo de PowerShell.  
  
1.  Use un paso de trabajo de PowerShell para que el subsistema del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecute la utilidad **sqlps** , que inicia PowerShell e importa el módulo **sqlps** .  
  
2.  Use un paso de trabajo de símbolo del sistema para ejecutar PowerShell.exe y especificar un script que importa el módulo **sqlps** .  
  
###  <a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
  
> [!CAUTION]  
>  Cada paso de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ejecuta PowerShell con el módulo **sqlps** inicia un proceso que consume aproximadamente 20 MB de memoria. Si ejecuta muchos pasos de trabajo de Windows PowerShell simultáneos, el rendimiento se puede ver afectado adversamente.  
  
##  <a name="PShellJob"></a> Crear un paso de trabajo de PowerShell  
 **Para crear un paso de trabajo de PowerShell**  
  
1.  Expanda el **Agente SQL Server**, cree un trabajo o haga clic con el botón derecho en uno existente y, después, haga clic en **Propiedades**. Para obtener más información acerca de cómo crear un trabajo, vea [Crear trabajos](http://msdn.microsoft.com/library/465fb7fc-7622-4252-a178-ea51691c935b).  
  
2.  En el cuadro de diálogo **Propiedades del trabajo** , haga clic en la página **Pasos** y, a continuación, haga clic en **Nuevo**.  
  
3.  En el cuadro de diálogo **Nuevo paso de trabajo** , escriba un nombre para el paso de trabajo en **Nombre del paso**.  
  
4.  En la lista **Tipo** , haga clic en **PowerShell**.  
  
5.  En la lista **Ejecutar como** , seleccione la cuenta de proxy con las credenciales que utilizará el trabajo.  
  
6.  En el cuadro **Comando** , especifique la sintaxis del script de PowerShell que se ejecutará para el paso de trabajo. También puede hacer clic en **Abrir** y seleccionar un archivo que contenga la sintaxis del script.  
  
7.  Haga clic en la página **Avanzadas** para establecer las siguientes opciones de paso de trabajo: acción que se llevará a cabo si el paso de trabajo progresa o no, número de veces que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe intentar ejecutar el paso de trabajo y frecuencia de los intentos.  
  
##  <a name="CmdExecJob"></a> Crear un paso de trabajo del símbolo del sistema  
 **Para crear un paso de trabajo de CmdExec**  
  
1.  Expanda el **Agente SQL Server**, cree un trabajo o haga clic con el botón derecho en uno existente y, después, haga clic en **Propiedades**. Para obtener más información acerca de cómo crear un trabajo, vea [Crear trabajos](http://msdn.microsoft.com/library/465fb7fc-7622-4252-a178-ea51691c935b).  
  
2.  En el cuadro de diálogo **Propiedades del trabajo** , haga clic en la página **Pasos** y, a continuación, haga clic en **Nuevo**.  
  
3.  En el cuadro de diálogo **Nuevo paso de trabajo** , escriba un nombre para el paso de trabajo en **Nombre del paso**.  
  
4.  En la lista **Tipo** , elija **Sistema operativo (CmdExec)**.  
  
5.  En la lista **Ejecutar como** , seleccione la cuenta e proxy con las credenciales que utilizará el trabajo. De forma predeterminada, los pasos de trabajo de CmdExec se ejecutan en el contexto de la cuenta de servicio de Agente SQL Server.  
  
6.  En el cuadro **Procesar código de salida de un comando correcto** , escriba un valor de 0 a 999999.  
  
7.  En el cuadro **Comando** , escriba powershell.exe con parámetros que especifiquen el script de PowerShell que se va a ejecutar.  
  
8.  Haga clic en la página **Avanzadas** para configurar las opciones del paso de trabajo como, por ejemplo: la acción que se realizará si el paso de trabajo es correcto o si es erróneo, el número de veces que Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intentará ejecutar el paso de trabajo y el archivo en el que Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede escribir la salida del paso de trabajo. Solo los miembros del rol fijo de servidor **sysadmin** pueden escribir la salida de paso de trabajo en un archivo del sistema operativo.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
