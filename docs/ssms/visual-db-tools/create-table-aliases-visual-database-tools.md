---
title: Crear alias de tabla (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- table aliases [SQL Server]
- aliases [SQL Server], tables
ms.assetid: 49e61e85-8abf-4ca7-8c70-7e9f8f1078bd
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 7b505c949c0e40150f992d024bb790bf06d9724e
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67690480"
---
# <a name="create-table-aliases-visual-database-tools"></a>Crear alias de tabla (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Los alias facilitan el trabajo con nombres de tabla. El uso de alias es útil cuando:  
  
-   Desea acortar la instrucción del [panel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) y facilitar su lectura.  
  
-   La consulta hace referencia varias veces al nombre de tabla (como en el caso de los nombres completos de columnas) y quiere asegurarse de que la longitud de la consulta no superará un límite específico de caracteres. (Algunas bases de datos imponen una longitud máxima a las consultas.)  
  
-   Trabaja con varias instancias de la misma tabla (como en el caso de una autocombinación) y necesita una forma de hacer referencia a cada instancia.  
  
Por ejemplo, puede crear un alias `"e"` para un nombre de tabla `employee_information` y luego hacer referencia a la tabla como `"e"` en el resto de la consulta.  
  
### <a name="to-create-an-alias-for-a-table-or-table-valued-object"></a>Para crear un alias para una tabla o un objeto con valores de tabla  
  
1.  Agregue la tabla o el objeto con valores de tabla a la consulta.  
  
2.  En el **panel Diagrama**, haga clic con el botón derecho en el objeto para el que desea crear un alias y después elija **Propiedades** en el menú contextual.  
  
3.  En la ventana **Propiedades** , escriba el alias en el campo **Alias** .  
  
## <a name="see-also"></a>Consulte también  
[Agregar tablas a las consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Realizar operaciones básicas con consultas (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
