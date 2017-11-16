---
title: "Especificar varias condiciones de búsqueda en varias columnas | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- search criteria [SQL Server], multiple conditions
- multiple search conditions
- search conditions [SQL Server], multiple
- OR operator
- AND, Criteria pane
ms.assetid: 06617729-0d0b-4da2-9890-b7e2f5cdbc7b
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d97db8a777c9ba47f4b986033ee583dfb89a3abc
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="specify-multiple-search-conditions-for-multiple-columns-visual-database-tools"></a>Especificar varias condiciones de búsqueda para varias columnas (Visual Database Tools)
Puede ampliar o reducir el alcance de la consulta incluyendo varias columnas de datos como parte de la condición de búsqueda. Por ejemplo, podría:  
  
-   Buscar los empleados que han trabajado más de cinco años en la compañía o que tienen determinados puestos de trabajo.  
  
-   Buscar un libro publicado por una editorial específica y relativo a la cocina.  
  
Para crear una consulta que busque valores en dos o más columnas, debe especificar una condición OR. Para crear una consulta que cumpla todas las condiciones de dos o más columnas, debe especificar una condición AND.  
  
## <a name="specifying-an-or-condition"></a>Especificar una condición OR  
Para crear varias condiciones vinculadas con OR, debe incluir cada condición en una columna diferente del panel Criterios.  
  
#### <a name="to-specify-an-or-condition-for-two-different-columns"></a>Para especificar una condición OR para dos columnas diferentes  
  
1.  En el [panel Criterios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), agregue las columnas en las que desee realizar la búsqueda.  
  
2.  En la columna **Filtro** de la primera columna en la que se va a realizar la búsqueda, especifique la primera condición.  
  
3.  En la columna **O...** de la segunda columna de datos en la que se va a realizar la búsqueda, especifique la segunda condición, dejando en blanco la columna **Filtro** .  
  
    El Diseñador de consultas y vistas crea una cláusula WHERE que contiene una condición OR similar a la siguiente:  
  
    ```  
    SELECT job_lvl, hire_date  
    FROM employee  
    WHERE (job_lvl >= 200) OR   
      (hire_date < '01/01/1998')  
    ```  
  
4.  Repita los pasos 2 y 3 para las demás condiciones que desee agregar. Use una columna **O...** distinta para cada una de ellas.  
  
## <a name="specifying-an-and-condition"></a>Especificar una condición AND  
Para buscar en columnas de datos diferentes utilizando condiciones vinculadas con AND, debe incluir todas las condiciones en la columna **Filtro** de la cuadrícula.  
  
#### <a name="to-specify-an-and-condition-for-two-different-columns"></a>Para especificar una condición AND para dos columnas diferentes  
  
1.  En el [panel Criterios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), agregue las columnas en las que desee realizar la búsqueda.  
  
2.  En la columna **Filtro** de la primera columna de datos en la que se va a realizar la búsqueda, especifique la primera condición.  
  
3.  En la columna **Filtro** de la segunda columna de datos, especifique la segunda condición.  
  
    El Diseñador de consultas y vistas crea una cláusula WHERE que contiene una condición AND similar a la siguiente:  
  
    ```  
    SELECT pub_id, title  
    FROM titles  
    WHERE (pub_id = '0877') AND (title LIKE '%Cook%')  
    ```  
  
4.  Repita los pasos 2 y 3 para las demás condiciones que desee agregar.  
  
## <a name="see-also"></a>Vea también  
[Combinar condiciones cuando AND tiene prioridad (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-and-has-precedence-visual-database-tools.md)  
[Combinar condiciones cuando OR tiene prioridad (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
[Convenciones para combinar condiciones de búsqueda en el panel Criterios (Visual Database Tools)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[Especificar criterios de búsqueda (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
