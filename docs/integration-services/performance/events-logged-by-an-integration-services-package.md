---
title: Eventos registrados por un paquete de Integration Services | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- package [Integration Services], events
- events [Integration Services], package
ms.assetid: 55a0951a-46f3-4f0f-9972-74cec9cc26b7
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 30cec734f1bf60180475e1bebc6b8c66c7686bf5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="events-logged-by-an-integration-services-package"></a>Eventos registrados por un paquete de Integration Services
  Los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] registran mensajes de eventos en el registro de eventos de aplicación Windows. Los paquetes registran estos mensajes cuando se inician, cuando se detienen y cuando se producen ciertos problemas.  
  
 En este tema, se proporciona información sobre los mensajes de eventos comunes que un paquete registra en el registro de eventos de aplicación. De forma predeterminada, los paquetes registran algunos de estos mensajes aunque no se haya habilitado el registro en ellos. Sin embargo, hay otros mensajes que solo se registran si se ha habilitado dicho registro. Con independencia de si el paquete registra de forma predeterminada estos mensajes, o porque se haya habilitado el registro, el origen del evento de los mensajes es SQLISPackage.  
  
 Para información sobre cómo ejecutar paquetes de SSIS, consulte [Ejecución de proyectos y paquetes](../packages/run-integration-services-ssis-packages.md).  
  
 Para obtener información sobre cómo solucionar problemas de ejecución de paquetes, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="messages-about-the-status-of-the-package"></a>Mensajes sobre el estado del paquete  
 Al ejecutar un paquete [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , el paquete suele registrar diversos mensajes sobre su progreso y su estado. En la tabla siguiente se muestran estos mensajes.  
  
> [!NOTE]  
>  El paquete registrará los mensajes de la tabla siguiente aunque no se haya habilitado el registro.  
  
|Identificador del evento|Nombre simbólico|Texto|Notas|  
|--------------|-------------------|----------|-----------|  
|12288|DTS_MSG_PACKAGESTART|Se ha iniciado el paquete "".|El paquete ha comenzado a ejecutarse.|  
|12289|DTS_MSG_PACKAGESUCCESS|El paquete "" finalizó correctamente.|El paquete se ha ejecutado correctamente y ya no está ejecutándose.|  
|12290|DTS_MSG_PACKAGECANCEL|El paquete "%1!s!" se ha cancelado.|El paquete ya no se está ejecutando porque se ha cancelado.|  
|12291|DTS_MSG_PACKAGEFAILURE|Error en el paquete "".|El paquete no se ha podido ejecutar correctamente y ha dejado de ejecutarse.|  
  
 De forma predeterminada, en una instalación nueva, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se configura para no incluir en el registro de eventos de aplicación ciertos eventos relacionados con la ejecución de paquetes. Esta configuración evita que se generen demasiadas entradas en el registro de eventos al utilizar la característica de recopilador de datos de la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Los eventos que no se registran son EventID 12288, "Se ha iniciado el paquete" y EventID 12289, "El paquete finalizó correctamente". Para registrar estos eventos en el registro de eventos de aplicación, abra el Registro para editarlo. A continuación, en el Registro, busque el nodo HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS y cambie el valor DWORD de la opción LogPackageExecutionToEventLog de 0 a 1. Sin embargo, en una instalación de actualización, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se configura para registrar estos dos eventos. Para deshabilitar el registro, cambie el valor de la opción LogPackageExecutionToEventLog de 1 a 0.  
  
## <a name="messages-associated-with-package-logging"></a>Mensajes asociados al registro de paquetes  
 Si ha habilitado el registro en el paquete, el registro de eventos de aplicación es uno de los destinos admitidos por las características de registro opcionales en los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
 Si ha habilitado el registro en el paquete y la ubicación es el registro de eventos de aplicación, el paquete registrará las entradas relacionadas con la información siguiente:  
  
-   Mensajes sobre la fase en la que se encuentra el paquete mientras se ejecuta.  
  
-   Mensajes sobre eventos concretos que se producen mientras el paquete se ejecuta.  
  
### <a name="messages-about-the-stages-of-package-execution"></a>Mensajes sobre las fases de ejecución del paquete  
  
|Identificador del evento|Nombre simbólico|Texto|Notas|  
|--------------|-------------------|----------|-----------|  
|12544|DTS_MSG_EVENTLOGENTRY|Nombre de evento: %1%r Mensaje: %9%r Operador: %2%r Nombre de origen: %3%r Id. de origen: %4%r Id. de ejecución: %5%r Hora de inicio: %6%r Hora de finalización: %7%r Código de datos: %8|Cuando se configura el registro de paquetes en el registro de eventos de aplicación, varios mensajes usan este formato genérico.|  
|12556|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|Nombre de evento: %1%r Mensaje: %9%r Operador: %2%r Nombre de origen: %3%r Id. de origen: %4%r Id. de ejecución: %5%r Hora de inicio: %6%r Hora de finalización: %7%r Código de datos: %8|El paquete se ha iniciado.|  
|12547|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|Nombre de evento: %1%r Mensaje: %9%r Operador: %2%r Nombre de origen: %3%r Id. de origen: %4%r Id. de ejecución: %5%r Hora de inicio: %6%r Hora de finalización: %7%r Código de datos: %8|La validación del objeto está a punto de comenzar.|  
|12548|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|Nombre de evento: %1%r Mensaje: %9%r Operador: %2%r Nombre de origen: %3%r Id. de origen: %4%r Id. de ejecución: %5%r Hora de inicio: %6%r Hora de finalización: %7%r Código de datos: %8|La validación del objeto ha finalizado.|  
|12552|DTS_MSG_EVENTLOGENTRY_PROGRESS|Nombre de evento: %1%r Mensaje: %9%r Operador: %2%r Nombre de origen: %3%r Id. de origen: %4%r Id. de ejecución: %5%r Hora de inicio: %6%r Hora de finalización: %7%r Código de datos: %8|Este mensaje genérico informa acerca del progreso del paquete.|  
|12546|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|Nombre de evento: %1%r Mensaje: %9%r Operador: %2%r Nombre de origen: %3%r Id. de origen: %4%r Id. de ejecución: %5%r Hora de inicio: %6%r Hora de finalización: %7%r Código de datos: %8|El objeto ha finalizado su trabajo.|  
|12557|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|Nombre de evento: %1%r Mensaje: %9%r Operador: %2%r Nombre de origen: %3%r Id. de origen: %4%r Id. de ejecución: %5%r Hora de inicio: %6%r Hora de finalización: %7%r Código de datos: %8|El paquete ha terminado de ejecutarse.|  
  
### <a name="messages-about-events-that-occur"></a>Mensajes sobre los eventos que se producen  
 En la tabla siguiente, se muestran solo algunos de los mensajes generados por eventos. Para consultar una lista más completa de los mensajes de error, advertencia e información que usa [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , vea [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md).  
  
|Identificador del evento|Nombre simbólico|Texto|Notas|  
|--------------|-------------------|----------|-----------|  
|12251|DTS_MSG_EVENTLOGENTRY_TASKFAILED|Nombre de evento: %1%r Mensaje: %9%r Operador: %2%r Nombre de origen: %3%r Id. de origen: %4%r Id. de ejecución: %5%r Hora de inicio: %6%r Hora de finalización: %7%r Código de datos: %8|Error en la tarea.|  
|12250|DTS_MSG_EVENTLOGENTRY_ERROR|Nombre de evento: %1%r Mensaje: %9%r Operador: %2%r Nombre de origen: %3%r Id. de origen: %4%r Id. de ejecución: %5%r Hora de inicio: %6%r Hora de finalización: %7%r Código de datos: %8|Este mensaje informa de que se ha producido un error.|  
|12249|DTS_MSG_EVENTLOGENTRY_WARNING|Nombre de evento: %1%r Mensaje: %9%r Operador: %2%r Nombre de origen: %3%r Id. de origen: %4%r Id. de ejecución: %5%r Hora de inicio: %6%r Hora de finalización: %7%r Código de datos: %8|Este mensaje informa de que se ha producido una advertencia.|  
|12258|DTS_MSG_EVENTLOGENTRY_INFORMATION|Nombre de evento: %1%r Mensaje: %9%r Operador: %2%r Nombre de origen: %3%r Id. de origen: %4%r Id. de ejecución: %5%r Hora de inicio: %6%r Hora de finalización: %7%r Código de datos: %8|La información de este mensaje no está asociada a ningún error ni a ninguna advertencia.|  

## <a name="view-log-entries-in-the-log-events-window"></a>Ver entradas del registro en la ventana Registrar eventos
  En este procedimiento se describe cómo ejecutar un paquete y ver las entradas de registro que escribe. Se pueden ver las entradas del registro en tiempo real. Las entradas del registro escritas en la ventana **Registrar eventos** también se pueden copiar y guardar para futuros análisis.  
  
 No es necesario escribir las entradas en un registro para que se escriban en la ventana **Registrar eventos** .  
  
### <a name="to-view-log-entries"></a>Para ver entradas del registro  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el menú **SSIS** , haga clic en **Registrar eventos**. Opcionalmente, se puede mostrar la ventana **Registrar eventos** asignando el comando View.LogEvents a una combinación de teclas elegida por el usuario en la página **Teclado** del cuadro de diálogo **Opciones** .  
  
3.  En el menú **Depurar** , haga clic en **Iniciar depuración**.  
  
     A medida que el tiempo de ejecución encuentra eventos y mensajes personalizados que están habilitados para el registro, las entradas del registro para cada evento o mensaje se escriben en la ventana **Registrar eventos** .  
  
4.  En el menú **Depurar** , haga clic en **Detener depuración**.  
  
     Las entradas del registro permanecen disponibles en la ventana **Registrar eventos** hasta que vuelve a ejecutar el paquete, ejecuta un paquete diferente o cierra [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
5.  Vea las entradas del registro en la ventana **Registrar eventos** .  
  
6.  También puede hacer clic en las entradas del registro que quiere copiar, hacer clic con el botón derecho y luego hacer clic en **Copiar**.  
  
7.  O bien, puede hacer doble clic en una entrada del registro y, en el cuadro de diálogo **Entrada del registro** , ver los detalles de una única entrada.  
  
8.  En el cuadro de diálogo **Entrada del registro** , haga clic en las flechas arriba y abajo para mostrar la entrada del registro anterior o siguiente, y haga clic en el icono de copiar para copiar la entrada del registro.  
  
9. Abra un editor de texto, pegue y luego guarde la entrada del registro en un archivo de texto.
