---
description: Propiedades del trabajo - Nuevo trabajo (página Notificaciones)
title: Propiedades del trabajo - Nuevo trabajo (página Notificaciones)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: eec2f2b28b800a39fdef76ac2f3d2f7ef2d37014
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480766"
---
# <a name="job-properties---new-job-notifications-page"></a>Propiedades del trabajo - Nuevo trabajo (página Notificaciones)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

Use esta página para establecer acciones que el Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe realizar cuando finalice el trabajo.  
  
## <a name="options"></a>Opciones  
**Correo electrónico**  
Seleccione esta opción para enviar correo electrónico cuando el trabajo finalice. Después de seleccionar esta opción, elija el operador al que se va a notificar y la condición que activará la notificación: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
**Page**  
Seleccione esta opción para enviar correo electrónico al buscapersonas de un operador cuando el trabajo finalice. Después de seleccionar esta opción, especifique el operador al que se va a notificar y la condición que activará la notificación: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
**NET SEND**  
Seleccione esta opción para utilizar NET SEND para avisar a un operador cuando el trabajo finalice. Después de seleccionar esta opción, especifique el operador al que se va a notificar y la condición que activará la notificación: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
**Escribir en el registro de eventos de aplicación Windows**  
Seleccione esta opción para escribir una entrada en el registro de eventos de la aplicación cuando el trabajo finalice. Después de seleccionar esta opción, especifique la condición que hará que se escriba la entrada: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
**Eliminar automáticamente el trabajo**  
Seleccione esta opción para eliminar el trabajo cuando éste finalice. Después de seleccionar esta opción, especifique la condición que activará la eliminación del trabajo: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
## <a name="see-also"></a>Consulte también  
[Implementar trabajos](../../ssms/agent/implement-jobs.md)  
[Cómo: Configurar el Agente SQL Server para que use el correo electrónico de base de datos](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
