---
title: Especificar la palabra clave WITH al usar sugerencias de tabla en modo de compatibilidad 90 | Documentos de Microsoft
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
- WITH keyword
- table hints [SQL Server]
ms.assetid: 7636cc85-5155-44db-baf6-df807761adb8
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: da01cc9f626f88c63a10da37540eb6fa00f1b0c3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104845"
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
  
  
