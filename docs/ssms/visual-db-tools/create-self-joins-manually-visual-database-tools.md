---
title: Crear autocombinaciones manualmente
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- self-joins
- manual joins [SQL Server]
- joins [SQL Server], self
ms.assetid: 910ed516-cb84-481b-95d0-cba3e89afdba
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 162f2e872d1feedd3cecdf54b766ed8e3a43365b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000002"
---
# <a name="create-self-joins-manually-visual-database-tools"></a>Crear autocombinaciones manualmente (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Puede combinar una tabla consigo misma aunque no tenga una relación reflexiva en la base de datos. Por ejemplo, puede utilizar una autocombinación para buscar pares de autores que residan en la misma ciudad.  
  
Al igual que el resto de las combinaciones, una autocombinación requiere al menos dos tablas. La diferencia reside en que, en lugar de agregar una segunda tabla a la consulta, se agrega una segunda instancia de la misma tabla. De ese modo, puede comparar una columna de la primera instancia de la tabla con la misma columna de la segunda instancia y, por tanto, comparar los valores de una columna entre sí. El [Diseñador de consultas y vistas](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) asigna un alias a la segunda instancia de la tabla.  
  
Por ejemplo, si se crea una autocombinación para buscar todos los pares de autores de Berkeley, se compara la columna `city` de la primera instancia de la tabla con la columna `city` de la segunda instancia. La consulta resultante podría tener el siguiente aspecto:  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
La creación de una autocombinación requiere a menudo varias condiciones de combinación. Para comprender el motivo de este requisito, considere el resultado de la consulta anterior:  
  
```  
Cheryl Carson       Cheryl Carson  
   Abraham Bennet      Abraham Bennet  
   Cheryl Carson       Abraham Bennet  
   Abraham Bennet      Cheryl Carson  
```  
  
La primera fila es inservible; indica que Cheryl Carson vive en la misma ciudad que Cheryl Carson. La segunda fila también es inservible. Para eliminar estos datos inútiles, agregue otra condición que conserve solo las filas de resultados en las que los dos nombres de autores correspondan a autores diferentes. La consulta resultante podría tener el siguiente aspecto:  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
               AND authors.au_id  
                <> authors1.au_id  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
El conjunto de resultados mejora:  
  
```  
Cheryl Carson       Abraham Bennet  
   Abraham Bennet      Cheryl Carson  
```  
  
Pero las dos filas de resultados son redundantes. En la primera se indica que Carson vive en la misma ciudad que Bennet y en la segunda, que Bennet vive en la misma ciudad que Carson. Para eliminar esta redundancia, puede cambiar la segunda condición de combinación de "no es igual a" a "menor que". La consulta resultante podría tener el siguiente aspecto:  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
               AND authors.au_id  
                < authors1.au_id  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
Y el conjunto de resultados tendría el siguiente aspecto:  
  
```  
Cheryl Carson       Abraham Bennet  
```  
  
### <a name="to-create-a-self-join-manually"></a>Para crear una autocombinación manualmente  
  
1.  Agregue al [panel Diagrama](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) la tabla o el objeto con valores de tabla con el que desea trabajar.  
  
2.  Vuelva a agregar la misma tabla, de forma que en el panel Diagrama muestre la misma tabla u objeto con valores de tabla dos veces.  
  
    El Diseñador de consultas y vistas asigna un alias a la segunda instancia mediante la adición de un número consecutivo al nombre de tabla. Asimismo, el Diseñador de consultas y vistas crea una línea de combinación entre las dos repeticiones de la tabla u objeto con valores de tabla en el panel Diagrama.  
  
3.  Haga clic con el botón derecho y elija **Propiedades** en el menú contextual.  
  
4.  En la ventana Propiedades, haga clic en **Condición y tipo de combinación** y después en los **puntos suspensivos (...)** situados a la derecha de la propiedad.  
  
5.  En el [cuadro de diálogo Combinar](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md) , cambie el operador de comparación entre las claves principales según corresponda. Por ejemplo, puede cambiar el operador a menor que (<).  
  
6.  Cree la otra condición de combinación (por ejemplo, authors.zip = authors1.zip) arrastrando el nombre de la columna de combinación principal de la primera aparición de la tabla u objeto con valores de tabla y colocándolo en la columna correspondiente de la segunda aparición.  
  
7.  Especifique otras opciones para la consulta, como las columnas de resultados, las condiciones de búsqueda y el criterio de ordenación.  
  
## <a name="see-also"></a>Consulte también  
[Crear autocombinaciones de forma automática (Visual Database Tools)](../../ssms/visual-db-tools/create-self-joins-automatically-visual-database-tools.md)  
[Realizar consultas con combinaciones &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
