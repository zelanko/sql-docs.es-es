---
title: Combinar tablas manualmente (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- manual joins [SQL Server]
- joins [SQL Server], manual
- joins [SQL Server], creating
ms.assetid: 9c785356-646b-4c87-82d4-25efd6051d9d
author: stevestein
ms.author: sstein
ms.openlocfilehash: fe3dcd7f2affdbeb2e2fa5769f1aa6d02d27d5ac
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064947"
---
# <a name="join-tables-manually-visual-database-tools"></a>Combinar tablas manualmente (Visual Database Tools)
  Cuando se agregan dos o más tablas a una consulta, el [Diseñador de consultas y vistas](visual-database-tools.md) intenta combinarlas en función de datos comunes o de información almacenada en la base de datos acerca de cómo se relacionan las tablas. Para detalles, consulte [Combinar tablas automáticamente &#40;Visual Database Tools&#41;](join-tables-automatically-visual-database-tools.md). No obstante, si el Diseñador de consultas y vistas no ha combinado las tablas automáticamente o si desea crear otras condiciones de combinación entre tablas, puede combinar las tablas de forma manual.  
  
 Puede crear combinaciones basadas en comparaciones entre dos columnas cualesquiera y no solo entre columnas que contengan la misma información. Por ejemplo, si la base de datos contiene dos tablas, `titles` y `roysched`, puede comparar los valores de la columna `ytd_sales` de la tabla `titles` con las columnas `lorange` y `hirange` de la tabla `roysched` . Esta combinación le permitirá buscar títulos cuyas ventas anuales acumuladas estén comprendidas entre los intervalos inferior y superior de los pagos por regalías (royalties).  
  
> [!TIP]  
>  Las combinaciones funcionan con más rapidez si se indizan las columnas de la condición de combinación. En algunas ocasiones, la combinación realizada en columnas no indizadas puede dar lugar a una consulta lenta.  
  
### <a name="to-manually-join-tables-or-table-structured-objects"></a>Para combinar manualmente tablas u objetos estructurados en tablas  
  
1.  Agregue al [panel Diagrama](diagram-pane-visual-database-tools.md) los objetos que desee combinar.  
  
2.  Arrastre el nombre de la columna de combinación de la primera tabla u objeto estructurado en tabla y colóquelo en la columna relacionada de la segunda tabla u objeto estructurado en tabla. No puede basar una combinación en columnas del tipo de datos `text`, `ntext` o `mage`.  
  
    > [!NOTE]  
    >  Las columnas de combinación deben tener el mismo tipo de datos (o compatibles). Por ejemplo, si la columna de combinación de la primera tabla es una fecha, deberá relacionarla con una columna de fecha de la segunda tabla. O bien, si la primera columna de combinación es un entero, la columna de combinación relacionada debe ser también de un tipo de datos entero, pero puede tener un tamaño diferente. El Diseñador de consultas y vistas no comprobará los tipos de datos de las columnas que utilice para crear una combinación, pero al ejecutar la consulta, la base de datos mostrará un error si los tipos de datos no son compatibles.  
  
3.  Si es necesario, cambie el operador de combinación; de forma predeterminada, el operador es un signo igual (=). Para detalles, consulte [Modificar operadores de combinación &#40;Visual Database Tools&#41;](modify-join-operators-visual-database-tools.md).  
  
 El Diseñador de consultas y vistas agrega una cláusula INNER JOIN a la instrucción SQL en el [panel SQL](sql-pane-visual-database-tools.md). Puede cambiar el tipo a una combinación externa. Para detalles, consulte [Crear combinaciones externas &#40;Visual Database Tools&#41;](create-outer-joins-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte también  
 [Realizar consultas con combinaciones &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)  
  
  
