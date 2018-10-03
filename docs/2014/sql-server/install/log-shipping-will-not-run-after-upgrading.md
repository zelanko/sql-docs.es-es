---
title: Trasvase de registros no se ejecutará después de actualizar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server]
ms.assetid: 6727cb7d-ac01-4972-a730-dbb7cdc29705
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e4aac17eead48a142ebcba07cd769fef5a469d3e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48201945"
---
# <a name="log-shipping-will-not-run-after-upgrading"></a>El trasvase de registros no se ejecutará tras la actualización
  El Asesor de actualizaciones ha detectado que se está usando el trasvase de registros. El trasvase de registros de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] es incompatible con el trasvase de registros de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y no se puede actualizar directamente. Después de la actualización a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], vuelva a configurar el trasvase de registros con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o mediante procedimientos almacenados.  
  
## <a name="see-also"></a>Vea también  
 [Categoría del trabajo del Agente SQL Server del trasvase de registros provoca un error de actualización](../../../2014/sql-server/install/sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail.md)   
 [Actualización cambiará la cuenta de Proxy de usuario de agente de SQL Server a la cuenta temporal UpgradedProxyAccount](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
