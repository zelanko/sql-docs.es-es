---
title: Registro de errores de SQL Server (Grupos de disponibilidad Always On) (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 39d0c98d-75af-4dd1-b908-30d31af56f2a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e868788745efcc6525b985c861ae15cca6d3b752
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51599385"
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
  
-   Estado de concesión entre la DLL del recurso de SQL Server (en ejecución en el clúster WSFC) y la instancia de SQL Server (para obtener más información, vea [How It Works: SQL Server Always On lease timeout](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-alwayson-lease-timeout.aspx) (Cómo funciona: tiempo de espera de concesión de Always On de SQL Server)).  
  
-   Eventos de error del grupo de disponibilidad  


Los síntomas siguientes deben dar lugar a una revisión del registro de errores de SQL Server:  

-   No se puede acceder a las bases de datos de disponibilidad  
  
-   Conmutación por error inesperada del grupo de disponibilidad  
  
-   Grupo de disponibilidad en estado Resolviendo de forma inesperada  
  
-   Grupo de disponibilidad en un estado indeterminado  
  
Para obtener más información, vea [Ver el registro de errores de SQL Server &#40;SQL Server Management Studio&#41;](~/relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md).  
  
  
