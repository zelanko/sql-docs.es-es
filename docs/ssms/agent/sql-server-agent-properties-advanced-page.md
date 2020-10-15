---
description: Propiedades de Agente SQL Server (página Avanzadas)
title: Propiedades de Agente SQL Server (página Avanzadas)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.advanced.f1
ms.assetid: a4d798ee-4c18-40d4-b6af-63d17503738c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ebb096313477068f1c1e33aa777c06b0b72d3d4e
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038198"
---
# <a name="sql-server-agent-properties-advanced-page"></a>Propiedades de Agente SQL Server (página Avanzadas)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

Use esta página para ver y modificar las propiedades avanzadas del servicio del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
**Reenvío de eventos de SQL Server**  
Las opciones de esta categoría activan y configuran el reenvío de eventos.  
  
**Reenviar eventos a otro servidor**  
Reenvía los eventos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otro servidor.  
  
**Server**  
Seleccione el nombre del servidor al que se reenvían los eventos.  
  
**Eventos no controlados**  
Solo reenvía eventos no controlados al servidor especificado. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo reenvía eventos a los que no responde ninguna alerta.  
  
**Todos los eventos**  
Reenvía todos los eventos. Cuando una alerta de la instancia local responde al evento, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reenvía el evento y procesa la alerta.  
  
**Si el evento tiene una gravedad de o por encima de**  
Solo reenvía eventos con el nivel de gravedad igual o superior al especificado.  
  
**Condición de CPU inactiva**  
Las opciones de esta categoría definen las condiciones en las que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecuta trabajos programados para ejecutarse en la programación de CPU inactiva.  
  
**Definir condición de CPU inactiva**  
Define las condiciones en las que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera que la CPU está inactiva.  
  
**El promedio de uso de la CPU baja de**  
Porcentaje de uso de CPU por debajo del cual se considera inactiva la CPU.  
  
**Y permanece por debajo durante**  
Cantidad de tiempo que el promedio de uso de la CPU debe situarse por debajo del nivel especificado antes de que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecute trabajos en la programación de CPU inactiva.  
  
## <a name="see-also"></a>Consulte también  
[Crear y adjuntar programaciones a trabajos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[Administrar eventos](../../ssms/agent/manage-events.md)  
