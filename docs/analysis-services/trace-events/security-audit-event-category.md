---
title: "Categoría de eventos de auditoría de seguridad | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [Analysis Services], security audit
- security events [Analysis Services]
ms.assetid: 9686a495-68d7-4137-8e30-2655aa519f6c
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 74ae764326058f6ccedb8edf0b781b1f93dc0d87
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="security-audit-event-category"></a>Auditoría de seguridad (categoría de eventos)
  La categoría de eventos Auditoría de seguridad tiene las clases de eventos que se describen en la siguiente tabla.  
  
|Clase de eventos|Identificador del evento|Description|  
|-----------------|--------------|-----------------|  
|Audit Login|1|Registra todos los nuevos eventos de conexión desde que se inició el seguimiento, como cuando un cliente solicitó una conexión a un servidor que ejecuta una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|Audit Logout|2|Registra todos los nuevos eventos de desconexión desde que se inició el seguimiento, como cuando un cliente envía un comando de desconexión.|  
|Audit Server Starts and Stops|4|Registra las actividades de cierre, inicio y pausa de los servicios.|  
|Audit Object Permission Event|18|Registra todos los cambios de permiso de un objeto.|  
|Audit Admin Operations Event|19|Registra las operaciones de servidor de copia de seguridad, restauración, sincronización, operaciones de adjuntar o separar, carga de imágenes y guardado de imágenes.|  
  
 Para obtener más información acerca de las columnas asociadas a cada una de las clases de evento de Auditoría de seguridad, vea [Security Audit Data Columns](../../analysis-services/trace-events/security-audit-data-columns.md).  
  
## <a name="see-also"></a>Vea también  
 [Eventos de seguimiento de Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
