---
title: Tarea Transferir mensajes de error | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transfererrormessagestask.f1
- sql13.dts.designer.transfererrormessagestask.general.f1
- sql13.dts.designer.transfererrormessagestask.errormessages.F1
helpviewer_keywords:
- Transfer Error Messages task [Integration Services]
ms.assetid: da702289-035a-4d14-bd74-04461fbfee1b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c189be4aa134ee15314571008ed29a3f53c467d2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518786"
---
# <a name="transfer-error-messages-task"></a>Tarea Transferir mensajes de error
  La tarea Transferir mensajes de error transfiere uno o más mensajes de error definidos por el usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los mensajes definidos por el usuario son mensajes con un identificador igual o mayor que 50000. Los mensajes con un identificador menor que 50000 son mensajes de error del sistema, y no se pueden transferir mediante la tarea Transferir mensajes de error.  
  
 La tarea Transferir mensajes de error se puede configurar para que transfiera todos los mensajes de error o solo los mensajes de error especificados. Los mensajes de error definidos por el usuario pueden estar disponibles en distintos idiomas y la tarea se puede configurar para que transfiera únicamente los mensajes que estén en los idiomas seleccionados. Debe existir una versión en us_english del mensaje que utiliza página de códigos 1033 en el servidor de destino para poder transferir versiones en otros idiomas del mensaje a ese servidor.  
  
 La tabla sysmessages de la base de datos maestra contiene todos los mensajes de error, tanto los del sistema como los definidos por el usuario, que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Es posible que los mensajes definidos por el usuario que desea transferir ya existan en el destino. Un mensaje de error se define como un mensaje de error duplicado si el identificador y el idioma son iguales. La tarea Transferir mensajes de error se puede configurar para haga lo siguiente con los mensajes de error existentes:  
  
-   Sobrescribir los mensajes de error existentes.  
  
-   Hacer que la tarea genere un error cuando existan mensajes duplicados.  
  
-   Omitir los mensajes de error duplicados.  
  
 Durante la ejecución, la tarea Transferir mensajes de error se conecta con los servidores de origen y de destino utilizando uno o dos administradores de conexión SMO. El administrador de conexiones SMO se configura independientemente de la tarea Transferir mensajes de error y después se hace referencia a él en la tarea Transferir mensajes de error. El administrador de conexiones SMO especifica el servidor y el modo de autenticación que se utiliza para tener acceso al servidor. Para más información, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 La tarea Transferir mensajes de error admite un origen y un destino que sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No hay restricciones respecto a qué versión hay que usar como origen o como destino.  
  
## <a name="events"></a>Eventos  
 La tarea genera un evento de información que indica el número de mensajes de error transferidos.  
  
 La tarea Transferir mensajes de error no indica el progreso incremental de la transferencia de mensajes de error; solo indica 0% y 100%.  
  
## <a name="execution-value"></a>Valor de ejecución  
 El valor de ejecución, que se define en la propiedad **ExecutionValue** de la tarea, devuelve el número de mensajes de error transferidos. Si asigna una variable definida por el usuario a la propiedad **ExecValueVariable** de la tarea Transferir mensajes de error, puede hacer que la información de la transferencia del mensaje de error esté disponible para otros objetos del paquete. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) y [Usar variables en paquetes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Entradas del registro  
 La tarea Transferir mensajes de error incluye las siguientes entradas del registro personalizadas:  
  
-   TransferErrorMessagesTaskStartTransferringObjects    Esta entrada del registro indica que se ha iniciado la transferencia. La entrada del registro incluye la hora de inicio.  
  
-   TransferErrorMessagesTaskFinishedTransferringObjects   Esta entrada del registro indica que ha finalizado la transferencia. La entrada del registro incluye la hora de finalización.  
  
 Además, una entrada del registro para el evento **OnInformation** indica el número de mensajes de error transferidos, y se escribe una entrada del registro para el evento **OnWarning event** por cada mensaje de error que se sobrescribe en el destino.  
  
## <a name="security-and-permissions"></a>Seguridad y permisos  
 Para crear mensajes de error, el usuario que ejecuta el paquete debe ser miembro de los roles sysadmin o serveradmin en el servidor de destino.  
  
## <a name="configuration-of-the-transfer-error-messages-task"></a>Configuración de la tarea Transferir mensajes de error  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferErrorMessagesTask.TransferErrorMessagesTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-error-messages-task-editor-general-page"></a>Editor de la tarea Transferir mensajes de error (página General)
  Utilice la página **General** del cuadro de diálogo **Editor de la tarea Transferir mensajes de error** para nombrar y describir la tarea Transferir mensajes de error. La tarea Transferir mensajes de error transfiere uno o más mensajes de error definidos por el usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].   
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Escriba un nombre único para la tarea Transferir mensajes de error. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Transferir mensajes de error.  
  
## <a name="transfer-error-messages-task-editor-messages-page"></a>Editor de la tarea Transferir mensajes de error (página Mensajes)
  Use la página **Mensajes** del cuadro de diálogo **Editor de la tarea Transferir mensajes de error** para especificar propiedades para copiar uno o varios mensajes de error definidos por el usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otra. 
  
### <a name="options"></a>Opciones  
 **SourceConnection**  
 Seleccione un administrador de conexiones SMO de la lista, o bien haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de origen.  
  
 **DestinationConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de destino.  
  
 **IfObjectExists**  
 Seleccione si la tarea debe sobrescribir mensajes de error definidos por el usuario existentes, omitir mensajes existentes o generar un error si existen ya mensajes de error con el mismo nombre en el servidor de destino.  
  
 **TransferAllErrorMessages**  
 Seleccione si la tarea debe copiar todos los mensajes definidos por el usuario o solo los especificados del servidor de origen al de destino.  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**True**|Copiar todos los mensajes definidos por el usuario.|  
|**False**|Copiar solo los mensajes definidos por el usuario especificados.|  
  
 **ErrorMessagesList**  
 Haga clic en el botón Examinar **(…)** para seleccionar los mensajes de error que quiera copiar.  
  
> [!NOTE]  
>  Para poder seleccionar los mensajes de error que se van a copiar, debe especificar el parámetro **SourceConnection** .  
  
 **ErrorMessageLanguagesList**  
 Haga clic en el botón Examinar **(…)** para seleccionar los idiomas para los que se van a copiar mensajes de error definidos por el usuario al servidor de destino. Debe existir una versión en us_english (página de códigos 1033) del mensaje en el servidor de destino para poder transferir versiones en otros idiomas del mensaje a ese servidor.  
  
> [!NOTE]  
>  Para poder seleccionar los mensajes de error que se van a copiar, debe especificar el parámetro **SourceConnection** .  
  
## <a name="see-also"></a>Ver también  
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Flujo de control](../../integration-services/control-flow/control-flow.md)  
  
  
