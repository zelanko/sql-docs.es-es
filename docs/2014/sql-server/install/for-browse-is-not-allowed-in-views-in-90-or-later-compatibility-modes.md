---
title: PARA examinar no se permite en vistas en modo de compatibilidad 90 o posterior | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], FOR BROWSE clause
- FOR BROWSE clause
ms.assetid: 8f49b1c1-d877-4c46-b988-f8cdd8ac0925
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4811a3df80257b1e2d0e903fad562568eeec4ea2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66095177"
---
# <a name="for-browse-is-not-allowed-in-views-in-90-or-later-compatibility-modes"></a>No se permite FOR BROWSE en vistas en modo de compatibilidad 90 o posteriores
  El Asesor de actualizaciones ha detectado el uso de la cláusula FOR BROWSE en una vista. Se permite el uso de la cláusula FOR BROWSE (pero no se tiene en cuenta) en las vistas cuando el modo de compatibilidad de la base de datos está establecido en 80. No se permite el uso de la cláusula FOR BROWSE en las vistas cuando el modo de compatibilidad de la base de datos está establecido en 90 o más.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Cuando actualiza, las bases de datos de usuarios conservan su modo de compatibilidad. Antes de cambiar el modo de compatibilidad de la base de datos a 90 o más, elimine la cláusula FOR BROWSE de las definiciones de la vista. Para obtener más información, vea "sp_dbcmptlevel" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
