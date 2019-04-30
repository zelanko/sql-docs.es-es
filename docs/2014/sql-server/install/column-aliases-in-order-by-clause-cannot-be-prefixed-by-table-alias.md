---
title: Alias de columna en la cláusula ORDER BY no pueden ir precedidos de alias de tabla | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], columns
ms.assetid: fee7328f-6e8d-4005-930b-56fb6f17e0b2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 815e4105ca65b6bcdaa36de0554b9f6e0d3b478a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63190762"
---
# <a name="column-aliases-in-order-by-clause-cannot-be-prefixed-by-table-alias"></a>El alias de tabla no puede asignar un prefijo a los alias de columna de la cláusula ORDER BY
  En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o posterior, los alias de columna de la cláusula ORDER BY no pueden tener el prefijo del alias de tabla.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Por ejemplo, la siguiente consulta se ejecuta correctamente en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], pero devuelve un error en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY p.l  
```  
  
 [!INCLUDE[ssDEversion10](../../includes/ssdeversion10-md.md)] no interpreta `p.l` en la cláusula `ORDER BY` como una columna válida de la tabla.  
  
### <a name="exception"></a>Excepción  
 Si el alias de columna con prefijo que se especifica en la cláusula ORDER BY es un nombre de columna válido de la tabla especificada, la consulta se ejecutará sin errores; en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la semántica de la instrucción podría ser diferente. Por ejemplo, el alias de columna (`id`) especificado en la siguiente instrucción es un nombre de columna válido de la tabla `sysobjects`. En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], cuando se ejecuta la instrucción, se realiza la operación `CAST` una vez ordenado el conjunto de resultados. Esto significa que la columna `name` se utiliza en la operación de ordenación. En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], la operación `CAST` se produce antes de la operación de ordenación. Esto significa que la columna `id` de la tabla se utiliza en la operación de ordenación y devuelve el conjunto de resultados con un orden diferente al esperado.  
  
```  
SELECT CAST (o.name AS char(128)) AS id  
FROM sysobjects AS o  
ORDER BY o.id;  
```  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique las consultas que utilicen alias de columna precedidos por alias de tabla en la cláusula ORDER BY de alguna de las formas siguientes:  
  
-   Si es posible, no asigne ningún prefijo al alias de columna en la cláusula ORDER BY.  
  
-   Reemplace el alias de columna por el nombre de columna.  
  
 Por ejemplo, las siguientes consultas se ejecutan correctamente en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY l  
  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY p.LastName  
```  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
