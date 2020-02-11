---
title: Tarea Notificar al operador (Plan de mantenimiento) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.notifyoperator.f1
helpviewer_keywords:
- Notify Operator Task dialog box
ms.assetid: 39c0797c-ad2b-4591-85c9-a23a7f902895
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0ef94ed9e296c588b70789ace0bbbbe79bc8008f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68205966"
---
# <a name="notify-operator-task-maintenance-plan"></a>Tarea Notificar al operador (Plan de mantenimiento)
  Utilice el cuadro de diálogo de **tarea notificar** a los operadores para agregar una notificación automática a este plan de mantenimiento. Para usar esta tarea, debe tener correo electrónico de base de datos habilitado y configurado correctamente con msdb como una base de datos host de correo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y tener un operador del agente con una dirección de correo electrónico válida.  
  
 Esta tarea usa el procedimiento almacenado sp_notify_operator.  
  
## <a name="options"></a>Opciones  
 **Connection**  
 Seleccione la conexión al servidor que va a utilizar para la realización de esta tarea.  
  
 **Nuevo**  
 Cree una nueva conexión de servidor que utilizará al realizar esta tarea. El cuadro de diálogo **Nueva conexión** se describe a continuación.  
  
 **Operadores a los que notificar**  
 Especifica el destinatario del correo electrónico.  
  
 **Asunto del mensaje de notificación**  
 Especifica el texto que se va a incluir en la línea de asunto del mensaje de notificación.  
  
 **Cuerpo del mensaje de notificación**  
 Especifica el texto que se va a incluir en el cuerpo del mensaje de notificación.  
  
 **Ver T-SQL**  
 Muestra las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] realizadas en el servidor para esta tarea, en función de las opciones seleccionadas.  
  
> [!NOTE]  
>  Si el número de objetos afectados es elevado, es posible que deba esperar un rato hasta que se muestren.  
  
## <a name="new-connection-dialog-box"></a>Cuadro de diálogo Nueva conexión  
 **Nombre de la conexión**  
 Escriba un nombre para la nueva conexión.  
  
 **Seleccionar o especificar un nombre de servidor**  
 Seleccione un servidor al que conectarse cuando se realice esta tarea.  
  
 **Actualizar**  
 Actualiza la lista de servidores disponibles.  
  
 **Especificar información para iniciar sesión en el servidor**  
 Especifica el modo de autenticación en el servidor.  
  
 **Usar seguridad integrada de Windows NT**  
 Se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] con [!INCLUDE[msCoName](../../includes/msconame-md.md)] la autenticación de Windows.  
  
 **Utilizar un nombre de usuario y una contraseña específicos**  
 Se conecta a una instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] con la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esta opción no está disponible.  
  
 **Nombre de usuario**  
 Proporcione un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la autenticación. Esta opción no está disponible.  
  
 **Contraseña**  
 Proporcione una contraseña para que se utilice en la autenticación. Esta opción no está disponible.  
  
## <a name="see-also"></a>Consulte también  
 [Correo electrónico de base de datos](../database-mail/database-mail.md)   
 [sp_notify_operator &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-notify-operator-transact-sql)  
  
  
