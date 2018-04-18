---
title: Registro de errores de SQL Server (Grupos de disponibilidad Always On) (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 39d0c98d-75af-4dd1-b908-30d31af56f2a
caps.latest.revision: 4
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 535e8612c3b569a7dfcd9bbe88572e0fdc8c1f29
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/05/2018
---
# <a name="sql-server-error-log-always-on-availability-groups"></a>Registro de errores de SQL Server (Grupos de disponibilidad Always On)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El registro de errores de SQL Server informa de eventos que afectan a los grupos de disponibilidad Always On, por ejemplo:  
  
-   Comunicación con el clúster de clústeres de conmutación por error de Windows Server  
  
-   Transiciones de estado de réplicas de disponibilidad  
  
-   Transiciones de estado de bases de datos de disponibilidad  
  
-   Estado de conectividad de bases de datos de disponibilidad entre réplicas principales y secundarias  
  
-   Estado de los puntos de conexión de grupos de disponibilidad  
  
-   Estado de los agentes de escucha de grupos de disponibilidad  
  
-   Estado de concesión entre la DLL del recurso de SQL Server (en ejecución en el clúster WSFC) y la instancia de SQL Server (para obtener más información, vea [How It Works: SQL Server Always On lease timeout](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-alwayson-lease-timeout.aspx) (Cómo funciona: tiempo de espera de concesión de Always On de SQL Server)).  
  
-   Eventos de error del grupo de disponibilidad  


Los síntomas siguientes deben dar lugar a una revisión del registro de errores de SQL Server:  

-   No se puede acceder a las bases de datos de disponibilidad  
  
-   Conmutación por error inesperada del grupo de disponibilidad  
  
-   Grupo de disponibilidad en estado Resolviendo de forma inesperada  
  
-   Grupo de disponibilidad en un estado indeterminado  
  
Para obtener más información, vea [Ver el registro de errores de SQL Server &#40;SQL Server Management Studio&#41;](~/relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md).  
  
  