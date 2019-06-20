---
title: No se admite en instrucciones CREATE STATISTICS en el modo de compatibilidad de 90 o posterior con filas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH ROWS in CREATE STATISTICS statement
ms.assetid: 197b2ecf-a1a3-4a3a-a523-a0ee919c1dde
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e48602f61c09a8de76e2894a4fa808b2f39f4cbe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090966"
---
# <a name="with-rows-is-not-supported-in-create-statistics-statements-in-the-compatibility-mode-of-90-or-later"></a>No se admite WITH ROW en instrucciones CREATE STATISTICS en el modo de compatibilidad de 90 o superior
  No se admite el uso de WITH ROWS en instrucciones CREATE STATISTICS si se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el modo de compatibilidad establecido en 90 o más.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique las instrucciones CREATE STATISTICS que incluyan WITH ROWS especificando WITH SAMPLE *número* filas, o bien especificando otras opciones que cumplen con la sintaxis documentada. Para obtener más información, vea el tema "CREATE STATISTICS (Transact-SQL) en los libros en pantalla SQL Server.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
