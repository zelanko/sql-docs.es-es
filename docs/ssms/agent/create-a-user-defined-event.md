---
description: Crear un evento definido por el usuario
title: Crear un evento definido por el usuario
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
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
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bf18385b89ac7af32bfde26d704880eb4e9bb300
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036678"
---
# <a name="create-a-user-defined-event"></a>Crear un evento definido por el usuario
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

Puede crear eventos definidos por el usuario si desea supervisar los eventos distintos de otros predefinidos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. También puede asignar un nivel de gravedad a cada evento definido por el usuario.  
  
> [!NOTE]  
> Cuando use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccione la opción **Escribir en el registro de eventos de aplicación Windows** para cada mensaje de evento definido por el usuario, y garantizar así que se registran los mensajes. De manera predeterminada, los mensajes definidos por el usuario con niveles de gravedad inferiores a 19 no se envían al registro de aplicación de [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows cuando se producen. Por tanto, no desencadenan alertas del Agente SQL Server.  
  
Los mensajes de eventos definidos por el usuario deben tener un número de mensaje exclusivo. Los números de los mensajes de eventos definidos por el usuario deben ser mayores de 50.000. Se pueden definir mensajes para el evento en varios idiomas. No obstante, debe existir un mensaje de error en **En-US** para que se puedan agregar mensajes en otros idiomas.  
  
Si administra un entorno [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en varios idiomas, cree mensajes definidos por el usuario en cada uno de los idiomas admitidos. Por ejemplo, si crea un nuevo mensaje de evento que se va a utilizar en un servidor en inglés y en alemán, utilice el mismo número de mensaje para ambos, pero asigne un idioma distinto a cada uno.  
  
Las tareas siguientes ofrecen información acerca de cómo crear eventos definidos por el usuario y alertas que respondan a los eventos:  
  
**Para crear una alerta basada en un número de mensaje**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)  
  
**Para crear una alerta basada en niveles de gravedad**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)  
  
**Para definir la respuesta a una alerta**  
  
-   [SQL Server Management Studio](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)  
  
**Para crear el mensaje de error de un evento definido por el usuario**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)  
  
**Para modificar el mensaje de error de un evento definido por el usuario**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)  
  
**Para eliminar el mensaje de error de un evento definido por el usuario**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)  
  
**Para deshabilitar o volver a activar una alerta**  
  
-   [SQL Server Management Studio](../../ssms/agent/disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)  
  
## <a name="see-also"></a>Consulte también  
[sp_update_alert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)  
