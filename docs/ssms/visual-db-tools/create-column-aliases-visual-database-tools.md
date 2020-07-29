---
title: Crear alias de columna
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], aliases
- aliases [SQL Server], columns
ms.assetid: e2e1c166-8ea7-47a2-b6a7-e419bf0fa3bb
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: c4feb18b5f01b1e999ecec5b5b8e022230912d8f
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "85977998"
---
# <a name="create-column-aliases-visual-database-tools"></a>Crear alias de columna (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Puede crear alias para nombres de columnas con el fin de facilitar el trabajo con nombres de columnas, cálculos y valores de resumen. Por ejemplo, puede crear un alias de columna para:  
  
-   Crear un nombre de columna, como "Importe total", para una expresión como `(quantity * unit_price)` o para una función de agregado.  
  
-   Crear un nombre abreviado de un nombre de columna, como `"d_id"` para `"discounts.stor_id."`  
  
Cuando haya definido un alias de columna, podrá utilizarlo en una consulta Select para especificar los resultados de la consulta.  
  
### <a name="to-create-a-column-alias"></a>Para crear un alias de columna  
  
1.  En el panel **Criterios**, busque la fila que contiene la columna de datos para la que desea crear un alias y, si es necesario, márquela como columna de resultados. Si la columna de datos no está en la cuadrícula, agréguela.  
  
2.  Escriba el alias en la columna **Alias** de la fila. El alias debe cumplir todas las convenciones de nomenclatura de SQL. Si el nombre de alias escrito contiene espacios, el Diseñador de consultas y vistas colocará automáticamente delimitadores en torno al mismo.  
  
## <a name="see-also"></a>Consulte también  
[Agregar columnas a las consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md)  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Realizar operaciones básicas con consultas (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
