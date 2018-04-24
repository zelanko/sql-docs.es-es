---
title: Cambiar la dirección IP de una instancia de clúster de conmutación por error | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: failover-clusters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- modifying IP addresses
- failover clustering [SQL Server], IP addresses
- IP addresses [SQL Server]
- clusters [SQL Server], IP addresses
ms.assetid: b685f400-cbfe-4c5d-a070-227a1123dae4
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 692598e4fa27e18c40767d14e46aa48d4d03d265
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="change-the-ip-address-of-a-failover-cluster-instance"></a>Cambiar la dirección IP de una instancia de clúster de conmutación por error
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo se cambia el recurso de dirección IP de una instancia de clúster de conmutación por error (FCI) AlwaysOn con el complemento Administrador de clústeres de conmutación por error. El complemento Administrador de clústeres de conmutación por error es la aplicación de administración de clústeres del servicio de clústeres de conmutación por error de Windows Server (WSFC).  
  
-   **Before you begin:**  [Security](#Security)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
 Antes de comenzar, revise el siguiente tema de los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] : [Antes de instalar los clústeres de conmutación por error](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Para mantener o actualizar una DCI, debe ser administrador local y tener permisos para iniciar sesión como servicio en todos los nodos de la FCI.  
  
##  <a name="WSFC"></a> Usar el complemento Administrador de clústeres de conmutación por error  
 **Para cambiar el recurso de dirección IP de una FCI**  
  
1.  Abra el complemento Administrador de clústeres de conmutación por error.  
  
2.  Expanda el nodo **servicios y aplicaciones** en el panel izquierdo y haga clic en la FCI.  
  
3.  En el panel derecho, en la categoría **Nombre del servidor** , haga clic con el botón derecho en la instancia de SQL Server y seleccione la opción **Propiedades** para abrir el cuadro de diálogo **Propiedades** .  
  
4.  En la pestaña **General** , cambie el recurso de dirección IP.  
  
5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
6.  En el panel derecho, haga clic con el botón derecho en la dirección IP1 de SQL (nombre de la instancia en clúster de conmutación por error) y seleccione **Poner sin conexión**. Verá que el estado de la dirección IP1 de SQL (nombre de la instancia en clúster de conmutación por error), el nombre de red de SQL (nombre de la instancia en clúster de conmutación por error) y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pasa de En línea a Sin conexión pendiente y luego a Sin conexión.  
  
7.  En el panel derecho, haga clic con el botón derecho en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]y seleccione **Poner en línea**. Verá que el estado de la dirección IP1 de SQL (nombre de la instancia en clúster de conmutación por error), el nombre de red de SQL (nombre de la instancia en clúster de conmutación por error) y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pasa de Sin conexión a Sin conexión pendiente y luego a En línea.  
  
8.  Cierre el complemento Administrador de clústeres de conmutación por error.  
  
  
