---
title: Designar un servidor de reenvío de eventos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b79da95e2709e2bb5ff3a3d76cac06b2a4268f2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68189383"
---
# <a name="designate-an-events-forwarding-server-sql-server-management-studio"></a>Designate an Events Forwarding Server (SQL Server Management Studio)
  En este tema se describe cómo designar un servidor al [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que reenvía [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] eventos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mediante. Observe que el reenvío de eventos se aplica a los eventos reenviados entre servidores, no a los eventos reenviados entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hospedadas en un único equipo. Tenga en cuenta también que para recibir eventos reenviados, el servidor de administración de alertas debe ser una instancia predeterminada de SQL Server.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para designar un servidor de reenvío de eventos, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-designate-an-events-forwarding-server"></a>Para designar un servidor de reenvío de eventos  
  
1.  En el **Explorador de objetos** , haga clic en el signo más para expandir el servidor desde el que desea reenviar eventos a otro servidor.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y seleccione **propiedades**.  

3.  En el cuadro de diálogo **Propiedades de Agente SQL Server -**_nombre_de_servidor_, en **Seleccionar una página**, haga clic en **Avanzadas**.  

4.  En **Reenvío de eventos de SQL Server**, active la casilla **Reenviar eventos a otro servidor** .  
  
5.  En la lista **Servidor** , seleccione un servidor y, a continuación, en **Eventos**, realice una de las selecciones siguientes:  
  
    -   Seleccione la opción **No controlados** para reenviar solo los eventos que no han sido controlados por alertas locales.  
  
    -   Seleccione la opción **Todos los eventos** para reenviar todos los eventos, independientemente de si han sido controlados o no por alertas locales.  
  
6.  En la lista **Si el evento tiene una gravedad de o por encima de** , haga clic en el nivel de gravedad a partir del cual se reenvían los eventos al servidor seleccionado.  
  
7.  Cuando termine, haga clic en **Aceptar**.  
  
  
