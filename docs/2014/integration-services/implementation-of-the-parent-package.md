---
title: Implementación del paquete primario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- parent packages [Integration Services]
ms.assetid: d8f94830-fa27-4151-88df-cbdc6bf0fc80
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2cec1f30ba728f1cf3b808acb2fb362e21d259a4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66058155"
---
# <a name="implementation-of-the-parent-package"></a>Implementación del paquete primario
  Cuando se lleva a cabo el equilibro de carga de paquetes SSIS entre varios servidores, el siguiente paso tras la creación e implementación de los paquetes secundarios, así como la creación de trabajos del Agente SQL Server para ejecutarlos, es crear el paquete primario. El paquete primario contendrá varias tareas Ejecutar trabajo del Agente SQL Server y cada tarea se encarga de llamar a un trabajo del Agente SQL Server que ejecuta uno de los paquetes secundarios. A su vez, las tareas Ejecutar trabajo del Agente SQL Server del paquete primario ejecutan los distintos trabajos del Agente SQL Server. Cada tarea del paquete primario contiene información tal como cómo conectarse al servidor remoto y qué trabajo ejecutar en ese servidor. Para más información, consulte [Execute SQL Server Agent Job Task](control-flow/execute-sql-server-agent-job-task.md).  
  
 Para identificar el paquete primario que ejecuta paquetes secundarios, en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] haga clic con el botón derecho en el paquete en el Explorador de soluciones y, después, haga clic en **Paquete de punto de entrada**.  
  
## <a name="listing-child-packages"></a>Listado de paquetes secundarios  
 Si implementa un proyecto que contiene un paquete primario y uno o varios paquetes secundarios en el servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , puede ver una lista de los paquetes secundarios que ejecuta el paquete primario. Cuando se ejecuta el paquete primario, se genera automáticamente un informe de **información general** para el paquete primario en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. El informe lista los paquetes secundarios ejecutados por la tarea Ejecutar paquete contenida en el paquete primario, como se muestra en la imagen siguiente.  
  
 ![Informe de información general que incluye una lista de los paquetes secundarios](media/overviewreport-childpackagelisting.png "Informe de información general que incluye una lista de los paquetes secundarios")  
  
 Si desea información sobre cómo acceder al informe de **información general** , vea [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md).  
  
## <a name="precedence-constraints-in-the-parent-package"></a>Restricciones de precedencia en el paquete primario  
 Cuando crea restricciones de precedencia entre las tareas Ejecutar trabajo del Agente SQL Server del paquete primario, estas restricciones de precedencia controlan solamente la hora en la que se inician los trabajos del Agente SQL Server en los servidores remotos. Las restricciones de precedencia no pueden recibir información sobre el éxito o error de los paquetes secundarios que se ejecutan a partir de los pasos de los trabajos del Agente SQL Server.  
  
 Esto significa que el éxito o error de un paquete secundario no se propaga al paquete primario, dado que la única función de la tarea Ejecutar trabajo del Agente SQL Server en el paquete primario es solicitar a trabajo del Agente SQL Server que ejecute el paquete secundario. Una vez que la llamada al trabajo del Agente SQL Server es satisfactoria, el paquete primario recibe un resultado de <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success>.  
  
 Un error en este escenario solo significa que ha habido un error en la llamada a la tarea del trabajo del Agente SQL Server remoto. Una situación en la que esto puede ocurrir es cuando el servidor remoto está inactivo y el agente no responde. No obstante, en tanto se active el agente, el paquete primario completa su tarea sin problemas.  
  
> [!NOTE]  
>  Puede usar una tarea Ejecutar SQL que contenga una instrucción Transact-SQL de **sp_start_job N'package_name'**. Para más información, vea [sp_start_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql).  
  
## <a name="debugging-environment"></a>Entorno de depuración  
 Al probar el paquete primario, utilice el entorno de depuración del diseñador ejecutándolo mediante Depurar/Iniciar depuración (F5). También puede usar la utilidad del símbolo del sistema **dtexec**. Para obtener más información, vea [DTExec Utility](packages/dtexec-utility.md).  
  
  
