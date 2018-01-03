---
title: Resumir los resultados de una consulta (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- summarizing query results
- queries [SQL Server], results
- aggregate queries [SQL Server]
ms.assetid: c9e15350-ed57-4d95-814d-815fbebfd86b
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 23be6f5ada4c862e4f55d71d3023a8e0c56fdb7a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="summarize-query-results-visual-database-tools"></a>Resumir los resultados de una consulta (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Al crear consultas de funciones agregadas, se aplican determinados principios lógicos. Por ejemplo, no puede mostrar el contenido de filas individuales en una consulta de resumen. El Diseñador de consultas y vistas le ayuda a cumplir estos principios ajustándose al comportamiento del [panel Diagrama](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) y el [panel Criterios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md) .  
  
Si comprende los principios de las consultas de funciones agregadas y el comportamiento del Diseñador de consultas y vistas, podrá crear consultas de agregado correctas en cuanto a la lógica. El principio predominante es que las consultas de agregado solo pueden producir información de resumen. Por tanto, la mayoría de los principios que siguen describen las formas de hacer referencia a las columnas de datos individuales dentro de una consulta de agregado.  
  
## <a name="in-this-section"></a>En esta sección  
[Trabajar con columnas en consultas de funciones agregadas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-columns-in-aggregate-queries-visual-database-tools.md)  
Describe los conceptos de la agrupación y el resumen de columnas con las cláusulas GROUP BY, WHERE y HAVING.  
  
[Contar las filas de una tabla &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/count-rows-in-a-table-visual-database-tools.md)  
Proporciona los pasos para contar el número de filas de una tabla o el número de filas de una tabla que cumpla un conjunto de criterios.  
  
[Resumir o agregar los valores de todas las filas de una tabla &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools.md)  
Proporciona los pasos para resumir todas las filas en lugar de un conjunto de filas agrupadas.  
  
[Resumir o agregar valores mediante expresiones personalizadas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-or-aggregate-values-using-custom-expressions-visual-database-tools.md)  
Proporciona los pasos para utilizar expresiones para resumir o agregar en lugar de utilizar las cláusulas predefinidas.  
  
## <a name="related-sections"></a>Secciones relacionadas  
[Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
Proporciona vínculos a temas en los que se explica cómo se utiliza el Diseñador de consultas y vistas.  
  
