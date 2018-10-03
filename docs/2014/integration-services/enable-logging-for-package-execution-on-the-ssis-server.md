---
title: Habilitar el registro de ejecución del paquete en el servidor SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 8930c63c-bc6f-46c2-b428-b3c29ee89a7d
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c6d1d614ee66731a24355a918678226dcc54ae35
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48201655"
---
# <a name="enable-logging-for-package-execution-on-the-ssis-server"></a>Habilitar el registro para la ejecución de paquetes en el servidor SSIS
  En este procedimiento se describe cómo establecer o cambiar el nivel de registro para un paquete cuando se ejecuta un paquete que ha implementado en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. El nivel de registro que se establece al ejecutar el paquete invalida el registro de paquete configurado mediante [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Vea [Habilitar el registro de paquetes en SQL Server Data Tools](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md) para obtener más información.  
  
 Para especificar el nivel de registro, puede usar uno de los métodos siguientes. En este tema se trata el primer método.  
  
-   Configurar una instancia de una ejecución de paquetes mediante el cuadro de diálogo Ejecutar paquete  
  
-   Configurar parámetros para una instancia de una ejecución mediante [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)  
  
-   Configurar un trabajo del Agente SQL Server para una ejecución de paquetes mediante el cuadro de diálogo Nuevo paso de trabajo.  
  
### <a name="to-set-the-logging-level-for-a-package-by-using-the-execute-package-dialog-box"></a>Para establecer el nivel de registro de un paquete mediante el cuadro de diálogo Ejecutar paquete  
  
1.  En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], navegue hasta el paquete en el Explorador de objetos.  
  
2.  Haga clic con el botón derecho en el paquete y seleccione **Ejecutar**.  
  
3.  Seleccione la pestaña **Avanzadas** en el cuadro de diálogo **Ejecutar paquete** .  
  
4.  En **Nivel de registro**, seleccione el nivel de registro. Vea la tabla siguiente para obtener una descripción de los valores disponibles.  
  
5.  Complete otras configuraciones de paquetes que desee y haga clic en **Aceptar** para ejecutar el paquete.  
  
 Están disponibles los niveles de registro siguientes.  
  
|Nivel de registro|Descripción|  
|-------------------|-----------------|  
|None|El registro está desactivado. Solo se registra el estado de ejecución del paquete.|  
|Básico|Se registran todos los eventos, excepto los eventos personalizados y de diagnóstico. Este es el valor predeterminado.|  
|Rendimiento|Solo se registran las estadísticas de rendimiento, y los eventos OnError y OnWarning.<br /><br /> El informe **Rendimiento de la ejecución** muestra el Tiempo activo y el TIempo total para los componentes de flujo de datos del paquete. Esta información está disponible cuando el nivel de registro de la última ejecución del paquete se estableció en **Performance** (Rendimiento) o **Verbose**(Detallado). Para obtener más información, consulte [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md).<br /><br /> La vista [catalog.execution_component_phases](/sql/integration-services/system-views/catalog-execution-component-phases) muestra las horas de inicio y de finalización de los componentes de flujo de datos, para cada fase de una ejecución. Esta vista muestra esta información para estos componentes solo cuando el nivel de registro de la ejecución del paquete se estableció en **Rendimiento** o en **Detallado**.|  
|Verbose|Se registran todos los eventos, incluidos los eventos personalizados y de diagnóstico.<br /><br /> Un ejemplo de un evento de diagnóstico es el evento de DiagnosticEx. Siempre que una tarea Ejecutar paquete ejecuta un paquete secundario, registra este evento. El mensaje de evento consta de los valores de los parámetros pasados a los paquetes secundarios<br /><br /> El valor de la columna de mensaje para DiagnosticEx es texto XML. . Para ver el texto del mensaje de una ejecución de paquete, ejecute una consulta en la vista [catalog.operation_messages &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database).<br /><br /> Nota: Los eventos personalizados incluyen los eventos registrados por [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] tareas. Para más información, vea [Custom Messages for Logging](../../2014/integration-services/custom-messages-for-logging.md).<br /><br /> La vista [catalog.execution_data_statistics](../relational-databases/statistics/statistics.md) muestra una fila cada vez que un componente de flujo de datos envía datos a un componente de nivel inferior para una ejecución del paquete. El nivel de registro se debe establecer en **Detallado** para capturar esta información en la vista.|  
  
## <a name="see-also"></a>Vea también  
 [Servicios de integración &#40;SSIS&#41; registro](performance/integration-services-ssis-logging.md)   
 [Habilitar el registro de paquetes en SQL Server Data Tools](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)  
  
  
