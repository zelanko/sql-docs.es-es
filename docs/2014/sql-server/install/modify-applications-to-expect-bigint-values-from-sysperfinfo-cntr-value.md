---
title: Modifique las aplicaciones para esperar valores BIGINT de sysperfinfo. cntr_value | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sysperfinfo
- bigint values [SQL Server]
ms.assetid: b0345303-6e9a-4078-8148-6e1bce207b8c
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 108a9b981debc95e182b16847c39a03d4b242088
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012214"
---
# <a name="modify-applications-to-expect-bigint-values-from-sysperfinfocntr_value"></a>Modificar las aplicaciones para obtener valores bigint de sysperfinfo.cntr_value
  sysperfinfo devuelve un `bigint` valor para la columna cntr_value.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique las aplicaciones que utilizan sysperfinfo para asegurarse de que puedan controlar los valores `bigint` de la columna cntr_value.  
  
> [!NOTE]  
>  sysperfinfo es una vista de compatibilidad. Debe utilizar en su lugar la vista de administración dinámica sys.dm_os_performance_counter.  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
