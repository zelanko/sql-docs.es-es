---
title: Implementación de paquetes secundarios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- child packages
ms.assetid: ab0c09d7-ce2e-487d-a1ed-a4b5adb6cc01
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7390434b1565c64b63e62c89d1e61b13f18cd6a6
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965715"
---
# <a name="implementation-of-child-packages"></a>Implementación de paquetes secundarios
  Cuando implementa el equilibrio de carga mediante [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], los paquetes secundarios se instalan en otros servidores para aprovechar el tiempo de servidor o CPU disponible. Para crear y ejecutar los paquetes secundarios, es necesario realizar los pasos siguientes:  
  
-   Diseñar los paquetes secundarios.  
  
-   Mover los paquetes al servidor remoto.  
  
-   Crear un trabajo del Agente SQL Server en el servidor remoto que contenga un paso que ejecute el paquete secundario.  
  
-   Probar y depurar el trabajo del Agente SQL Server y los paquetes secundarios.  
  
 Cuando diseñe los paquetes secundarios, puesto que no hay ningún límite establecido para el diseño, podrá incluir la funcionalidad que desee. Sin embargo, si el paquete tiene acceso a datos, debe asegurarse de que el servidor que ejecuta el paquete tenga acceso a los datos.  
  
 Para identificar el paquete primario que ejecuta paquetes secundarios, en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] haga clic con el botón derecho en el paquete en el Explorador de soluciones y, después, haga clic en **Paquete de punto de entrada**.  
  
 Una vez diseñados los paquetes secundarios, el próximo paso es implementarlos en los servidores remotos.  
  
## <a name="moving-the-child-package-to-the-remote-instance"></a>Mover el paquete secundario a la instancia remota  
 Existen varias formas de mover paquetes a otros servidores. Los dos métodos sugeridos son:  
  
-   Exportar paquetes mediante [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
-   Implementar paquetes generando una utilidad de implementación para el proyecto que contiene los paquetes que desea implementar y, a continuación, ejecutar el Asistente para la instalación de paquetes para instalar los paquetes en el sistema de archivos o en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener más información, vea [implementación de paquetes &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md).  
  
 Debe repetir la implementación con cada servidor remoto que desee utilizar.  
  
## <a name="creating-the-sql-server-agent-jobs"></a>Crear trabajos del Agente SQL Server  
 Una vez que se hayan implementado los paquetes secundarios en los distintos servidores, cree un trabajo del Agente SQL Server en cada servidor que contenga un paquete secundario. El trabajo del Agente SQL Server incluye un paso que ejecuta el paquete secundario cuando se llama al agente del trabajo. Los trabajos del Agente SQL Server no son trabajos programados, sino que ejecutan paquetes secundarios únicamente cuando los llama un paquete primario. La notificación del éxito o fracaso del trabajo que se devuelve al paquete primario refleja el éxito o fracaso del trabajo del Agente SQL Server y si la llamada fue satisfactoria, no el éxito o fracaso del paquete secundario o si éste se ejecutó.  
  
## <a name="debugging-the-sql-server-agent-jobs-and-child-packages"></a>Depurar los trabajos del Agente SQL Server y los paquetes secundarios  
 Puede probar los trabajos del Agente SQL Server y sus paquetes secundarios a través de uno de los métodos siguientes:  
  
-   Ejecutar cada paquete secundario en el diseñador SSIS haciendo clic en **depurar**  /  **iniciar sin depurar**.  
  
-   Ejecutar el trabajo individual del Agente SQL Server en el equipo remoto a través de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], para asegurarse de que el paquete se ejecuta.  
  
 Para obtener información sobre cómo solucionar problemas de los paquetes que se ejecutan desde trabajos del Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , vea el artículo acerca de [un paquete de SSIS no se ejecuta al llamarlo desde un paso de trabajo del Agente SQL Server](https://support.microsoft.com/kb/918760) en Support Knowledge Base de [!INCLUDE[msCoName](../includes/msconame-md.md)] .  
  
 El Agente SQL Server comprueba el acceso al subsistema de un proxy y da acceso al proxy cada vez que se ejecuta el paso de trabajo.  
  
 Puede crear un proxy en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Ejecutar un paquete en el servidor SSIS con SQL Server Management Studio](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Entrada de blog, [SSIS: acceso a variables en un paquete primario](https://andyleonard.blog/2015/08/ssis-design-pattern-access-parent-variables-from-a-child-package-in-the-ssis-catalog/), en andyleonard. blog.  
  
-   Artículo, [tarea ejecutar paquete](../integration-services/control-flow/execute-package-task.md).  
  
  
