---
title: Especificar condiciones de búsqueda (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- choosing search criteria
- search conditions [SQL Server], specifying
- search criteria [SQL Server], specifying conditions
ms.assetid: 18e2c759-68ec-4efe-b208-2f73418cd9bd
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0bbff2cbc8eb04bad8c45ff5ef236acd22bb4a5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65105748"
---
# <a name="specify-search-conditions-visual-database-tools"></a>Especificar condiciones de búsqueda (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Puede especificar las filas de datos que aparecen en la consulta mediante condiciones de búsqueda. Por ejemplo, si realiza una consulta en una tabla `employee` , puede especificar que se busquen solo los empleados que trabajan en una determinada región.  
  
Las condiciones de búsqueda se especifican mediante una expresión. Normalmente, las expresiones constan de un operador y un valor de búsqueda. Por ejemplo, para buscar los empleados de una región de ventas determinada, podría especificar el siguiente criterio de búsqueda para la columna `region` :  
  
```  
='UK'  
```  
  
> [!NOTE]  
> Si trabaja con varias tablas, el Diseñador de consultas y vistas examina cada condición de búsqueda para determinar si la comparación realizada da lugar a una combinación. Si es así, el Diseñador de consultas y vistas convierte automáticamente la condición de búsqueda en una combinación. Para más información, consulte [Combinar tablas automáticamente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md).  
  
### <a name="to-specify-search-conditions"></a>Para especificar condiciones de búsqueda  
  
1.  Si aún no lo ha hecho, agregue al panel Criterios las columnas o expresiones que desee utilizar en la condición de búsqueda.  
  
    Si va a crear una consulta SELECT y no desea que las columnas o expresiones de búsqueda aparezcan en el resultado de la consulta, borre la columna **Resultados** de cada columna o expresión de búsqueda para que no aparezcan como columnas de resultados.  
  
2.  Busque la fila que contiene la columna de datos o la expresión que desea buscar y, a continuación, en la columna **Filtro** , escriba una condición de búsqueda.  
  
    > [!NOTE]  
    > Si no especifica ningún operador, el Diseñador de consultas y vistas inserta automáticamente el operador de igualdad "=".  
  
El Diseñador de consultas y vistas actualiza la instrucción SQL en el [panel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) agregando o modificando la cláusula WHERE.  
  
## <a name="see-also"></a>Consulte también  
[Reglas para especificar valores de búsqueda &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[Especificar criterios de búsqueda (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
