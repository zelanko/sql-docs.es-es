---
title: Tarea Cola de mensajes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.messagequeuetask.f1
helpviewer_keywords:
- Message Queue task [Integration Services]
- receiving messages
- messages [Integration Services]
- sending messages
ms.assetid: ae1d8fad-6649-4e93-b589-14a32d07da33
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d4a9cc34a1aee631b4b28c6eba845308ac5b2c79
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438272"
---
# <a name="message-queue-task"></a>Message Queue Task
  La tarea Cola de mensajes le permite usar Message Queue Server (que también recibe el nombre de MSMQ) para enviar y recibir mensajes entre paquetes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], o enviar mensajes a una cola de aplicaciones procesada por una aplicación personalizada. Estos mensajes pueden adoptar la forma de texto simple, archivos o variables y sus valores.  
  
 Al utilizar la tarea Cola de mensajes, puede coordinar operaciones en toda la empresa. Los mensajes se pueden colocar en cola y enviarse más tarde si el destino no está disponible o está ocupado. Por ejemplo, la tarea puede colocar en cola mensajes para el equipo portátil sin conexión de los representantes de ventas, que reciben sus mensajes cuando se conectan a la red. Puede usar la tarea Cola de mensajes para los siguientes fines:  
  
-   Retrasar la ejecución de la tarea hasta que hayan entrado otros paquetes. Por ejemplo, en cada punto de venta, después del mantenimiento nocturno, una tarea Cola de mensajes puede enviar un mensaje al equipo corporativo. Un paquete que se ejecuta en el equipo corporativo contiene tareas Cola de mensajes, cada una de las cuales espera el mensaje de un punto de venta específico. Cuando llega un mensaje de un punto de venta, una tarea carga los datos desde ese punto de venta. Una vez han llegado todos los puntos de venta, el paquete calcula los resultados totales.  
  
-   Enviar archivos de datos al equipo que los procesa. Por ejemplo, los resultados de la caja registradora de un restaurante pueden enviarse en un mensaje de archivo de datos al sistema de nóminas corporativo, donde se extraen los datos de las propinas de cada camarero.  
  
-   Distribuir archivos en toda la empresa. Por ejemplo, un paquete puede utilizar una tarea Cola de mensajes para enviar un archivo de paquete a otro equipo. A continuación, un paquete que se ejecuta en el equipo de destino puede utilizar una tarea Cola de mensajes para recuperar y guardar localmente el paquete.  
  
 Al enviar o recibir mensajes, la tarea Cola de mensajes usa uno de estos cuatro tipos de mensajes: archivo de datos, cadena, mensaje de cadena para variable o variable. El tipo de mensaje Mensaje de cadena para variable solamente se puede usar al recibir mensajes.  
  
 La tarea usa el administrador de conexiones MSMQ para conectarse a una cola de mensajes. Para más información, vea [Administrador de conexiones MSMQ](../connection-manager/msmq-connection-manager.md). Para obtener más información acerca de Message Queue Server, vea [MSDN Library](https://go.microsoft.com/fwlink/?LinkId=7022).  
  
 La tarea Cola de mensajes exige que se instale el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Algunos componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que puede seleccionar para su instalación en la página **Componentes para instalar** o **Selección de características** del Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalan un subconjunto parcial de componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Estos componentes resultan útiles para tareas específicas, pero la funcionalidad de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] estará limitada. Por ejemplo, la opción [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] instala los componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que se necesitan para diseñar un paquete, pero no se instala el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y, por tanto, la tarea Cola de mensajes no es funcional. Para garantizar la instalación completa de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], debe seleccionar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en la página **Componentes para instalar** . Para más información sobre cómo instalar y ejecutar la tarea Cola de mensajes, vea [Instalar Integration Services](../install-windows/install-integration-services.md).  
  
> [!NOTE]  
>  La tarea Cola de mensajes no cumple el estándar federal de procesamiento de información (FIPS, Federal Information Processing Standard) 140-2 cuando el sistema operativo del equipo se configura en modo FIPS y la tarea usa cifrado. Si la tarea Cola de mensajes no usa cifrado, se puede ejecutar la tarea correctamente.  
  
## <a name="message-types"></a>Tipos de mensajes  
 Puede configurar los tipos de mensaje que proporciona la tarea Cola de mensajes de las siguientes maneras:  
  
-   El mensaje `Data file` especifica que un archivo contiene el mensaje. Al recibir mensajes, puede configurar la tarea para guardar el archivo, sobrescribir un archivo existente y especificar el paquete desde el cual la tarea puede recibir mensajes.  
  
-   El mensaje `String` especifica el mensaje como una cadena. Al recibir mensajes, puede configurar la tarea para comparar la cadena recibida con una cadena definida por el usuario y actuar según la comparación. La comparación de cadenas puede ser exacta, distinguir o no entre mayúsculas y minúsculas o usar una subcadena.  
  
-   `String message to variable` especifica el mensaje de origen como una cadena que se envía a una variable de destino. Puede configurar la tarea para comparar la cadena recibida con una cadena definida por el usuario aplicando una comparación exacta, que no distinga entre mayúsculas y minúsculas o de subcadena. Este tipo de mensaje está disponible solamente cuando la tarea recibe mensajes.  
  
-   `Variable` especifica que el mensaje contiene una o más variables. Puede configurar la tarea para especificar los nombres de las variables que se incluyen en el mensaje. Al recibir mensajes, puede configurar la tarea para especificar el paquete desde el cual se pueden recibir mensajes y la variable que es el destino del mensaje.  
  
## <a name="sending-messages"></a>enviar mensajes  
 Cuando configure la tarea Cola de mensajes para enviar mensajes, puede utilizar uno de los algoritmos de cifrado actualmente compatibles con tecnología de Message Queue Server, RC2 y RC4, para cifrar el mensaje. Ambos algoritmos de cifrado se consideran ahora criptográficamente menos seguros que algoritmos más recientes con los que aún no es compatible la tecnología de Message Queue Server. Por tanto, debe considerar con detenimiento sus necesidades criptográficas a la hora de enviar mensajes con la tarea Cola de mensajes.  
  
## <a name="receiving-messages"></a>recibir mensajes  
 Al recibir mensajes, la tarea Cola de mensajes se puede configurar de las siguientes maneras:  
  
-   Omitir el mensaje o eliminar el mensaje de la cola.  
  
-   Especificar un tiempo de espera.  
  
-   Generar un error cuando se agota el tiempo de espera.  
  
-   Sobrescribir un archivo existente, si el mensaje se guarda en un `Data file`.  
  
-   Guardar el archivo de mensajes con un nombre de archivo diferente, si el mensaje usa el tipo `Data file message`.  
  
## <a name="custom-logging-messages-available-on-the-message-queue-task"></a>Mensajes de registro personalizados disponibles en la tarea Cola de mensajes  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Cola de mensajes. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) y [Mensajes personalizados para registro](../custom-messages-for-logging.md).  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`MSMQAfterOpen`|Indica que la tarea finalizó la apertura de la cola de mensajes.|  
|`MSMQBeforeOpen`|Indica que la tarea inició la apertura de la cola de mensajes.|  
|`MSMQBeginReceive`|Indica que la tarea comenzó a recibir un mensaje.|  
|`MSMQBeginSend`|Indica que la tarea comenzó a enviar un mensaje.|  
|`MSMQEndReceive`|Indica que la tarea finalizó la recepción de un mensaje.|  
|`MSMQEndSend`|Indica que la tarea finalizó el envío de un mensaje.|  
|`MSMQTaskInfo`|Proporciona información descriptiva sobre la tarea.|  
|`MSMQTaskTimeOut`|Indica que se superó el tiempo de espera de la tarea.|  
  
## <a name="configuration-of-the-message-queue-task"></a>Configuración de la tarea Cola de mensajes  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación. Para obtener información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea Cola de mensajes &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor de la tarea Cola de mensajes &#40;página Recibir&#41;](../message-queue-task-editor-receive-page.md)  
  
-   [Editor de la tarea Cola de mensajes &#40;página Enviar&#41;](../message-queue-task-editor-send-page.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener información sobre cómo establecer estas propiedades mediante programación, vea la documentación de la clase **Microsoft.SqlServer.Dts.Tasks.MessageQueueTask.MessageQueueTask** en la Guía del desarrollador.  
  
## <a name="related-tasks"></a>Related Tasks  
 Para más información sobre cómo establecer estas propiedades en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md).  
  
## <a name="see-also"></a>Consulte también  
 [Tareas de Integration Services](integration-services-tasks.md)   
 [Flujo de control](control-flow.md)  
  
  
