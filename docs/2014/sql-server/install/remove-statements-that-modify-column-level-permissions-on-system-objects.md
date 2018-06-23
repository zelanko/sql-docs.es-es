---
title: Quite las instrucciones que modifican los permisos de nivel de columna en objetos del sistema | Documentos de Microsoft
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
- column-level permissions [SQL Server]
- removed statement permissions [SQL Server]
ms.assetid: 7f4fbbef-2696-4911-903b-63f6d9e4484a
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3bb611f4ccad6f6c5d89680857d4e96eabf79611
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113078"
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
  
  
