---
title: Solucionar problemas de estado de recursos de SQL Server (Utilidad de SQL Server) | Microsoft Docs
description: Obtenga información sobre la solución de problemas relativos al estado de recursos que identifica un UCP de SQL Server, como la sobreutilización de la CPU, el espacio de archivo o el espacio en disco asignado.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 614f07b5-f221-4013-9f8d-22964cf42270
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c6c6d499d485941d490848b68b5c8142edd0cb4b
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810699"
---
# <a name="troubleshoot-sql-server-resource-health-sql-server-utility"></a>Solucionar problemas de estado de recursos de SQL Server (Utilidad de SQL Server).
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  La solución de los problemas de mantenimiento de recursos identificados por un UCP de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría incluir reducir la utilización de la CPU en un equipo o en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o mitigar la sobreutilización de la CPU para una aplicación de capa de datos. Otros problemas podrían consistir en solucionar el uso excesivo de espacio de archivo para archivos de base de datos o el uso excesivo de espacio en disco asignado en un volumen de almacenamiento.  
  
 Tenga en cuenta que si una base de datos se encuentra en estado de "emergencia", el estado de mantenimiento mostrará el espacio de archivo de registro excesivo sobreutilizado.  
  
 Para obtener más información sobre errores de recopilación de datos que generan iconos de estado deshabilitados en la vista de lista de instancias administradas en un UCP, vea [Características y tareas de la utilidad de SQL Server](/previous-versions/sql/sql-server-2016/ee210592(v=sql.130)). Para obtener más información para empezar a trabajar con la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
 Para obtener más información sobre cómo mitigar problemas concretos de mantenimiento de recursos identificados por un UCP de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte los siguientes temas:  
  
-   [Identificar la versión y edición de SQL Server](https://go.microsoft.com/fwlink/?LinkID=178504)  
  
-   [Solucionar problemas de rendimiento en SQL Server 2008](/previous-versions/sql/sql-server-2008/dd672789(v=sql.100))  
  
