---
description: Ordenar filas (Visual Database Tools)
title: Ordenar filas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- sorting rows [SQL Server]
- sorting query results [SQL Server]
ms.assetid: 780ef467-f96e-4373-8235-6dacbedb05a2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 2cc6ae5da87b1ef1f70c7b66fe3f06d8e6b2ed90
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491591"
---
# <a name="sort-rows-visual-database-tools"></a>Ordenar filas (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Puede ordenar las filas de un resultado de consulta. Es decir, puede indicar una columna o un conjunto de columnas determinado cuyos valores determinen el orden de las filas en el conjunto de resultados.  
  
> [!NOTE]  
> La secuencia de intercalación de la columna determina en parte el criterio de ordenación. La secuencia de intercalación se puede modificar en el [cuadro de diálogo Intercalación](../../ssms/visual-db-tools/collation-dialog-box-visual-database-tools.md).  
  
Los resultados de la consulta se pueden ordenar de varias maneras:  
  
-   **Puede organizar filas en orden ascendente o descendente** De forma predeterminada, SQL utiliza el orden por columnas para organizar las filas en orden ascendente. Por ejemplo, para organizar los títulos de libros por precio ascendente, solo tiene que ordenar las filas por la columna price. El código SQL resultante puede presentar el siguiente aspecto:  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price  
    ```  
  
    Por otro lado, si desea organizar los títulos con los libros más caros primero, puede especificar explícitamente un orden en el que se indiquen primero los valores más altos. Es decir, puede indicar que las filas del resultado se ordenen por valores descendentes de la columna price. El código SQL resultante puede presentar el siguiente aspecto:  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price DESC  
    ```  
  
-   **Puede ordenar por varias columnas** Por ejemplo, puede crear un conjunto de resultados con una fila para cada autor, que se ordene primero por estado y, a continuación, por ciudad. El código SQL resultante puede presentar el siguiente aspecto:  
  
    ```  
    SELECT *  
    FROM authors   
    ORDER BY state, city  
    ```  
  
-   **Puede ordenar por columnas que no aparezcan en el conjunto de resultados** Por ejemplo, puede crear un conjunto de resultados con los títulos más caros primero, aunque no aparezcan los precios. El código SQL resultante puede presentar el siguiente aspecto:  
  
    ```  
    SELECT title_id, title  
    FROM titles  
    ORDER BY price DESC  
    ```  
  
-   **Puede ordenar por columnas derivadas** Por ejemplo, puede crear un conjunto de resultados en el que cada fila contenga un título de libro y en el que aparezcan primero los libros que pagan las regalías (royalties) más elevadas por copia. El código SQL resultante puede presentar el siguiente aspecto:  
  
    ```  
    SELECT title, price * royalty / 100 as royalty_per_unit  
    FROM titles  
    ORDER BY royalty_per_unit DESC  
    ```  
  
    (La fórmula para calcular las regalías que cada libro genera por copia está resaltada).  
  
    Para calcular una columna derivada, puede utilizar la sintaxis SQL, como en el ejemplo anterior, o puede utilizar una función definida por el usuario que devuelva un valor escalar. Para obtener más información sobre las funciones definidas por el usuario, vea la documentación de SQL Server.  
  
-   **Puede ordenar filas agrupadas** Por ejemplo, puede crear un conjunto de resultados en el que cada fila describa una ciudad, además del número de autores de esa ciudad, y en el que aparezcan primero las ciudades que contienen muchos autores. El código SQL resultante puede presentar el siguiente aspecto:  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    ORDER BY COUNT(*) DESC, state  
    ```  
  
    Tenga en cuenta que la consulta utiliza `state` como columna de orden secundaria. De este modo, si dos estados tienen el mismo número de autores, esos estados aparecerán en orden alfabético.  
  
-   **Puede ordenar mediante el uso de datos internacionales** Es decir, puede ordenar una columna mediante el uso de convenciones de intercalación diferentes de las convenciones predeterminadas para esa columna. Por ejemplo, puede escribir una consulta que recupere todo los libros de Jaime Patiño. Para que los títulos aparezcan ordenados alfabéticamente, utilice una secuencia de intercalación de español en la columna de los títulos. El código SQL resultante puede presentar el siguiente aspecto:  
  
    ```  
    SELECT title  
    FROM   
        authors   
        INNER JOIN   
            titleauthor   
            ON authors.au_id   
            =  titleauthor.au_id   
            INNER JOIN  
                titles   
                ON titleauthor.title_id   
                =  titles.title_id   
    WHERE   
         au_fname = 'Jaime' AND   
         au_lname = 'Patiño'  
    ORDER BY   
         title COLLATE SQL_Spanish_Pref_CP1_CI_AS  
    ```  
  
## <a name="see-also"></a>Consulte también  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
