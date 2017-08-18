---
title: "Usar alertas y umbrales de advertencia de las métricas de rendimiento de la creación de reflejo | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- monitoring database mirroring [SQL Server]
- thresholds [SQL Server]
- database mirroring [SQL Server], managing in SQL Server Management Studio
- alerts [SQL Server], database mirroring
- database mirroring [SQL Server], monitoring
- warnings [database mirroring]
ms.assetid: 8cdd1515-0bd7-4f8c-a7fc-a33b575e20f6
caps.latest.revision: 40
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1d7f8c3105d562dd4203f5f9d2f47852068af819
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server"></a>Usar alertas y umbrales de advertencia de las métricas de rendimiento de la creación de reflejo (SQL Server)
  Este tema contiene información acerca de los eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para los que se pueden configurar y administrar umbrales de advertencia para la creación de reflejo de la base de datos. Puede usar el Monitor de creación de reflejo de la base de datos o los procedimientos almacenados **sp_dbmmonitorchangealert**, **sp_dbmmonitorhelpalert**y **sp_dbmmonitordropalert** . Este tema también contiene información acerca de cómo configurar alertas en los eventos de creación de reflejo de la base de datos.  
  
 Después de establecer la supervisión de una base de datos reflejada, un administrador del sistema puede configurar los umbrales de advertencia de algunas métricas de rendimiento clave. Además, el administrador puede configurar alertas para estos y otros eventos de la creación de reflejo de la base de datos.  
  
 **En este tema:**  
  
-   [Métricas de rendimiento y umbrales de advertencia](#PerfMetricsAndWarningThresholds)  
  
-   [Configurar y administrar umbrales de advertencia](#SetUpManageWarningThresholds)  
  
-   [Usar alertas para una base de datos reflejada](#UseAlerts)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="PerfMetricsAndWarningThresholds"></a> Métricas de rendimiento y umbrales de advertencia  
 En la siguiente tabla se presenta una lista de las métricas de rendimiento para las que se pueden configurar advertencias, se describe el umbral de advertencia correspondiente y se muestra la etiqueta correspondiente del Monitor de creación de reflejo de la base de datos.  
  
|Métrica de rendimiento|Umbral de advertencia|Etiqueta del Monitor de creación de reflejo de la base de datos|  
|------------------------|-----------------------|--------------------------------------|  
|Registro sin enviar|Especifica cuántos kilobytes (KB) de registro sin enviar generan una advertencia en la instancia del servidor principal. Esta advertencia ayuda a medir la pérdida de datos potencial en términos de KB y resulta especialmente importante en el modo de alto rendimiento. No obstante, la advertencia también es relevante para el modo de alta seguridad cuando la creación de reflejo se detiene o suspende debido a que los asociados se han desconectado.|**Advierte si el registro sin enviar supera el valor de umbral**|  
|Registro sin restaurar|Especifica cuántos KB de registro sin restaurar generan una advertencia en la instancia del servidor reflejado. Esta advertencia ayuda a medir el tiempo de conmutación por error. El*tiempo de la conmutación por error* se compone principalmente del tiempo que el servidor reflejado anterior necesita para poner al día los registros pendientes en su cola rehecha, más un breve tiempo adicional.<br /><br /> Nota: En una conmutación automática por error, el tiempo para que el sistema detecte el error es independiente del tiempo de conmutación por error.<br /><br /> Para más información, consulte [Calcular la interrupción del servicio durante la conmutación de roles &#40;creación de reflejo de la base de datos&#41;](../../database-engine/database-mirroring/estimate-the-interruption-of-service-during-role-switching-database-mirroring.md).|**Advertir si el registro sin restaurar sobrepasa el umbral**|  
|Transacción sin enviar más antigua|Especifica el número de minutos con transacciones que se puede acumular en la cola de envío antes de que se genere una advertencia en la instancia del servidor principal. Esta advertencia ayuda a medir la pérdida de datos potencial en términos de tiempo y resulta especialmente importante en el modo de alto rendimiento. No obstante, la advertencia también es relevante para el modo de alta seguridad cuando la creación de reflejo se detiene o suspende debido a que los asociados se han desconectado.|**Advierte si la antigüedad de la transacción sin enviar más antigua supera el valor de umbral**|  
|Sobrecarga de confirmación del servidor reflejado|Especifica el número de milisegundos de retardo medio por transacción que se tolera antes de que se genere una advertencia en el servidor principal. Este retardo es la cantidad de sobrecarga en la que se incurre mientras la instancia del servidor principal espera a la instancia del servidor reflejado para escribir la entrada de registro de la transacción en la cola de puesta al día. Este valor solo es relevante en el modo de alta seguridad.|**Advierte si la sobrecarga de confirmación del servidor reflejado supera el valor de umbral**|  
  
 En una base de datos reflejada, un administrador del sistema puede especificar un umbral para cualquier de estas métricas de rendimiento. Para obtener más información, vea [Configurar y administrar umbrales de advertencia](#SetUpManageWarningThresholds)más adelante en este tema.  
  
##  <a name="SetUpManageWarningThresholds"></a> Configurar y administrar umbrales de advertencia  
 Un administrador del sistema puede configurar uno o más umbrales de advertencia para las métricas de rendimiento clave de la creación de reflejo. Se recomienda establecer un umbral para una determinada advertencia en ambos asociados para asegurarse de que la advertencia persista si la base de datos genera un error. El umbral adecuado en cada asociado depende de las capacidades de rendimiento del sistema del asociado.  
  
 Los umbrales de advertencia se pueden configurar y administrar mediante el uso de:  
  
-   Monitor de creación de reflejo de la base de datos  
  
     En el Monitor de creación de reflejo de la base de datos, el administrador puede ver, al mismo tiempo, la configuración actual de una base de datos seleccionada en las instancias del servidor principal y reflejado, al seleccionar la página con pestañas **Advertencias** . Desde aquí, el administrador puede abrir el cuadro de diálogo **Establecer umbrales de advertencia** para habilitar y configurar uno o más umbrales de advertencia.  
  
     Para obtener una introducción a la interfaz del Monitor de creación de reflejo de la base de datos, vea [Database Mirroring Monitor Overview](../../database-engine/database-mirroring/database-mirroring-monitor-overview.md). Para obtener información sobre cómo iniciar el Monitor de creación de reflejo de base de datos, vea [Iniciar el Monitor de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md).  
  
-   Procedimientos almacenados del sistema  
  
     El siguiente conjunto de procedimientos almacenados del sistema permite al administrador configurar y administrar los umbrales de advertencia de las bases de datos reflejadas de un asociado a la vez.  
  
    |Procedimiento|Descripción|  
    |---------------|-----------------|  
    |[sp_dbmmonitorchangealert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)|Agrega o cambia el umbral de advertencia de una métrica de rendimiento de creación de reflejo especificada.|  
    |[sp_dbmmonitorhelpalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)|Devuelve información acerca de los umbrales de advertencia de una o todas las métricas claves de rendimiento de creación de reflejo de la base de datos.|  
    |[sp_dbmmonitordropalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)|Quita la advertencia de una métrica de rendimiento especificada.|  
  
## <a name="performance-threshold-events-sent-to-the-windows-event-log"></a>Eventos de umbral de rendimiento enviados al Registro de eventos de Windows  
 Si se define un umbral de advertencia para una métrica de rendimiento, cuando se actualiza la tabla de estado, el último valor se evalúa con el umbral. Si se alcanza el umbral, el procedimiento de actualización, **sp_dbmmonitorupdate**, genera un evento informativo (un *evento de umbral de rendimiento*) para la métrica y escribe el evento en el Registro de eventos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. En la siguiente tabla se presenta una lista de los Id. de eventos de los eventos de umbral de rendimiento.  
  
|Métrica de rendimiento|Identificador del evento|  
|------------------------|--------------|  
|Registro sin enviar|32042|  
|Registro sin restaurar|32043|  
|Transacción sin enviar más antigua|32040|  
|Sobrecarga de confirmación del servidor reflejado|32044|  
  
> [!NOTE]  
>  Un administrador puede definir alertas en uno o más de estos eventos. Para obtener más información, vea [Usar alertas para una base de datos reflejada](#UseAlerts)más adelante en este  
>   
>  tema.  
  
##  <a name="UseAlerts"></a> Usar alertas para una base de datos reflejada  
 Una parte importante de la supervisión de una base de datos reflejada es la configuración de alertas en los eventos significativos de creación de reflejo de la base de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera los tipos siguientes de eventos de creación de reflejo de la base de datos:  
  
-   Eventos de umbral de rendimiento  
  
     Para obtener más información, vea "Eventos de umbral de rendimiento enviados al Registro de eventos de Windows", anteriormente en este tema.  
  
-   Eventos de cambio de estado  
  
     Hay eventos del Instrumental de administración de Windows (WMI) que se generan cuando se producen cambios en el estado interno de una sesión de creación de reflejo de la base de datos.  
  
    > [!NOTE]  
    >  Para obtener más información, vea [Conceptos del proveedor WMI para eventos de servidor](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md).  
  
 Un administrador del sistema puede configurar alertas de estos eventos mediante el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u otras aplicaciones como, por ejemplo, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Operations Manager.  
  
 Cuando se definen alertas de eventos de la creación de reflejo de la base de datos, se recomienda definir umbrales de advertencia y alertas en las instancias de los servidores asociados. Los eventos individuales se generan en el servidor principal o reflejado, pero cada asociado puede realizar cualquiera de los roles en cualquier momento. Para asegurarse de que una alerta continúa en funcionamiento después de una conmutación por error, la alerta se debe definir en ambos asociados.  
  
 Para obtener más información, consulte las notas del producto sobre alertas de eventos de la creación de reflejo de la base de datos en este [sitio web de SQL Server](http://go.microsoft.com/fwlink/?linkid=62373). Estas notas del producto contienen información acerca de la configuración de alertas mediante el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , los eventos WMI de la creación de reflejo y scripts de ejemplo.  
  
> [!IMPORTANT]  
>  En todas las sesiones de creación de reflejo, se recomienda encarecidamente configurar la base de datos para que envíe una alerta de cualquier evento de cambio de estado. Significará que se ha producido algo que puede poner en riesgo los datos, a menos que un cambio de estado se espere como resultado de un cambio de configuración manual. Identificar y solucionar la causa de un cambio de estado inesperado le ayudará a proteger los datos.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para crear una alerta mediante SQL Server Management Studio**  
  
-   [Crear una alerta con un número de error](http://msdn.microsoft.com/library/03dd7fac-5073-4f86-babd-37e45a86023c)  
  
-   [Crear una alerta de evento WMI](http://msdn.microsoft.com/library/b8c46db6-408b-484e-98f0-a8af3e7ec763)  
  
 **Para supervisar la creación de reflejo de la base de datos**  
  
-   [Iniciar el Monitor de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [sp_dbmmonitoraddmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorchangealert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)  
  
-   [sp_dbmmonitorchangemonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)  
  
-   [sp_dbmmonitordropalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)  
  
-   [sp_dbmmonitordropmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorhelpalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)  
  
-   [sp_dbmmonitorhelpmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
-   [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
  
