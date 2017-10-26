---
title: General Statistics (objeto de SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLServer:General Statistics
- General Statistics object
ms.assetid: c738e549-d7e7-4211-9ec3-064ac140af7c
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e179c0523d8d406f9413f98a0a5a7acbc7e714a1
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-general-statistics-object"></a>General Statistics (objeto de SQL Server)
  El objeto **SQLServer:General Statistics** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona contadores para supervisar la actividad general en el servidor, como el número de conexiones actuales y el número de usuarios que se conectan y se desconectan de equipos en los que se ejecuta una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]por segundo. Esto resulta útil cuando se trabaja en sistemas de procesamiento de transacciones en línea (OLTP) grandes, con un gran número de clientes que se conectan y se desconectan de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta tabla describe los contadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **de** .  
  
|Contadores de Estadísticas generales de SQL Server|Descripción|  
|--------------------------------------------|-----------------|  
|**Tablas temporales activas**|Número de tablas o variables de tabla temporales en uso.|  
|**Restablecimientos de conexión/s**|Número total de inicios de sesión comenzados desde el grupo de conexiones.|  
|**Notificaciones de eventos que se quitarán con retraso**|Número de notificaciones de eventos que esperan a que un subproceso del sistema las quite.|  
|**Solicitudes HTTP autenticadas**|Número de solicitudes HTTP autenticadas iniciadas por segundo.|  
|**Conexiones lógicas**|Número de conexiones lógicas con el sistema.<br /><br /> La principal finalidad de las conexiones lógicas es dar servicio a varias solicitudes de conjuntos de resultados activos múltiples (MARS). En las solicitudes MARS, cada vez que una aplicación establece una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede haber varias conexiones lógicas que correspondan a una conexión física.<br /><br /> Cuando no se usa MARS, la relación entre conexiones físicas y lógicas es 1:1. Por tanto, cada vez que una aplicación establece una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], las conexiones lógicas aumentarán en 1.|  
|**Inicios de sesión/seg.**|Número total de inicios de sesión por segundo. No se incluyen las conexiones agrupadas.|  
|**Cierres de sesión/seg.**|Número total de cierres de sesión iniciados por segundo.|  
|**Interbloqueos de Mars**|Número de interbloqueos de Mars detectados.|  
|**Velocidad de esperas no atómicas**|Número de esperas no atómicas por segundo.|  
|**Procesos bloqueados**|Número de los procesos bloqueados actualmente.|  
|**Solicitudes SOAP vacías**|Número de solicitudes SOAP vacías iniciadas por segundo.|  
|**Llamadas de métodos SOAP**|Número de llamadas de métodos SOAP iniciadas por segundo.|  
|**Solicitudes de inicio de sesión SOAP**|Número de solicitudes de inicio de sesión SOAP iniciadas por segundo.|  
|**Solicitudes de finalización de sesión SOAP**|Número de solicitudes de finalización de sesión SOAP iniciadas por segundo.|  
|**Solicitudes SOAP SQL**|Número de solicitudes SOAP SQL iniciadas por segundo.|  
|**Solicitudes SOAP WSDL**|Número de solicitudes de lenguaje de descripción de servicios web SOAP iniciadas por segundo.|  
|**Esperas de bloqueo de proveedor de E/S de seguimiento de SQL**|Número de esperas de bloqueo del proveedor de E/S de archivos por segundo.| 
|**Velocidad de creación de tablas temporales**|Número de tablas o variables de tabla temporales creadas por segundo.|  
|**Tablas temporales que destruir**|Número de tablas y variables de tablas temporales en espera de que destruya el subproceso de sistema de limpieza.|  
|**Identificador de unidad de recuperación de tempdb**|El número de identificador de unidad de recuperación tempdb duplicado que se generó.|
|**Identificador de conjunto de filas de tempdb**|El número de identificador de conjunto de filas tempdb duplicado que se generó.| 
|**Cola de notificación de eventos de seguimiento**|Número de instancias de notificación de eventos de seguimiento que esperan en la cola interna para ser enviados a través de Service Broker.|  
|**Transacciones**|Número de altas de transacciones (locales, DTC y enlazadas juntas).|  
|**Conexiones de usuario**|Cuenta el número de usuarios actualmente conectados a SQL Server.|  
  
## <a name="see-also"></a>Vea también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  

