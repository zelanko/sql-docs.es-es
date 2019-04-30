---
title: Crear combinaciones externas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- outer joins
- joins [SQL Server], outer
ms.assetid: 18de47b1-f936-427d-b852-fe6d20334f71
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cd5c9a9cb2e40c7b0a235ff848c1f9a0025773a5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184309"
---
# <a name="create-outer-joins-visual-database-tools"></a>Crear combinaciones externas (Visual Database Tools)
  De forma predeterminada, el [Diseñador de consultas y vistas](visual-database-tools.md) crea una combinación interna entre tablas. Las combinaciones internas eliminan las filas que no coinciden con alguna fila de la otra tabla. Sin embargo, las combinaciones externas devuelven todas las filas de una de las tablas o vistas mencionadas en la cláusula FROM, como mínimo, siempre que tales filas cumplan alguna de las condiciones de búsqueda de WHERE o HAVING. Si desea incluir filas de datos en el conjunto de resultados que no se correspondan con ninguna fila de la tabla combinada, puede crear una combinación externa.  
  
 Cuando se crea una combinación externa, el orden en que aparecen las tablas en la instrucción SQL (el que se muestra en el panel SQL) es importante. La primera tabla que se agrega se convierte en la tabla "de la izquierda", y la segunda en la "de la derecha". (El orden real en el que aparecen las tablas en el [panel Diagrama](diagram-pane-visual-database-tools.md) es irrelevante). Cuando se especifica una combinación externa izquierda o derecha, se hace referencia al orden en el que se agregaron las tablas a la consulta y al orden en el que aparecen en la instrucción SQL en el [panel SQL](sql-pane-visual-database-tools.md).  
  
### <a name="to-create-an-outer-join"></a>Para crear una combinación externa  
  
1.  Cree la combinación, ya sea automática o manualmente. Para detalles, consulte [Combinar tablas automáticamente &#40;Visual Database Tools&#41;](join-tables-automatically-visual-database-tools.md) o [Combinar tablas manualmente &#40;Visual Database Tools&#41;](join-tables-manually-visual-database-tools.md).  
  
2.  Seleccione la línea de combinación en el panel Diagrama y, a continuación, desde el **Diseñador de consultas** menú, elija **seleccionar todas las filas de \<tablename >**, seleccione el comando que incluye la tabla cuyo adicional filas que van a incluir.  
  
    -   Elija la primera tabla para crear una combinación externa izquierda.  
  
    -   Elija la segunda tabla para crear una combinación externa derecha.  
  
    -   Elija ambas tablas para crear una combinación externa completa.  
  
 Cuando se especifica una combinación externa, el Diseñador de consultas y vistas modifica la línea de combinación para indicar que se trata de una combinación externa.  
  
 Asimismo, el Diseñador de consultas y vistas modifica la instrucción SQL en el panel SQL para reflejar el cambio en el tipo de combinación, como se muestra en la siguiente instrucción:  
  
```  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee LEFT OUTER JOIN jobs ON   
    employee.job_id = jobs.job_id  
```  
  
 Puesto que las combinaciones externas incluyen filas no coincidentes, puede utilizarlas para buscar filas que infrinjan las restricciones FOREIGN KEY. Para ello, cree una combinación externa y, a continuación, agregue una condición de búsqueda para buscar las filas en las que la columna de clave principal de la tabla de la derecha sea NULL. Por ejemplo, la siguiente combinación externa busca las filas de la tabla `employee` que no tienen filas correspondientes en la tabla `jobs` :  
  
```  
SELECT employee.emp_id, employee.job_id  
FROM employee LEFT OUTER JOIN jobs   
   ON employee.job_id = jobs.job_id  
WHERE (jobs.job_id IS NULL)  
```  
  
## <a name="see-also"></a>Vea también  
 [Consultas con combinaciones &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)   
 [Cuadro de diálogo Combinar &#40;Visual Database Tools&#41;](join-dialog-box-visual-database-tools.md)  
  
  
