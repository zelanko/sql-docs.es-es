---
title: Alertas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent alerts, event types
- SQL Server Agent alerts, names
- alerts [SQL Server], performance conditions
- alerts [SQL Server], about alerts
- WMI event responses [SQL Server Agent alerts]
- events [WMI]
- performance condition alerts [SQL Server Agent]
- alerts [SQL Server], event types
- SQL Server Agent alerts, performance conditions
- SQL Server Agent alerts, about alerts
- alerts [SQL Server], names
ms.assetid: 3f57d0f0-4781-46ec-82cd-b751dc5affef
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e4b40106834927506b84959da54aed959c8993ef
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48067015"
---
# <a name="alerts"></a>Trabajos
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera eventos que se incluyen en el registro de aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente lee el registro de aplicación y compara los eventos con las alertas definidas. Cuando el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encuentra una coincidencia, activa una alerta, que es una respuesta automatizada a un evento. Además de supervisar los eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también puede supervisar las condiciones de rendimiento y los eventos de Instrumental de administración de Windows (WMI).  
  
 Para definir una alerta, debe especificar:  
  
-   Nombre de la alerta.  
  
-   El evento o condición de rendimiento que desencadena la alerta.  
  
-   La acción que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza como respuesta al evento o condición de rendimiento.  
  
## <a name="naming-an-alert"></a>Asignar nombre a una alerta  
 Cada alerta debe tener un nombre. Los nombres de las alertas deben ser exclusivos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y no pueden tener más de **128** caracteres.  
  
## <a name="selecting-an-event-type"></a>Seleccionar un tipo de evento  
 Una alerta responde a un tipo de evento específico. Las alertas responden a los siguientes tipos de evento:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eventos  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] condiciones de rendimiento  
  
-   Eventos de WMI  
  
 El tipo de evento determina los parámetros que se utilizan para especificar el evento preciso.  
  
## <a name="specifying-a-sql-server-event"></a>Especificar un evento de SQL Server  
 Puede especificar una alerta para que se produzca en respuesta a uno o más eventos. Utilice los siguientes parámetros para especificar los eventos que desencadenan una alerta:  
  
-   **Número de error**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente activa una alerta cuando se produce un error específico. Por ejemplo, puede especificar el número de error 2571 para responder a los intentos no autorizados de invocar comandos de consola de base de datos (DBCC).  
  
-   **Nivel de gravedad**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente activa una alerta cuando se produce un error de la gravedad específica. Por ejemplo, puede especificar el nivel de gravedad 15 para responder a errores de sintaxis en instrucciones Transact-SQL.  
  
-   **Base de datos**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente solo activa una alerta cuando el evento tiene lugar en una base de datos determinada. Esta opción se aplica además del número de error o el nivel de gravedad. Por ejemplo, si una instancia contiene una base de datos que se utiliza para la producción y una base de datos que se utiliza para la elaboración de informes, puede definir una alerta que responda a los errores de sintaxis solo en la base de datos de producción.  
  
-   **Texto del evento**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente activa una alerta cuando el evento especificado contiene una cadena de texto determinada en el mensaje de evento. Por ejemplo, puede definir una alerta que responda a los mensajes que contienen el nombre de una tabla o restricción determinada.  
  
## <a name="selecting-a-performance-condition"></a>Seleccionar una condición de rendimiento  
 Puede especificar una alerta para que se active en respuesta a una condición de rendimiento determinada. En este caso, debe especificar el contador de rendimiento que se supervisa, un umbral para la alerta y el comportamiento que el contador debe mostrar si la alerta tiene lugar. Para establecer una condición de rendimiento, debe definir los siguientes elementos en la página [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] General **del cuadro de diálogo** Nueva alerta **o** Propiedades de alerta **del Agente** :  
  
-   **Objeto**  
  
     El objeto es el área de rendimiento que se supervisa.  
  
-   **Contador**  
  
     Un contador es un atributo del área que se supervisa.  
  
-   **Instancia**  
  
     La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define la instancia específica (si la hay) del atributo que se va a supervisar.  
  
-   **Alertar si el contador** y **Valor**  
  
     El umbral de la alerta y el comportamiento que genera la alerta. El umbral es un número. El comportamiento **puede ser: está por debajo de**, **es igual a**o **está por encima de un número especificado en Valor**. El **Valor** es un número que describe el contador de condición de rendimiento. Por ejemplo, para establecer una alerta que tendrá lugar para el objeto de rendimiento **SQLServer:Locks** cuando pasen 30 minutos del **Tiempo de espera de bloqueos** , deberá elegir **está por encima de** y **especificar 30 para el valor**.  
  
     En otro ejemplo, puede especificar que una alerta tenga lugar para el objeto de rendimiento **SQLServer:Transactions** cuando el espacio disponible en **tempdb** esté por debajo de 1000 KB. Para ello, elegirá el contador **Espacio disponible en tempdb (KB)**, **está por debajo de**y un **Valor** de **1000**.  
  
    > [!NOTE]  
    >  Se muestrean periódicamente los datos de rendimiento, lo que puede causar una pequeña demora (unos segundos) entre el momento en que se alcanza el umbral y la activación de la alerta relativa al rendimiento.  
  
## <a name="selecting-a-wmi-event"></a>Seleccionar un evento de WMI  
 Puede especificar que una alerta tenga lugar como respuesta a un determinado evento de WMI. Para seleccionar un evento de WMI, debe definir lo siguiente en la página [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] General **del cuadro de diálogo** Nueva alerta **o** Propiedades de alerta **del Agente** :  
  
-   **Espacio de nombres**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente se registra como un cliente de WMI en el espacio de nombres de WMI que se proporciona para consultar los eventos.  
  
-   **Query**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente usa la instrucción de Lenguaje de consulta de Instrumental de administración de Windows (WQL) proporcionada para identificar el evento específico.  
  
 A continuación se incluyen vínculos a las tareas más comunes:  
  
 **Para crear una alerta basada en un número de mensaje**  
  
-   [SQL Server Management Studio](create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **Para crear una alerta basada en niveles de gravedad**  
  
-   [SQL Server Management Studio](create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **Para crear una alerta basada en un evento de WMI**  
  
-   [SQL Server Management Studio](create-a-wmi-event-alert.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **Para definir la respuesta a una alerta**  
  
-   [SQL Server Management Studio](../sql-server-management-studio-ssms.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)  
  
 **Para crear el mensaje de error de un evento definido por el usuario**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql)  
  
 **Para modificar el mensaje de error de un evento definido por el usuario**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-altermessage-transact-sql)  
  
 **Para eliminar el mensaje de error de un evento definido por el usuario**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-dropmessage-transact-sql)  
  
 **Para deshabilitar o volver a activar una alerta**  
  
-   [SQL Server Management Studio](disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql)  
  
## <a name="see-also"></a>Vea también  
 [Usar objetos de SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md)  
  
  
