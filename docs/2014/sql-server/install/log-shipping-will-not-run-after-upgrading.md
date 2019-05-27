---
title: Trasvase de registros no se ejecutará después de actualizar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server]
ms.assetid: 6727cb7d-ac01-4972-a730-dbb7cdc29705
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 952a47eaa2028819908ef7e93326c31a289a0cc2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66093981"
---
# <a name="log-shipping-will-not-run-after-upgrading"></a>El trasvase de registros no se ejecutará tras la actualización
  El Asesor de actualizaciones ha detectado que se está usando el trasvase de registros. El trasvase de registros de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] es incompatible con el trasvase de registros de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y no se puede actualizar directamente. Después de la actualización a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], vuelva a configurar el trasvase de registros con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o mediante procedimientos almacenados.  
  
## <a name="see-also"></a>Vea también  
 [Categoría del trabajo del Agente SQL Server del trasvase de registros provoca un error de actualización](../../../2014/sql-server/install/sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail.md)   
 [Actualización cambiará la cuenta de Proxy de usuario de agente de SQL Server a la cuenta temporal UpgradedProxyAccount](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
