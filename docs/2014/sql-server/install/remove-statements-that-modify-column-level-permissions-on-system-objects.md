---
title: Quite las instrucciones que modifican los permisos de nivel de columna en objetos del sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- column-level permissions [SQL Server]
- removed statement permissions [SQL Server]
ms.assetid: 7f4fbbef-2696-4911-903b-63f6d9e4484a
caps.latest.revision: 21
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 217feecec3058c71a51914bde1db9e20755472db
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37316125"
---
# <a name="remove-statements-that-modify-column-level-permissions-on-system-objects"></a>Eliminar instrucciones que modifican los permisos de nivel de columna en los objetos del sistema
  El Asesor de actualizaciones ha detectado permisos de nivel de columna no estándar en objetos del sistema. No se mantendrán estos cambios en los permisos cuando se lleve a cabo la actualización. Además, ya no se admite el uso de permisos de nivel de columna en objetos del sistema. Elimine aquellas instrucciones de sus aplicaciones que establezcan permisos de nivel de columna en objetos del sistema.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Elimine todas aquellas instrucciones de sus aplicaciones que concedan, denieguen o revoquen permisos de nivel de columna para objetos del sistema.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
