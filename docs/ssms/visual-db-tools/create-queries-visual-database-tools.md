---
description: Crear consultas (Visual Database Tools)
title: Crear consultas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], creating
ms.assetid: 696a080d-848f-44d3-a918-e29bafaab85a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: fc2206e180c922f816337545a491af7bf8b2f461
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468417"
---
# <a name="create-queries-visual-database-tools"></a>Crear consultas (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Las consultas le permiten recuperar datos de las tablas y las vistas de su base de datos. El **Diseñador de consultas y vistas**, que permite crear y trabajar con consultas, se compone de cuatro paneles: el [panel Diagrama](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md), el [panel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md), el [panel Criterios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)y el [panel Resultados](../../ssms/visual-db-tools/results-pane-visual-database-tools.md).  
  
### <a name="to-create-a-new-query"></a>Para crear una nueva consulta  
  
1.  En el **Explorador de objetos**, expanda el nodo **Tablas** de la base de datos que desee consultar. Haga clic con el botón derecho en la tabla que desee consultar y haga clic en **Abrir tabla**.  
  
2.  Para agregar más tablas a la consulta, en el menú Diseñador de consultas, seleccione **Agregar tabla**.  
  
    > [!NOTE]  
    > Si no aparecen los paneles **Diagrama**, **SQL**, **Criterios**o **Resultados** , en el menú del Diseñador de consultas, seleccione **Panel** y haga clic en el panel que desea abrir.  
  
3.  En el cuadro de diálogo **Agregar tabla** , seleccione las tablas que desea consultar y haga clic en **Agregar** para cada una.  
  
4.  Cuando haya agregado todas las tablas que desea consultar, haga clic en **Cerrar**.  
  
    Para agregar más tablas posteriormente, haga clic con el botón derecho en el espacio abierto en el panel **Diagrama** y, en el menú contextual, haga clic en **Agregar tabla**.  
  
5.  En el panel **Diagrama**, active las casillas de los objetos con valores de tabla de cada columna que desea consultar.  
  
6.  En el menú del Diseñador de consultas, elija **Ejecutar SQL** para ejecutar la consulta.  
  
Para restringir más la consulta, puede cambiar el código SQL en el **panel SQL** o elegir opciones como el criterio de ordenación y los alias de las columnas en el panel **Criterios**.  
  
## <a name="see-also"></a>Consulte también  
[Guardar consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/save-queries-visual-database-tools.md)  
[Tipos de consultas (Visual Database Tools)](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
[Especificar criterios de búsqueda (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Realizar operaciones básicas con consultas (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
