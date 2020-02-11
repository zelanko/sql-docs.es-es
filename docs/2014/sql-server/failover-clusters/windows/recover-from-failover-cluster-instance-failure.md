---
title: Recuperarse de un error en una instancia de clúster de conmutación por error | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- clusters [SQL Server], recovery from failure
- failover clustering [SQL Server], recovery from failure
- hardware failures [SQL Server]
- recovering failover cluster failures [SQL Server]
ms.assetid: 3d151d0c-e841-4325-8606-c094de37d7d1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0c4da45e57342288cc23a9783709666f4c02d0bc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63050018"
---
# <a name="recover-from-failover-cluster-instance-failure"></a>Recuperarse de un error en una instancia de clúster de conmutación por error
  En este tema se describe cómo puede recuperarse de los errores de clúster usando el complemento Administrador de clústeres de conmutación por error después de que se produzca una conmutación por error en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. El complemento Administrador de clústeres de conmutación por error es la aplicación de administración de clústeres del servicio de clústeres de conmutación por error de Windows Server (WSFC).  
  
-   [Recuperarse de un error irreparable](#Scenario1)  
  
-   [Recuperarse de un error de software](#Scenario2)  
  
##  <a name="Scenario1"></a>Recuperarse de un error irreparable  
 Siga estos pasos para recuperarse de un error irreparable. El error puede deberse, por ejemplo, a un error del controlador de disco o del sistema operativo. En este caso, el error se debe a un problema de hardware en el nodo 1 de un clúster de dos nodos.  
  
1.  Cuando se produce un error en el nodo 1, la FCI de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conmuta al nodo 2.  
  
2.  Desaloje el nodo 1 de la FCI. Para ello, en el nodo 2, abra el complemento Administrador de clústeres de conmutación por error, haga clic con el botón derecho en Node1, haga clic en **Acciones de desplazamiento**y luego en **Expulsar el nodo**.  
  
3.  Compruebe que el nodo 1 se ha desalojado de la definición del clúster.  
  
4.  Instale el hardware nuevo que va a sustituir al que ha producido el error en el nodo 1.  
  
5.  Mediante el complemento Administrador de clústeres de conmutación por error, agregue el nodo 1 al clúster existente. Para obtener más información, vea [Antes de instalar los clústeres de conmutación por error](../install/before-installing-failover-clustering.md).  
  
6.  Asegúrese de que las cuentas de administrador son las mismas en todos los nodos de clúster.  
  
7.  Ejecute el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para agregar el nodo 1 a la FCI. Para obtener más información, vea [Agregar o quitar nodos en un clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
##  <a name="Scenario2"></a>Recuperación de un error de reparable  
 Siga estos pasos para recuperarse de un error reparable. En este caso, el error se produce porque el nodo 1 está inactivo o sin conexión pero todavía se puede recuperar. Este error podría estar causado por un error del sistema operativo, un error de hardware o un error de la propia instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
1.  Cuando se produce un error en el nodo 1, la FCI conmuta al nodo 2.  
  
2.  Solucione el problema del nodo 1.  
  
3.  Asegúrese de que todos los nodos están en línea y de que el servicio WSFC funciona.  
  
4.  Realice la conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] al nodo recuperado.  
  
  
