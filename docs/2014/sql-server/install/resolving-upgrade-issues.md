---
title: Resolver problemas de actualización | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installing Upgrade Advisor
- Upgrade Advisor [SQL Server], reference
- component issue resolution [Upgrade Advisor]
- resolving upgrade issues
- upgrade blocks [Upgrade Advisor]
- detecting upgrade issues
- finding upgrade issues
- Upgrade Advisor [SQL Server], blocking issues
- configurations preventing upgrading [Upgrade Advisor]
- locating upgrade issues
- blocking issues [Upgrade Advisor]
- issues preventing upgrading [Upgrade Advisor]
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, reference
- analyzing system [Upgrade Advisor], resolving issues
- settings preventing upgrading [Upgrade Advisor]
- upgrade issue reference [Upgrade Advisor]
- identifying upgrade issues
- fixing upgrade issues [Upgrade Advisor]
ms.assetid: 113eb435-8d36-4ed6-9790-b5e4c14809c8
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6072fb3c1d52048832bd6d07f34828c84eb2d491
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112151"
---
# <a name="resolving-upgrade-issues"></a>Resolver problemas de la actualización
  En los temas de esta sección se describen problemas de actualización que se pueden detectar, así como los que no se pueden detectar, pero que podrían afectar a la actualización o al uso de la aplicación tras su actualización. Los problemas se han organizado por componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Problemas de actualización de información de última hora](../../../2014/sql-server/install/late-breaking-upgrade-issues.md)  
  
-   [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
-   [Problemas de actualización de búsqueda de texto completo](../../../2014/sql-server/install/full-text-search-upgrade-issues.md)  
  
-   [Problemas de actualización de replicación](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
-   [Problemas de actualización de Reporting Services &#40;Asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
-   [Problemas de actualización de agente SQL Server](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
## <a name="issues-that-prevent-upgrading"></a>Problemas que impiden la actualización  
 Algunas configuraciones o valores de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden impedir que se realice la actualización a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Si el programa de instalación detecta estos problemas cuando instala [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], detiene el proceso de actualización y le pide que ejecute el Asesor de actualizaciones para corregir cualquier problema de bloqueos.  
  
### [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
 Si aparecen las siguientes tareas en el informe de actualización de [!INCLUDE[ssDE](../../includes/ssde-md.md)], deberá llevar a cabo las acciones necesarias antes de actualizar a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   [Desasociar la base de datos ID 32767](../../../2014/sql-server/install/detach-database-id-32767.md)  
  
-   [Cambiar el nombre de los inicios de sesión que coincidan con nombres de rol fijo de servidor](../../../2014/sql-server/install/rename-logins-matching-fixed-server-role-names.md)  
  
-   [Cambiar el nombre de usuario del sistema](../../../2014/sql-server/install/rename-user-sys.md)  
  
-   [Utilizar sp_rename para cambiar el nombre de índice duplicado](../../../2014/sql-server/install/use-sp-rename-to-rename-duplicate-index-name.md)  
  
## <a name="see-also"></a>Vea también  
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
