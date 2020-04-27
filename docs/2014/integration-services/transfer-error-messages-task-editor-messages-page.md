---
title: Editor de la tarea transferir mensajes de error (página mensajes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfererrormessagestask.errormessages.F1
helpviewer_keywords:
- Transfer Error Messages Task Editor
ms.assetid: cb2226a0-3037-4fdf-966f-81eabc0da9cf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f753aaddbd2647b1d8874b0d34db415f75aa99b9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66055039"
---
# <a name="transfer-error-messages-task-editor-messages-page"></a>Editor de la tarea Transferir mensajes de error (página Mensajes)
  Use la página **Mensajes** del cuadro de diálogo **Editor de la tarea Transferir mensajes de error** para especificar propiedades para copiar uno o varios mensajes de error definidos por el usuario de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a otra. Para obtener más información acerca de esta tarea, vea [Transfer Error Messages Task](control-flow/transfer-error-messages-task.md).  
  
## <a name="options"></a>Opciones  
 **SourceConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en ** \<nueva conexión... >** para crear una nueva conexión al servidor de origen.  
  
 **DestinationConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en ** \<nueva conexión... >** para crear una nueva conexión al servidor de destino.  
  
 **IfObjectExists**  
 Seleccione si la tarea debe sobrescribir mensajes de error definidos por el usuario existentes, omitir mensajes existentes o generar un error si existen ya mensajes de error con el mismo nombre en el servidor de destino.  
  
 **TransferAllErrorMessages**  
 Seleccione si la tarea debe copiar todos los mensajes definidos por el usuario o solo los especificados del servidor de origen al de destino.  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Reales**|Copiar todos los mensajes definidos por el usuario.|  
|**Es**|Copiar solo los mensajes definidos por el usuario especificados.|  
  
 **ErrorMessagesList**  
 Haga clic en el botón examinar **(...)** para seleccionar los mensajes de error que se van a copiar.  
  
> [!NOTE]  
>  Para poder seleccionar los mensajes de error que se van a copiar, debe especificar el parámetro **SourceConnection** .  
  
 **ErrorMessageLanguagesList**  
 Haga clic en el botón examinar **(...)** para seleccionar los idiomas en los que se van a copiar los mensajes de error definidos por el usuario en el servidor de destino. Debe existir una versión en us_english (página de códigos 1033) del mensaje en el servidor de destino para poder transferir versiones en otros idiomas del mensaje a ese servidor.  
  
> [!NOTE]  
>  Para poder seleccionar los mensajes de error que se van a copiar, debe especificar el parámetro **SourceConnection** .  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Tareas de Integration Services](control-flow/integration-services-tasks.md)   
 [Editor de la tarea transferir mensajes de error &#40;página general&#41;](general-page-of-integration-services-designers-options.md)   
 [Administrador de conexiones SMO](connection-manager/smo-connection-manager.md)   
 [Editor de la tarea transferir mensajes de error &#40;página general&#41;](general-page-of-integration-services-designers-options.md)   
 [SMO, administrador de conexiones](connection-manager/smo-connection-manager.md)  
  
  
