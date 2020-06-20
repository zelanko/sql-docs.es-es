---
title: FOR BROWSE no se permite en vistas en los modos de compatibilidad 90 o posteriores | Microsoft Docs
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
ms.openlocfilehash: 251e0ae2ff6f19dfcff3b0f8056f6697c1bfc40d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012619"
---
# <a name="for-browse-is-not-allowed-in-views-in-90-or-later-compatibility-modes"></a>No se permite FOR BROWSE en vistas en modo de compatibilidad 90 o posteriores
  El Asesor de actualizaciones ha detectado el uso de la cláusula FOR BROWSE en una vista. Se permite el uso de la cláusula FOR BROWSE (pero no se tiene en cuenta) en las vistas cuando el modo de compatibilidad de la base de datos está establecido en 80. No se permite el uso de la cláusula FOR BROWSE en las vistas cuando el modo de compatibilidad de la base de datos está establecido en 90 o más.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Cuando actualiza, las bases de datos de usuarios conservan su modo de compatibilidad. Antes de cambiar el modo de compatibilidad de la base de datos a 90 o más, elimine la cláusula FOR BROWSE de las definiciones de la vista. Para obtener más información, vea "sp_dbcmptlevel" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
