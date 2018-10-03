---
title: Modificar las aplicaciones para que esperen valores bigint de sysperfinfo.cntr_value | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- sysperfinfo
- bigint values [SQL Server]
ms.assetid: b0345303-6e9a-4078-8148-6e1bce207b8c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e4f7945a5657cefb43af402523a6aee3e12eb63a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48137537"
---
# <a name="modify-applications-to-expect-bigint-values-from-sysperfinfocntrvalue"></a>Modificar las aplicaciones para obtener valores bigint de sysperfinfo.cntr_value
  sysperfinfo devuelve un `bigint` valor para la columna cntr_value.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique las aplicaciones que utilizan sysperfinfo para asegurarse de que puedan controlar los valores `bigint` de la columna cntr_value.  
  
> [!NOTE]  
>  sysperfinfo es una vista de compatibilidad. Debe utilizar en su lugar la vista de administración dinámica sys.dm_os_performance_counter.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
