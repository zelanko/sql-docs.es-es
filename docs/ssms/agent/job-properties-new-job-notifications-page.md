---
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
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2d1bc2ec3aef699e491fdac2036352fd986fec85
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85690599"
---
# <a name="job-properties---new-job-notifications-page"></a>Propiedades del trabajo - Nuevo trabajo (página Notificaciones)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Use esta página para establecer acciones que el Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe realizar cuando finalice el trabajo.  
  
## <a name="options"></a>Opciones  
**Correo electrónico**  
Seleccione esta opción para enviar correo electrónico cuando el trabajo finalice. Después de seleccionar esta opción, elija el operador al que se va a notificar y la condición que activará la notificación: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
**Page**  
Seleccione esta opción para enviar correo electrónico al buscapersonas de un operador cuando el trabajo finalice. Después de seleccionar esta opción, especifique el operador al que se va a notificar y la condición que activará la notificación: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
**NET SEND**  
Seleccione esta opción para utilizar NET SEND para avisar a un operador cuando el trabajo finalice. Después de seleccionar esta opción, especifique el operador al que se va a notificar y la condición que activará la notificación: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
**Escribir en el registro de eventos de aplicación Windows**  
Seleccione esta opción para escribir una entrada en el registro de eventos de la aplicación cuando el trabajo finalice. Después de seleccionar esta opción, especifique la condición que hará que la entrada se escriba: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
**Eliminar automáticamente el trabajo**  
Seleccione esta opción para eliminar el trabajo cuando éste finalice. Después de seleccionar esta opción, especifique la condición que desencadenará la eliminación del trabajo: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
## <a name="see-also"></a>Consulte también  
[Implementar trabajos](../../ssms/agent/implement-jobs.md)  
[Cómo: Configurar el Agente SQL Server para que use el correo electrónico de base de datos](https://msdn.microsoft.com/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  
