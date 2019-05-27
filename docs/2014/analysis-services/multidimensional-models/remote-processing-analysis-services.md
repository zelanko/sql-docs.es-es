---
title: Remoto de procesamiento (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d58bcb3c-0b3f-4ab0-81eb-4fdcc86153af
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b383621408cc84a65e5f9c5adb711dd9f047be64
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66073208"
---
# <a name="remote-processing-analysis-services"></a>Procesamiento remoto (Analysis Services)
  Puede ejecutar el procesamiento programado o desatendido en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] remota, donde la solicitud de procesamiento se origina en un equipo, pero se ejecuta en otro equipo de la misma red.  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Si ejecuta versiones diferentes de SQL Server en cada equipo, las bibliotecas de cliente deben coincidir con la versión de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que está procesando el modelo. Por ejemplo, si el procesamiento se ejecuta en una instancia de [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] , el equipo desde el que se origina la solicitud debe tener la biblioteca de cliente correspondiente para [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]. Vea [Proveedores de datos usados para conexiones de Analysis Services](../instances/data-providers-used-for-analysis-services-connections.md).  
  
-   En el servidor remoto, la opción **Permitir conexiones remotas a este equipo** debe estar habilitada y la cuenta que emite la solicitud de procesamiento debe aparecer como un usuario permitido.  
  
-   Deben configurarse reglas de firewall de Windows para permitir conexiones entrantes a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Compruebe que puede conectarse a la instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Consulte [Configure the Windows Firewall to Allow Analysis Services Access](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
-   Resuelva los errores de procesamiento local existente antes de intentar ejecutar el procesamiento remoto. Compruebe que, si la solicitud de procesamiento es local, los datos se puedan recuperar correctamente desde el origen de datos relacional externo. Vea [Establezca las opciones de suplantación &#40;SSAS - multidimensional&#41;](set-impersonation-options-ssas-multidimensional.md) para obtener instrucciones sobre cómo especificar las credenciales que se han usado para recuperar los datos.  
  
## <a name="on-demand-remote-processing"></a>Procesamiento remoto a petición  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] acepta las solicitudes de procesamiento de las cuentas de usuario o de aplicación que tienen permisos de administrador de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Si es administrador, compruebe que puede conectarse a la instancia remota y procesar la base de datos manualmente a través de la conexión remota.  
  
1.  En el equipo que se usará para programar el procesamiento, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y conéctese a la instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  Haga clic con el botón derecho en la base de datos, seleccione **Proceso**, señale **Script** y elija **Generar script de acción en ventana Nueva consulta**. Los comandos que se usan para invocar el procesamiento aparecerán en la ventana de consulta.  
  
3.  Haga clic en **Aceptar** para iniciar el procesamiento.  
  
     La finalización correcta de esta tarea proporciona una consulta XMLA que se puede incrustar en un trabajo programado. También confirma que no haya ningún problema de conexión.  
  
## <a name="schedule-remote-processing-using-sql-server-agent-service"></a>Programar el procesamiento remoto mediante el servicio del Agente SQL Server  
 De forma predeterminada, el servicio del Agente SQL Server se ejecuta bajo una cuenta virtual con conexiones de red realizadas mediante la cuenta de equipo. Para evitar tener que conceder derechos de administración de una cuenta de equipo en la instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , debe cambiar la cuenta de servicio del Agente SQL Server para que se ejecute como una cuenta de usuario de dominio con privilegios mínimos.  
  
 Asegúrese de que concede todos los permisos necesarios, incluidos los de la cuenta **sysadmin** en la instancia del motor de base de datos que proporciona el servicio.  
  
 Use los siguientes vínculos para establecer permisos:  
  
-   [Configurar el Agente SQL Server](../../ssms/agent/configure-sql-server-agent.md)  
  
-   [SQL Server Agent Components](../../ssms/agent/sql-server-agent.md#Components) sugiere roles fijos de servidor alternativo si la concesión de permisos de **sysadmin** no es posible.  
  
 Una vez configurados los permisos de cuenta, continúe con estos pasos.  
  
#### <a name="grant-the-sql-server-agent-account-administrator-permission-on-ssas"></a>Conceder permiso de administrador de cuenta del Agente SQL Server en SSAS  
  
1.  Mediante [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], conéctese a la instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  Haga clic con el botón derecho en el nombre del servidor, haga clic en**Propiedades**y, después, en **Seguridad**.  
  
3.  Haga clic en **Agregar** para agregar la cuenta del Agente SQL Server.  
  
#### <a name="create-the-job"></a>Crear el trabajo  
  
1.  En Management Studio, conéctese a la instancia del motor de base de datos. El Agente SQL Server es el último elemento en el Explorador de objetos. Si es necesario, inicie el servicio.  
  
2.  Haga clic con el botón derecho en **Trabajos**, en **Nuevo trabajo** y, después, especifique un nombre.  
  
3.  En los pasos, haga clic en **Nuevo** y especifique un nombre.  
  
4.  En Tipo, seleccione **Comando de SQL Server Analysis Services**.  
  
5.  En Servidor, escriba el nombre de la instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
6.  En Comando, pegue el comando XMLA para procesar la base de datos. Se trata del script de XMLA que generó en el paso de comprobación para el procesamiento remoto a petición. Haga clic en **Aceptar** para guardar el trabajo.  
  
#### <a name="start-sql-server-profiler"></a>Iniciar SQL Server Profiler  
  
1.  En el equipo remoto, inicie SQL Server Profiler. Conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y haga clic en **Ejecutar** para iniciar el seguimiento de los eventos predeterminados.  
  
     Usará SQL Server Profiler para supervisar los eventos de procesamiento a medida que se produzcan.  
  
2.  De manera opcional, puede establecer propiedades de seguimiento para enviar el seguimiento a un archivo o una tabla de una base de datos.  
  
#### <a name="run-the-job"></a>Ejecutar el trabajo  
  
1.  En el equipo que se usa para ejecutar el trabajo, compruebe que el trabajo puede realizar la operación básica. En el Explorador de objetos, en el Agente SQL Server, amplíe **Trabajos**, haga clic con el botón derecho en el trabajo que acaba de crear y, después, en **Iniciar trabajo en el paso**. El trabajo se inicia inmediatamente. Puede supervisar el progreso en SQL Server Profiler.  
  
2.  Como paso final, modifique el trabajo para que se ejecute según una programación definida y agregue las alertas o las notificaciones necesarias para administrar el trabajo. También podría ser conveniente ajustar el script de procesamiento o crear varios pasos en el trabajo para procesar objetos de forma independiente.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Agent Components](../../ssms/agent/sql-server-agent.md#Components)   
 [Programar tareas administrativas de SSAS con el Agente SQL Server](../instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)   
 [Procesamiento por lotes &#40;Analysis Services&#41;](batch-processing-analysis-services.md)   
 [Procesamiento de objetos de modelo multidimensional](processing-a-multidimensional-model-analysis-services.md)   
 [Procesar objetos &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)  
  
  
