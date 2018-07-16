---
title: Configuración del Agente SQL Server para que use el Correo electrónico de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], SQL Server Agent Mail
- SQL Server Agent Mail
ms.assetid: 4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ef40a0afa36d562fa46fa243bb2ab20fb82adf35
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37318515"
---
# <a name="configure-sql-server-agent-mail-to-use-database-mail"></a>Configurar el Agente SQL Server para que use el Correo electrónico de base de datos
  En este tema se describe cómo configurar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usar Correo electrónico de base de datos a fin de enviar notificaciones y alertas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   **Antes de empezar:**  
  
-   [Requisitos previos](#Prerequisites)  
  
-   [Seguridad](#Security)  
  
-   [Para configurar el Agente SQL Server para que use el Correo electrónico de base de datos mediante Server Management Studio](#SSMSProcedure)  
  
-   [Tareas de seguimiento](#Follow_Up)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Habilitar Correo electrónico de base de datos.  
  
-   Crear una cuenta de Correo electrónico de base de datos para la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que desea usar.  
  
-   Crear un perfil del Correo electrónico de base de datos para uso de la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y agregar el usuario a la función **DatabaseMailUserRole** de la base de datos **msdb** .  
  
-   Establecer el perfil como perfil predeterminado de la base de datos **msdb** .  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 El usuario que crea cuentas de perfil y ejecuta procedimientos almacenados debe ser miembro del rol fijo de servidor sysadmin.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 **Para configurar el Agente SQL Server de modo que use el Correo electrónico de base de datos**  
  
-   En el Explorador de objetos, expanda una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Haga clic con el botón derecho en **Agente SQL Server**y, luego, haga clic en **Propiedades**.  
  
-   Haga clic en **Sistema de alerta**.  
  
-   Seleccione **Habilitar perfil de correo**.  
  
-   En la lista **Sistema de correo** , seleccione **Correo electrónico de base de datos**.  
  
-   En la lista **Perfil de correo**, seleccione un perfil de correo para el Correo electrónico de base de datos.  
  
-   Reinicie el Agente SQL Server.  
  
##  <a name="Follow_Up"></a> Tareas de seguimiento  
 Las siguientes tareas son necesarias para completar la configuración del agente con el fin de que envíe alertas y notificaciones.  
  
-   [Alertas](../../ssms/agent/alerts.md)  
  
     Las alertas se pueden configurar para notificar a un operador de una determinada condición de evento o de sistema operativo de la base de datos.  
  
-   [Operadores](../../ssms/agent/operators.md)  
  
     Los operadores son alias de personas o grupos que pueden recibir la notificación electrónica  
  
  
