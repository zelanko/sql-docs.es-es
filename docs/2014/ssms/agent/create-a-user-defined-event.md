---
title: Crear un evento definido por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent alerts, user-defined events
- user-defined events [SQL Server]
- multiple language support [SQL Server], alerts
- languages [SQL Server], alerts
- severity levels [SQL Server]
- global considerations [SQL Server], alerts
- events [SQL Server], user-defined
- SQL Server Agent alerts, multiple-language environments
- alerts [SQL Server], user-defined events
- alerts [SQL Server], multiple-language environments
- custom events [SQL Server Agent]
- international considerations [SQL Server], alerts
ms.assetid: 03d71a35-97fa-4bba-aa9a-23ac9c9cf879
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4c59bfb6f5f2c9621d212dc52a92daecd79fad7b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37313325"
---
# <a name="create-a-user-defined-event"></a>Crear un evento definido por el usuario
  Puede crear eventos definidos por el usuario si desea supervisar los eventos distintos de otros predefinidos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. También puede asignar un nivel de gravedad a cada evento definido por el usuario.  
  
> [!NOTE]  
>  Cuando use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccione la opción **Escribir en el registro de eventos de aplicación Windows** para cada mensaje de evento definido por el usuario, y garantizar así que se registran los mensajes. De manera predeterminada, los mensajes definidos por el usuario con niveles de gravedad inferiores a 19 no se envían al registro de aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows cuando se producen. Por tanto, no desencadenan alertas del Agente SQL Server.  
  
 Los mensajes de eventos definidos por el usuario deben tener un número de mensaje exclusivo. Los números de los mensajes de eventos definidos por el usuario deben ser mayores de 50.000. Se pueden definir mensajes para el evento en varios idiomas. No obstante, debe existir un mensaje de error en **En-US** para que se puedan agregar mensajes en otros idiomas.  
  
 Si administra un entorno [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en varios idiomas, cree mensajes definidos por el usuario en cada uno de los idiomas admitidos. Por ejemplo, si crea un nuevo mensaje de evento que se va a utilizar en un servidor en inglés y en alemán, utilice el mismo número de mensaje para ambos, pero asigne un idioma distinto a cada uno.  
  
 Las tareas siguientes ofrecen información acerca de cómo crear eventos definidos por el usuario y alertas que respondan a los eventos:  
  
 **Para crear una alerta basada en un número de mensaje**  
  
-   [SQL Server Management Studio](create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **Para crear una alerta basada en niveles de gravedad**  
  
-   [SQL Server Management Studio](create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **Para definir la respuesta a una alerta**  
  
-   [SQL Server Management Studio](../sql-server-management-studio-ssms.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)  
  
 **Para crear el mensaje de error de un evento definido por el usuario**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql)  
  
 **Para modificar el mensaje de error de un evento definido por el usuario**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-altermessage-transact-sql)  
  
 **Para eliminar el mensaje de error de un evento definido por el usuario**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-dropmessage-transact-sql)  
  
 **Para deshabilitar o volver a activar una alerta**  
  
-   [SQL Server Management Studio](disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql)  
  
## <a name="see-also"></a>Vea también  
 [sp_update_alert &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql)  
  
  
