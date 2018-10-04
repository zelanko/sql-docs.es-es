---
title: Especificar la palabra clave WITH al utilizar las sugerencias de tabla en modo de compatibilidad 90 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH keyword
- table hints [SQL Server]
ms.assetid: 7636cc85-5155-44db-baf6-df807761adb8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8ffa920d49bac601354d9364dd308c94696def46
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227205"
---
# <a name="specify-the-with-keyword-when-using-table-hints-in-90-compatibility-mode"></a>Especificar la palabra clave WITH al utilizar sugerencias de tabla en el modo de compatibilidad 90
  Con algunas excepciones, las sugerencias de tabla solo se admiten en la cláusula FROM de una consulta cuando se especifican con la palabra clave WITH. Para obtener más información, vea los temas "FROM ([!INCLUDE[tsql](../../includes/tsql-md.md)])" y "Sugerencia de tabla ([!INCLUDE[tsql](../../includes/tsql-md.md)])" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique las consultas que incluyan sugerencias de tabla en la cláusula FROM incluyendo la palabra clave WITH antes de la sugerencia de tabla.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
