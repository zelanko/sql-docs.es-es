---
title: Categoría de eventos de auditoría de seguridad | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [Analysis Services], security audit
- security events [Analysis Services]
ms.assetid: 9686a495-68d7-4137-8e30-2655aa519f6c
caps.latest.revision: 24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 79141f6ed5c61e03b792875fbff2253f9e8bd0aa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180912"
---
# <a name="security-audit-event-category"></a>Auditoría de seguridad (categoría de eventos)
  La categoría de eventos Auditoría de seguridad tiene las clases de eventos que se describen en la siguiente tabla.  
  
|Clase de eventos|Identificador del evento|Descripción|  
|-----------------|--------------|-----------------|  
|Audit Login|1|Registra todos los nuevos eventos de conexión desde que se inició el seguimiento, como cuando un cliente solicitó una conexión a un servidor que ejecuta una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|Audit Logout|2|Registra todos los nuevos eventos de desconexión desde que se inició el seguimiento, como cuando un cliente envía un comando de desconexión.|  
|Audit Server Starts and Stops|4|Registra las actividades de cierre, inicio y pausa de los servicios.|  
|Audit Object Permission Event|18|Registra todos los cambios de permiso de un objeto.|  
|Audit Admin Operations Event|19|Registra las operaciones de servidor de copia de seguridad, restauración, sincronización, operaciones de adjuntar o separar, carga de imágenes y guardado de imágenes.|  
  
 Para obtener más información acerca de las columnas asociadas a cada una de las clases de evento de Auditoría de seguridad, vea [Security Audit Data Columns](security-audit-data-columns.md).  
  
## <a name="see-also"></a>Vea también  
 [Eventos de seguimiento de Analysis Services](analysis-services-trace-events.md)  
  
  
