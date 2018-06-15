---
title: Propiedades de alerta (página Historial) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ag.alert.history.f1
ms.assetid: f5359f5c-93a3-4a4a-8286-e9fe6f0196c7
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bb8ef6ac08f6fba987b7840cdec7e4e175606af6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33038382"
---
# <a name="alert-properties-history-page"></a>Propiedades de alerta (página Historial)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]


> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.


Utilice esta página para ver y modificar el historial de las alertas del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  

## <a name="options"></a>Opciones  
**Fecha de la última alerta**  
Muestra la fecha en que se produjo el último evento especificado, o **(Nunca ocurrido)** si el evento no se ha producido desde que se creó la alerta.  
  
**Fecha de la última respuesta**  
Muestra la fecha en que la alerta respondió por última vez al evento, o **(Nunca respondió)** si el evento no se ha producido desde que se creó la alerta.  
  
**Número de repeticiones**  
Número total de repeticiones del evento desde que se creó la alerta, o desde la última vez que se restableció el recuento.  
  
**Restablecer cuenta**  
Restablece la información de esta página.  
  
## <a name="see-also"></a>Ver también  
[Alertas](../../ssms/agent/alerts.md)  
  
