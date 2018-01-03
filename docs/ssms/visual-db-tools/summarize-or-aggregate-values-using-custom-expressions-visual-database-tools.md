---
title: Resumir o agregar valores mediante expresiones personalizadas | Microsoft Docs
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
- custom expressions to aggregate values [SQL Server]
ms.assetid: 34130ac1-0106-4766-b324-acb0b7bb6f6e
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c34ad32139e6baabb94009858809043915773be
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="summarize-or-aggregate-values-using-custom-expressions-visual-database-tools"></a>Resumir o agregar valores mediante expresiones personalizadas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Además de usar funciones de agregado para agregar datos, puede crear expresiones personalizadas para generar valores de agregado. Estas expresiones se pueden utilizar en lugar de las funciones de agregado en cualquier lugar de una consulta de funciones agregadas.  
  
Por ejemplo, en la tabla `titles` podría crear una consulta que mostrara no solo el precio medio, sino el precio medio resultante si se aplicara un descuento.  
  
No se pueden incluir expresiones basadas en cálculos en los que solo se utilicen filas individuales de la tabla; las expresiones deben basarse en valores agregados, ya que solo estos valores están disponibles cuando se calcula la expresión.  
  
### <a name="to-specify-a-custom-expression-for-a-summary-value"></a>Para especificar una expresión personalizada para un valor de resumen  
  
1.  Especifique los grupos de la consulta. Para detalles, consulte [Agrupar filas en los resultados de la consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md).  
  
2.  Desplácese a una fila vacía del panel Criterios y escriba la expresión en la columna **Columnas**.  
  
    El [Diseñador de consultas y vistas](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) asigna automáticamente un alias de columna a la expresión para crear un encabezado de columna útil en los resultados de la consulta. Para más información, consulte [Crear alias de columna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
3.  En la columna **Agrupar por** de la expresión, seleccione **Expresión**.  
  
4.  Ejecuta la consulta.  
  
## <a name="see-also"></a>Ver también  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  
