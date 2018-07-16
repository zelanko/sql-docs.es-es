---
title: Operadores de combinación externa *= y =* no se admiten en los modos de compatibilidad 90 o posterior | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- outer joins
- =* join
- '*= join'
- joins [SQL Server]
ms.assetid: ca4aa11f-1048-411f-9c6c-3d0a8e319f2f
caps.latest.revision: 12
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 579565320855694166f57039402e3fbef14183d5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37255447"
---
# <a name="outer-join-operators--and--are-not-supported-in-90-or-later-compatibility-modes"></a>Operadores de combinación externa *= y =* no se admiten en los modos de compatibilidad 90 o posterior
  El Asesor de actualizaciones ha detectado el uso de operadores de combinación externa * = y =\*. Estos operadores no se admiten en los modos de compatibilidad 90 y posteriores. Cuando actualiza, las bases de datos de usuarios conservan su modo de compatibilidad. Las instrucciones que usan estos operadores generarán un error.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Antes de cambiar el modo de compatibilidad de base de datos a 90 o posterior, modifique las instrucciones que usan los operadores de combinación externa * = y =\* utilizar palabras clave equivalentes de combinación externa. El ejemplo siguiente muestra una consulta que utiliza el operador `*=` y una consulta equivalente que utiliza las palabras clave `LEFT OUTER JOIN`.  
  
```  
-- This query uses an old-style outer join operator.  
USE pubs  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee, jobs   
WHERE employee.job_id *= jobs.job_id  
ORDER BY employee.job_id  
  
-- This query uses the ANSI standard keywords LEFT OUTER JOIN.  
USE pubs;  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee LEFT OUTER JOIN jobs ON   
    employee.job_id = jobs.job_id  
ORDER BY employee.job_id  
```  
  
 Para obtener más información sobre combinaciones externas, vea "Usar combinaciones externas" en los Libros en pantalla de SQL Server.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
