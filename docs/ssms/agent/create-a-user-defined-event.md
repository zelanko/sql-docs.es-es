---
title: Crear un evento definido por el usuario | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0f5aea958032436b1d9f168dafb0ad24712d0931
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="create-a-user-defined-event"></a>Crear un evento definido por el usuario
Puede crear eventos definidos por el usuario si desea supervisar los eventos distintos de otros predefinidos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. También puede asignar un nivel de gravedad a cada evento definido por el usuario.  
  
> [!NOTE]  
> Cuando use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], seleccione la opción **Escribir en el registro de eventos de aplicación Windows** para cada mensaje de evento definido por el usuario, y garantizar así que se registran los mensajes. De manera predeterminada, los mensajes definidos por el usuario con niveles de gravedad inferiores a 19 no se envían al registro de aplicación de [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows cuando se producen. Por tanto, no desencadenan alertas del Agente SQL Server.  
  
Los mensajes de eventos definidos por el usuario deben tener un número de mensaje exclusivo. Los números de los mensajes de eventos definidos por el usuario deben ser mayores de 50.000. Se pueden definir mensajes para el evento en varios idiomas. No obstante, debe existir un mensaje de error en **En-US** para que se puedan agregar mensajes en otros idiomas.  
  
Si administra un entorno [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en varios idiomas, cree mensajes definidos por el usuario en cada uno de los idiomas admitidos. Por ejemplo, si crea un nuevo mensaje de evento que se va a utilizar en un servidor en inglés y en alemán, utilice el mismo número de mensaje para ambos, pero asigne un idioma distinto a cada uno.  
  
Las tareas siguientes ofrecen información acerca de cómo crear eventos definidos por el usuario y alertas que respondan a los eventos:  
  
**Para crear una alerta basada en un número de mensaje**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/d9b41853-e22d-4813-a79f-57efb4511f09)  
  
**Para crear una alerta basada en niveles de gravedad**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/d9b41853-e22d-4813-a79f-57efb4511f09)  
  
**Para definir la respuesta a una alerta**  
  
-   [SQL Server Management Studio](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)  
  
**Para crear el mensaje de error de un evento definido por el usuario**  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/54746d30-f944-40e5-a707-f2d9be0fb9eb)  
  
**Para modificar el mensaje de error de un evento definido por el usuario**  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/1b28f280-8ef9-48e9-bd99-ec14d79abaca)  
  
**Para eliminar el mensaje de error de un evento definido por el usuario**  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/17287a15-cdde-43d1-bb18-9f920bc15db8)  
  
**Para deshabilitar o volver a activar una alerta**  
  
-   [SQL Server Management Studio](../../ssms/agent/disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/4bbaeaab-8aca-4c9e-abc1-82ce73090bd3)  
  
## <a name="see-also"></a>Vea también  
[sp_update_alert (Transact-SQL)](http://msdn.microsoft.com/en-us/4bbaeaab-8aca-4c9e-abc1-82ce73090bd3)  
  

