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
ms.openlocfilehash: de4abebf061d2eaa419d8b71c9cf5a50d3e505db
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582948"
---
# <a name="specify-the-with-keyword-when-using-table-hints-in-90-compatibility-mode"></a>Especificar la palabra clave WITH al utilizar sugerencias de tabla en el modo de compatibilidad 90
  Con algunas excepciones, las sugerencias de tabla solo se admiten en la cláusula FROM de una consulta cuando se especifican con la palabra clave WITH. Para obtener más información, vea los temas "FROM ([!INCLUDE[tsql](../../includes/tsql-md.md)])" y "Sugerencia de tabla ([!INCLUDE[tsql](../../includes/tsql-md.md)])" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique las consultas que incluyan sugerencias de tabla en la cláusula FROM incluyendo la palabra clave WITH antes de la sugerencia de tabla.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
