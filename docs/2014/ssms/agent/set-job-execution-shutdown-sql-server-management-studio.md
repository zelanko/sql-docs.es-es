---
title: Configurar el cierre de la ejecución de trabajos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
- SQL Server Agent jobs, execution shutdowns
ms.assetid: ac23e88f-53fc-41de-bb16-0c27c002d5a5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 935a54d1f3b7606ac4f761e9e49953edfd7f77e6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091995"
---
# <a name="set-job-execution-shutdown-sql-server-management-studio"></a>Configurar el cierre de la ejecución de trabajos (SQL Server Management Studio)
  En este tema se describe cómo configurar el tiempo que el Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esperará a que finalice la ejecución de los trabajos antes de que el propio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finalice en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para establecer un tiempo de cierre para un trabajo del Agente SQL Server, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden establecer el tiempo que el Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esperará a que finalice la ejecución de los trabajos antes de que el propio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finalice. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-set-job-execution-shutdown"></a>Para configurar el cierre de la ejecución de trabajos  
  
1.  En **El Explorador de objetos** , haga clic en el signo más para expandir el servidor en el que desea establecer un intervalo de cierre de la ejecución de trabajos.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y seleccione **Propiedades**.  
  
3.  En **Seleccionar una página**, seleccione **Sistema de trabajo**.  
  
4.  Configure **Intervalo de tiempo de espera de cierre** en segundos para aumentar o reducir dicho intervalo. Así se determina el tiempo que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] va a esperar a que finalice la ejecución de los trabajos antes de que se cierre el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
