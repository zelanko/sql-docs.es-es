---
title: Solucionar problemas de estado de recursos de SQL Server (Utilidad de SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: maintenance-plans
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 614f07b5-f221-4013-9f8d-22964cf42270
caps.latest.revision: "7"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4b8b2c608c77443858f915cb9e7b3a84c96d2e86
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="troubleshoot-sql-server-resource-health-sql-server-utility"></a>Solucionar problemas de estado de recursos de SQL Server (Utilidad de SQL Server).
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] La solución de los problemas de mantenimiento de recursos identificados por un UCP de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría incluir mitigar la sobreutilización de la CPU en un equipo o en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o mitigar la sobreutilización de la CPU para una aplicación de capa de datos. Otros problemas podrían consistir en solucionar el uso excesivo de espacio de archivo para archivos de base de datos o el uso excesivo de espacio en disco asignado en un volumen de almacenamiento.  
  
 Tenga en cuenta que si una base de datos se encuentra en estado de “emergencia”, el estado de mantenimiento mostrará el espacio de archivo de registro excesivo sobreutilizado.  
  
 Para obtener más información sobre errores de recopilación de datos que generan iconos de estado deshabilitados en la vista de lista de instancias administradas en un UCP, vea [Características y tareas de la utilidad de SQL Server](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453). Para obtener más información para empezar a trabajar con la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
 Para obtener más información sobre cómo mitigar problemas concretos de mantenimiento de recursos identificados por un UCP de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte los siguientes temas:  
  
-   [Identificar la versión y edición de SQL Server](http://go.microsoft.com/fwlink/?LinkID=178504)  
  
-   [Solucionar problemas de rendimiento en SQL Server 2008](http://go.microsoft.com/fwlink/?LinkId=151354)  
  
  
