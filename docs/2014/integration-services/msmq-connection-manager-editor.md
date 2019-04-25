---
title: Editor del Administrador de conexiones MSMQ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msmqconnectionmanager.f1
helpviewer_keywords:
- MSMQ Connection Manager Editor
ms.assetid: ef842cb4-82da-4550-85fe-9bedbc1e77c7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d532433c36f3b4c18b39d16dcbbe81a3d969acfc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767237"
---
# <a name="msmq-connection-manager-editor"></a>administrador de conexiones MSMQ, editor del
  Use el cuadro de diálogo **Administrador de conexiones MSMQ** para especificar la ruta de acceso a una cola de mensajes de Message Queuing (que también recibe el nombre de MSMQ).  
  
 Para obtener más información acerca del administrador de conexiones MSMQ, vea [MSMQ Connection Manager](connection-manager/msmq-connection-manager.md).  
  
> [!NOTE]  
>  El administrador de conexiones MSMQ admite colas públicas y privadas locales, además de colas públicas remotas. No admite colas privadas remotas. Para obtener una solución que utilice la tarea Script, vea [Enviar a una cola de mensajes privada remota con la tarea Script](control-flow/script-task.md).  
  
## <a name="options"></a>Opciones  
 **Name**  
 Proporcione un nombre único para el administrador de conexiones MSMQ en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descripción**  
 Describa el administrador de conexiones. Como método recomendado, describa el administrador de conexiones desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Ruta de acceso**  
 Escriba la ruta de acceso completa de la cola de mensajes. El formato de la ruta de acceso depende del tipo de cola.  
  
|Tipo de cola|Ruta de acceso de ejemplo|  
|----------------|-----------------|  
|Público|\<nombre del equipo>\\<nombre de la cola\>|  
|Privada|\<nombre del equipo>\Private$\\<nombre de la cola\>|  
  
 Puede utilizar "." para representar el equipo local.  
  
 **Prueba**  
 Después de configurar el Administrador de conexiones MSMQ, confirme que la conexión es viable haciendo clic en **Probar**.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
