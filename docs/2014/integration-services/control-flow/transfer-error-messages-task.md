---
title: Tarea Transferir mensajes de error | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfererrormessagestask.f1
helpviewer_keywords:
- Transfer Error Messages task [Integration Services]
ms.assetid: da702289-035a-4d14-bd74-04461fbfee1b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: eaefd6e7ae4748505db9bd84601de6166f9d5f98
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62830131"
---
# <a name="transfer-error-messages-task"></a>Tarea Transferir mensajes de error
  La tarea Transferir mensajes de error transfiere uno o más mensajes de error definidos por el usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los mensajes definidos por el usuario son mensajes con un identificador igual o mayor que 50000. Los mensajes con un identificador menor que 50000 son mensajes de error del sistema, y no se pueden transferir mediante la tarea Transferir mensajes de error.  
  
 La tarea Transferir mensajes de error se puede configurar para que transfiera todos los mensajes de error o solo los mensajes de error especificados. Los mensajes de error definidos por el usuario pueden estar disponibles en distintos idiomas y la tarea se puede configurar para que transfiera únicamente los mensajes que estén en los idiomas seleccionados. Debe existir una versión en us_english del mensaje que utiliza página de códigos 1033 en el servidor de destino para poder transferir versiones en otros idiomas del mensaje a ese servidor.  
  
 La tabla sysmessages de la base de datos maestra contiene todos los mensajes de error, tanto los del sistema como los definidos por el usuario, que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Es posible que los mensajes definidos por el usuario que desea transferir ya existan en el destino. Un mensaje de error se define como un mensaje de error duplicado si el identificador y el idioma son iguales. La tarea Transferir mensajes de error se puede configurar para haga lo siguiente con los mensajes de error existentes:  
  
-   Sobrescribir los mensajes de error existentes.  
  
-   Hacer que la tarea genere un error cuando existan mensajes duplicados.  
  
-   Omitir los mensajes de error duplicados.  
  
 Durante la ejecución, la tarea Transferir mensajes de error se conecta con los servidores de origen y de destino utilizando uno o dos administradores de conexión SMO. El administrador de conexiones SMO se configura independientemente de la tarea Transferir mensajes de error y después se hace referencia a él en la tarea Transferir mensajes de error. El administrador de conexiones SMO especifica el servidor y el modo de autenticación que se utiliza para tener acceso al servidor. Para más información, consulte [SMO Connection Manager](../connection-manager/smo-connection-manager.md).  
  
 La tarea Transferir mensajes de error admite un origen y un destino que sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No hay restricciones respecto a qué versión hay que usar como origen o como destino.  
  
## <a name="events"></a>Eventos  
 La tarea genera un evento de información que indica el número de mensajes de error transferidos.  
  
 La tarea Transferir mensajes de error no indica el progreso incremental de la transferencia de mensajes de error; solo indica 0% y 100%.  
  
## <a name="execution-value"></a>Valor de ejecución  
 El valor de ejecución, que se define en la propiedad `ExecutionValue` de la tarea, devuelve el número de mensajes de error transferidos. Si se asigna una variable definida por el usuario a la propiedad `ExecValueVariable` de la tarea Transferir mensajes de error, se puede hacer que la información de la transferencia de mensajes de error esté disponible para otros objetos del paquete. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) y [Usar variables en paquetes](../use-variables-in-packages.md).  
  
## <a name="log-entries"></a>Entradas del registro  
 La tarea Transferir mensajes de error incluye las siguientes entradas del registro personalizadas:  
  
-   TransferErrorMessagesTaskStartTransferringObjects    Esta entrada del registro indica que se ha iniciado la transferencia. La entrada del registro incluye la hora de inicio.  
  
-   TransferErrorMessagesTaskFinishedTransferringObjects   Esta entrada del registro indica que ha finalizado la transferencia. La entrada del registro incluye la hora de finalización.  
  
 Además, una entrada del registro para el evento `OnInformation` indica el número de mensajes de error transferidos, y se escribe una entrada del registro para el evento `OnWarning event` por cada mensaje de error que se sobrescribe en el destino.  
  
## <a name="security-and-permissions"></a>Seguridad y permisos  
 Para crear mensajes de error, el usuario que ejecuta el paquete debe ser miembro de los roles sysadmin o serveradmin en el servidor de destino.  
  
## <a name="configuration-of-the-transfer-error-messages-task"></a>Configuración de la tarea Transferir mensajes de error  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea transferir mensajes de error &#40;página general&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor de la tarea Transferir mensajes de error &#40;página Mensajes&#41;](../transfer-error-messages-task-editor-messages-page.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferErrorMessagesTask.TransferErrorMessagesTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Consulte también  
 [Tareas de Integration Services](integration-services-tasks.md)   
 [Flujo de control](control-flow.md)  
  
  
