---
title: Excluir filas duplicadas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- row duplicates [SQL Server]
- duplicate rows
- row excluded in search [SQL Server]
- result sets [SQL Server], duplicate values
- excluding rows
ms.assetid: ab35a363-421d-4665-946b-ae3f6397af50
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 2f652c40278a44d4bbe068a441e08ffe610af002
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012159"
---
# <a name="exclude-duplicate-rows-visual-database-tools"></a>Excluir filas duplicadas (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Si solo desea ver los valores únicos de un conjunto de resultados, puede indicar que se excluyan los duplicados del conjunto de resultados.  
  
### <a name="to-exclude-duplicate-rows-from-the-result-set"></a>Para excluir filas duplicadas del conjunto de resultados  
  
1.  Haga clic con el botón derecho en el fondo del panel Diagrama y, luego, elija **Propiedades** en el menú contextual.  
  
2.  En la ventana Propiedades, haga clic en **Valores DISTINCT** y establezca el valor en **Sí**.  
  
    El Diseñador de consultas y vistas inserta la palabra clave DISTINCT delante de la lista de columnas mostradas en la instrucción SQL.  
  
    > [!NOTE]  
    > Si utiliza la palabra clave DISTINCT , es posible que no pueda modificar el conjunto de resultados en el panel de resultados.  
  
## <a name="see-also"></a>Consulte también  
[Especificar criterios de búsqueda (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
