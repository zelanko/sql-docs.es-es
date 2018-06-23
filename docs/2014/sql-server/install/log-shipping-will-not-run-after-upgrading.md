---
title: No se ejecutará después de actualizar de trasvase de registros | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- log shipping [SQL Server]
ms.assetid: 6727cb7d-ac01-4972-a730-dbb7cdc29705
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3187edcc72fca15e22644bcce107bf161dd0c645
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111703"
---
# <a name="log-shipping-will-not-run-after-upgrading"></a>El trasvase de registros no se ejecutará tras la actualización
  El Asesor de actualizaciones ha detectado que se está usando el trasvase de registros. El trasvase de registros de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] es incompatible con el trasvase de registros de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y no se puede actualizar directamente. Después de la actualización a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], vuelva a configurar el trasvase de registros con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o mediante procedimientos almacenados.  
  
## <a name="see-also"></a>Vea también  
 [Categoría del trabajo de trasvase del registro de agente SQL Server provoca un error de actualización](../../../2014/sql-server/install/sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail.md)   
 [Actualización cambiará la cuenta de Proxy de usuario de agente de SQL Server a la cuenta temporal UpgradedProxyAccount](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
