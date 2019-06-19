---
title: 'Propiedades de alerta: Nueva alerta (página Opciones) | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e2e2e04d210900a60d6d6cff432e19a61d6c88fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65099436"
---
# <a name="alert-properties---new-alert-options-page"></a>Propiedades de alerta - Nueva alerta (página Opciones)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Utilice esta página para ver y cambiar las opciones de las alertas del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

## <a name="options"></a>Opciones  
**Correo electrónico**  
Incluye el texto de error del evento, si existe alguno, en las notificaciones de correo electrónico.  
  
**Buscapersonas**  
Incluye el texto de error del evento, si existe alguno, en las notificaciones de buscapersonas.  
  
**NET SEND**  
Incluye el texto de error del evento, si existe alguno, en las notificaciones de NET SEND.  
  
**Mensaje adicional de notificación para enviar**  
Escriba el texto adicional que se va a incluir en los mensajes de notificación.  
  
**Retardo entre respuestas**  
Especifique un retardo para las repeticiones del evento. Algunos eventos pueden producirse con frecuencia durante un breve período de tiempo. En este caso, es posible que desee saber que se ha producido el evento, pero sin necesidad de generar una respuesta para cada evento. Use esta opción para especificar un tiempo de espera. Con un retardo, después de que la alerta responde al evento, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espera el retardo especificado antes de responder de nuevo, independientemente de si el evento se produce durante el retardo.  
  
**Minutos**  
Especifique un retardo en minutos. Para responder cada vez que se produce el evento, especifique 0 minutos y 0 segundos.  
  
**Segundos**  
Especifique un retardo en segundos. Para responder cada vez que se produce el evento, especifique 0 minutos y 0 segundos.  
  
## <a name="see-also"></a>Consulte también  
[Alertas](../../ssms/agent/alerts.md)  
  
