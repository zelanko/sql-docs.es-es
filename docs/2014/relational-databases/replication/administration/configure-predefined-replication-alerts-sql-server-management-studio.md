---
title: Configuración de alertas de replicación predefinidas (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 103f461c29e2bd7534ad5cb96836f06c972a6c5e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63187262"
---
# <a name="configure-predefined-replication-alerts-sql-server-management-studio"></a>Configurar alertas de replicación predefinidas (SQL Server Management Studio)
  La replicación ofrece las siguientes alertas predefinidas, que se pueden configurar para que respondan a eventos de replicación:  
  
-   **Replicación: éxito de agente**    
-   **Replicación: error de agente**    
-   **Replicación: reintento de agente**    
-   **Replicación: suscripción expirada quitada**    
-   **Replicación: Suscripción reinicializada por no pasar la validación**    
-   **Replicación: el suscriptor no ha superado la validación de datos**    
-   **Replicación: El suscriptor ha pasado la validación de datos**    
-   **Replicación: cierre personalizado del agente**  
  
 Configure estas alertas en la carpeta **Alertas** de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o en la pestaña **Advertencias** del Monitor de replicación. Para obtener más información acerca de cómo obtener acceso a esta pestaña, vea [ver información y realizar tareas mediante el monitor de replicación](../monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 Además de estas alertas, el Monitor de replicación proporciona una serie de advertencias y alertas relacionadas con el estado y el rendimiento. Para obtener más información, vea [establecer umbrales y advertencias en la infraestructura de alertas del monitor de replicación](../monitor/set-thresholds-and-warnings-in-replication-monitor.md) . Para obtener más información, consulte [Create a User-Defined Event](../../../ssms/agent/create-a-user-defined-event.md) (Crear un evento definido por el usuario).  
  
### <a name="to-configure-a-predefined-replication-alert-in-management-studio"></a>Para configurar una alerta de replicación predefinida en Management Studio  
  
1.  Conéctese al distribuidor en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.    
2.  Expanda la carpeta **Agente SQL Server** y, a continuación, la carpeta **Alertas** .    
3.  Haga clic con el botón secundario en una alerta de replicación y, a continuación, haga clic en **Propiedades**.    
4.  Establezca las opciones en ** \<** el cuadro de diálogo Propiedades de alerta de AlertName>:    
    -   En la página **General** , haga clic en **Habilitar**; especifique a qué base de datos desea que se aplique la alerta.    
    -   En la página **Respuesta** , especifique si desea que se envíe un mensaje de correo electrónico o que se ejecute un trabajo.  
  
         Si la alerta es **replicación: el suscriptor no ha superado la validación de datos**, puede especificar el trabajo de respuesta que la replicación proporciona para esta alerta: seleccione **Ejecutar trabajo**y, a continuación, haga clic en el botón Examinar (**...**). En el cuadro de diálogo **Buscar trabajo** , haga clic en **examinar**. En el cuadro de diálogo **Buscar objetos** , seleccione **Reinicializar suscripciones con errores de validación de datos**. Haga clic en **Aceptar** en los dos cuadros de diálogo abiertos. Cuando se ejecuta el trabajo, usa una llamada a procedimiento remoto (RPC) a un procedimiento almacenado que reinicializa la suscripción. Si el publicador usa un distribuidor remoto, debe definir un inicio de sesión de servidor remoto en el publicador, de manera que se pueda llevar a cabo la RPC del distribuidor al publicador.   
    -   En la página **Opciones** , personalice el texto de la respuesta.    
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-configure-an-alert-for-a-threshold-in-replication-monitor"></a>Para configurar una alerta para un umbral en el Monitor de replicación  
  
1.  En la pestaña **Advertencias** , haga clic en **Configurar alertas**.    
2.  En el cuadro de diálogo **Configurar alertas de replicación** , seleccione una alerta y haga clic en **Configurar**.    
3.  Establezca las opciones en ** \<** el cuadro de diálogo Propiedades de alerta de AlertName>:    
    -   En la página **General** , haga clic en **Habilitar**; especifique a qué base de datos desea que se aplique la alerta.    
    -   En la página **Respuesta** , especifique si desea que se envíe un mensaje de correo electrónico o que se ejecute un trabajo.    
         Si la alerta es **replicación: el suscriptor no ha superado la validación de datos**, puede especificar el trabajo de respuesta que la replicación proporciona para esta alerta: seleccione **Ejecutar trabajo**y, a continuación, haga clic en el botón Examinar (**...**). En el cuadro de diálogo **Buscar trabajo** , haga clic en **examinar**. En el cuadro de diálogo **Buscar objetos** , seleccione **Reinicializar suscripciones con errores de validación de datos**. Haga clic en **Aceptar** en los dos cuadros de diálogo abiertos. Cuando se ejecuta el trabajo, usa una llamada a procedimiento remoto (RPC) a un procedimiento almacenado que reinicializa la suscripción. Si el publicador usa un distribuidor remoto, debe definir un inicio de sesión de servidor remoto en el publicador, de manera que se pueda llevar a cabo la RPC del distribuidor al publicador.   
    -   En la página **Opciones** , personalice el texto de la respuesta.    
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]    
5.  Haga clic en **Cerrar**.  
  
## <a name="see-also"></a>Consulte también  
 [Usar alertas para eventos del Agente de replicación](../agents/use-alerts-for-replication-agent-events.md)  
  
  
