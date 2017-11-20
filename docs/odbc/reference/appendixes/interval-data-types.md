---
title: Tipos de datos Interval | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- second intervals [ODBC]
- data types [ODBC], interval data types
- interval data type [ODBC]
- day-time intervals [ODBC]
- intervals [ODBC], about intervals
- minute intervals [ODBC]
- day intervals [ODBC]
- year intervals [ODBC]
- month intervals [ODBC]
- interval data type [ODBC], about interval data types
- SQL data types [ODBC], interval
- year-month intervals [ODBC]
- C data types [ODBC], interval
- interval fields [ODBC]
ms.assetid: fba93f65-c1db-44f4-91ba-532f87241cf7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f1e19ac3f7c14326524ab7cbaa60f499c5d81e91
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="interval-data-types"></a>Tipos de datos Interval
Un intervalo se define como la diferencia entre dos fechas y horas. Intervalos se expresan en uno de dos maneras diferentes. Uno es un *-mes y año* intervalo que expresa intervalos en años y un número entero de meses. El otro es un *hora diurna* intervalo que expresa intervalos en días, minutos y segundos. Estos dos tipos de intervalos son distintos y no se pueden mezclar, porque meses pueden tener un número variable de días.  
  
 Un intervalo está formada por un conjunto de campos. No hay un orden implícito entre los campos. Por ejemplo, en un intervalo de año y mes, año ocurra primero, seguido por mes. De forma similar, en un intervalo de días a minutos, los campos están en orden día, hora y minuto. El primer campo de un tipo de intervalo se denomina la *iniciales* campo, o la *orden superior* campo. Se llama el último campo del *finales* campo.  
  
 En todos los intervalos, el campo inicial no está limitado por las reglas del calendario gregoriano. Por ejemplo, en un intervalo de horas y minutos, el campo de hora no está restringido a ser entre 0 y 23 (inclusive), que normalmente es. Los campos finales después del campo inicial siguen las restricciones habituales del calendario gregoriano. Para obtener más información, consulte [restricciones del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), más adelante en este apéndice.  
  
 Hay 13 tipos de datos SQL de intervalo y 13 tipos de datos C de intervalo. Cada uno de los tipos de datos interval C utiliza la misma estructura, SQL_INTERVAL_STRUCT, para contener los datos de intervalo. (Para obtener más información, vea la sección siguiente, [estructura de intervalo de C](../../../odbc/reference/appendixes/c-interval-structure.md).) Para obtener más información sobre los tipos de datos SQL, consulte [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md); para obtener más información sobre los tipos de datos C, consulte [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md).  
  
|Identificador de tipo|Clase|Description|  
|---------------------|-----------|-----------------|  
|MONTH|Mes del año|Número de meses entre dos fechas.|  
|YEAR|Mes del año|Número de años entre dos fechas.|  
|YEAR_TO_MONTH|Mes del año|Número de años y meses entre dos fechas.|  
|DAY|Hora del día|Número de días entre dos fechas.|  
|HOUR|Hora del día|Número de horas entre dos fechas/horas.|  
|MINUTE|Hora del día|Número de minutos entre dos fechas/horas.|  
|SECOND|Hora del día|Número de segundos entre dos fechas/horas.|  
|DAY_TO_HOUR|Hora del día|Número de días/horas entre dos fechas/horas.|  
|DAY_TO_MINUTE|Hora del día|Número de días, horas o minutos entre dos fechas/horas.|  
|DAY_TO_SECOND|Hora del día|Número de días/horas/minutos/segundos entre dos fechas/horas.|  
|HOUR_TO_MINUTE|Hora del día|Número de horas o minutos entre dos fechas/horas.|  
|HOUR_TO_SECOND|Hora del día|Número de horas, minutos y segundos entre dos fechas/horas.|  
|MINUTE_TO_SECOND|Hora del día|Número de minutos/segundos entre dos fechas/horas.|  
  
 Esta sección contiene los temas siguientes.  
  
-   [Estructura de intervalo de C](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [Precisión del tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [Longitud del tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [Literales de intervalo](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [Reemplazar predeterminado inicial y la precisión de segundos para los tipos de datos Interval](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)

