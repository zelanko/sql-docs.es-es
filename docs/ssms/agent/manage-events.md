---
title: Administrar eventos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- event-triggered jobs [SQL Server]
- forwarding events [SQL Server]
- alerts [SQL Server], forwarded events
- alerts [SQL Server], management servers
- SQL Server Agent alerts, management servers
ms.assetid: 8f4ee7f5-80df-49fd-b2b8-d020e04b6e1b
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a777dc834e835f7f06bc301158e4967d9c8117e1
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68258174"
---
# <a name="manage-events"></a>Administrar eventos
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Puede reenviar todos los mensajes de eventos que tengan o superen un nivel de gravedad de error específico a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esto se denomina *reenvío de eventos*. El servidor de reenvío es un servidor dedicado que también puede ser un servidor maestro. Puede utilizar el reenvío de eventos para centralizar la administración de alertas para un grupo de servidores, con lo que se reduce la carga de trabajo de los servidores con un alto grado de utilización.  
  
Un servidor que recibe eventos para un grupo de servidores distintos se denomina *servidor de administración de alertas*. En un entorno multiservidor, el servidor maestro se designa como servidor de administración de alertas.  
  
## <a name="advantages-of-using-an-alerts-management-server"></a>Ventajas del uso de un servidor de administración de alertas  
Entre las ventajas de configurar un servidor de administración de alertas se incluyen las siguientes:  
  
-   **Centralización**. Es posible un control centralizado y una vista consolidada de los eventos de varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un único servidor.  
  
-   **Escalabilidad**. Se pueden administrar muchos servidores físicos como un servidor lógico. Puede agregar o quitar servidores en este grupo de servidores físicos, según sea necesario.  
  
-   **Eficacia**. El tiempo de configuración disminuye gracias a que solo debe definir una vez las alertas y los operadores.  
  
## <a name="disadvantages-of-using-an-alerts-management-server"></a>Desventajas del uso de un servidor de administración de alertas  
Entre las desventajas de configurar un servidor de administración de alertas se incluyen las siguientes:  
  
-   **Aumento del tráfico**. El reenvío de eventos a un servidor de administración de alertas puede aumentar el tráfico de la red. Este aumento se puede moderar si se limita el reenvío a eventos que superan un nivel de gravedad especificado.  
  
-   **Único punto de error**. Si el servidor de administración de alertas se deja sin conexión, no se emite ninguna alerta para los eventos del grupo de servidores administrado.  
  
-   **Sobrecarga del servidor**. La administración de alertas de los eventos reenviados provoca un aumento de la carga de procesamiento en el servidor de administración de alertas.  
  
## <a name="guidelines-for-using-an-alerts-management-server"></a>Directrices de uso de un servidor de administración de alertas  
Al configurar un servidor de administración de alertas, siga las siguientes directrices:  
  
-   Para recibir eventos reenviados, el servidor de administración de alertas debe ser una instancia predeterminada de SQL Server.  
  
-   Evite ejecutar aplicaciones muy importantes o con un alto grado de uso en el servidor de administración de alertas.  
  
-   Planee cuidadosamente el tráfico de red ocasionado por la configuración de muchos servidores para compartir el mismo servidor de administración de alertas. Si se produce una congestión, reduzca el número de servidores que utilizan un servidor de administración de alertas determinado.  
  
    Los servidores registrados en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] en un servidor concreto constituyen la lista de servidores disponibles entre los que ese servidor puede elegir el servidor de reenvío de alertas.  
  
-   Defina alertas en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que requieran una respuesta específica del servidor, en lugar de reenviar las alertas al servidor de administración de alertas.  
  
    El servidor de administración de alertas considera a todos los servidores que le reenvían alertas como un único servidor lógico. Por ejemplo, un servidor de administración de alertas responde de la misma manera a un evento 605 del servidor A que a un evento 605 del servidor B.  
  
-   Tras configurar el sistema de alertas, compruebe periódicamente si hay eventos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el registro de aplicación de Microsoft Windows.  
  
    Las condiciones de error encontradas por el motor de alertas se escriben en el registro de aplicación Windows local con el nombre de origen "Agente SQL Server". Por ejemplo, si el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede enviar una notificación de correo electrónico como se ha definido, se escribirá un evento en el registro de aplicación.  
  
Si se desactiva una alerta definida localmente y se produce un evento que habría causado la activación de la alerta, el evento se reenviará al servidor de administración de alertas (si cumple la condición para el reenvío de alertas). Este reenvío permite al usuario activar y desactivar suplantaciones locales (alertas definidas localmente que también están definidas en el servidor de administración de alertas) según sea necesario, en el sitio local. También puede solicitar que se reenvíen siempre los eventos, aunque también se controlen mediante alertas locales.  
  
A continuación se presentan tareas habituales para administrar eventos en un entorno multiservidor:  
  
**Para designar un servidor de administración de alertas**  
  
-   [SQL Server Management Studio](../../ssms/agent/designate-an-events-forwarding-server-sql-server-management-studio.md)  
  
**Para definir la respuesta a una alerta**  
  
-   [SQL Server Management Studio](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)  
  
## <a name="running-event-triggered-jobs"></a>Ejecutar trabajos desencadenados por eventos  
Puede definir la ejecución de un trabajo en respuesta a una alerta. Por ejemplo, puede ejecutar un trabajo que solucione o diagnostique más exhaustivamente un problema detectado mediante la alerta.  
  
> [!NOTE]  
> Dado que un trabajo puede activar un evento, tenga cuidado de no crear un bucle recursivo de trabajos y alertas.  
  
## <a name="see-also"></a>Consulte también  
[sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/44bee7d9-7517-4071-99be-8b36f979c7cc)  
  
