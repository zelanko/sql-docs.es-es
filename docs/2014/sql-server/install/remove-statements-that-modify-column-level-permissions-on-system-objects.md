---
title: Quite las instrucciones que modifican los permisos de nivel de columna en objetos del sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- column-level permissions [SQL Server]
- removed statement permissions [SQL Server]
ms.assetid: 7f4fbbef-2696-4911-903b-63f6d9e4484a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f61990ae0eb35a399a1efca4a5a2cf754892e3d0
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582848"
---
# <a name="remove-statements-that-modify-column-level-permissions-on-system-objects"></a>Eliminar instrucciones que modifican los permisos de nivel de columna en los objetos del sistema
  El Asesor de actualizaciones ha detectado permisos de nivel de columna no estándar en objetos del sistema. No se mantendrán estos cambios en los permisos cuando se lleve a cabo la actualización. Además, ya no se admite el uso de permisos de nivel de columna en objetos del sistema. Elimine aquellas instrucciones de sus aplicaciones que establezcan permisos de nivel de columna en objetos del sistema.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Elimine todas aquellas instrucciones de sus aplicaciones que concedan, denieguen o revoquen permisos de nivel de columna para objetos del sistema.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
