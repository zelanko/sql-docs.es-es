---
title: Resumir o agregar valores mediante expresiones personalizadas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- summarizing query results
- custom expressions to aggregate values [SQL Server]
ms.assetid: 34130ac1-0106-4766-b324-acb0b7bb6f6e
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: acf28bbddb69d7dfe2888ad53465143103c90dba
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75254864"
---
# <a name="summarize-or-aggregate-values-using-custom-expressions-visual-database-tools"></a>Resumir o agregar valores mediante expresiones personalizadas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Además de utilizar las funciones de agregado para agregar datos, puede crear expresiones personalizadas para generar valores de agregado. Estas expresiones se pueden utilizar en lugar de las funciones de agregado en cualquier lugar de una consulta de funciones agregadas.  
  
Por ejemplo, en la tabla `titles` podría crear una consulta que mostrara no solo el precio medio, sino el precio medio resultante si se aplicara un descuento.  
  
No se pueden incluir expresiones basadas en cálculos en los que solo se utilicen filas individuales de la tabla; las expresiones deben basarse en valores agregados, ya que solo estos valores están disponibles cuando se calcula la expresión.  
  
### <a name="to-specify-a-custom-expression-for-a-summary-value"></a>Para especificar una expresión personalizada para un valor de resumen  
  
1.  Especifique los grupos de la consulta. Para detalles, consulte [Agrupar filas en los resultados de la consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md).  
  
2.  Desplácese a una fila vacía del panel Criterios y escriba la expresión en la columna **Columnas**.  
  
    El [Diseñador de consultas y vistas](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) asigna automáticamente un alias de columna a la expresión para crear un encabezado de columna útil en los resultados de la consulta. Para más información, consulte [Crear alias de columna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
3.  En la columna **Agrupar por** de la expresión, seleccione **Expresión**.  
  
4.  Ejecuta la consulta.  
  
## <a name="see-also"></a>Consulte también  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  
