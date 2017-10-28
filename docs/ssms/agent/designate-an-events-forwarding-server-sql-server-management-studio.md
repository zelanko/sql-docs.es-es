---
title: "Designar un servidor de reenvío de eventos | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3a888bf925f0deec6b774891d13da7548d1fe28f
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="designate-an-events-forwarding-server-sql-server-management-studio"></a>Designar un servidor de reenvío de eventos (SQL Server Management Studio)
En este tema se describe cómo designar un servidor al que [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] reenvía eventos en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] . Observe que el reenvío de eventos se aplica a los eventos reenviados entre servidores, no a los eventos reenviados entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] hospedadas en un único equipo. Tenga en cuenta también que para recibir eventos reenviados, el servidor de administración de alertas debe ser una instancia predeterminada de SQL Server.  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para designar un servidor de reenvío de eventos. utilizando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-designate-an-events-forwarding-server"></a>Para designar un servidor de reenvío de eventos  
  
1.  En el **Explorador de objetos** , haga clic en el signo más para expandir el servidor desde el que desea reenviar eventos a otro servidor.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y seleccione **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades de Agente SQL Server –***nombre_servidor* , en **Seleccionar una página**, seleccione **Avanzadas**.  
  
4.  En **Reenvío de eventos de SQL Server**, active la casilla **Reenviar eventos a otro servidor** .  
  
5.  En la lista **Servidor** , seleccione un servidor y, a continuación, en **Eventos**, realice una de las selecciones siguientes:  
  
    -   Seleccione la opción **No controlados** para reenviar solo los eventos que no han sido controlados por alertas locales.  
  
    -   Seleccione la opción **Todos los eventos** para reenviar todos los eventos, independientemente de si han sido controlados o no por alertas locales.  
  
6.  En la lista **Si el evento tiene una gravedad de o por encima de** , haga clic en el nivel de gravedad a partir del cual se reenvían los eventos al servidor seleccionado.  
  
7.  Cuando termine, haga clic en **Aceptar**.  
  

