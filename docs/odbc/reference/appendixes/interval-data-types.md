---
title: Tipos de datos Interval | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 930a848ea01d128cb248c7929408ce7510937ad9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188900"
---
# <a name="interval-data-types"></a>Tipo de datos de intervalo
Un intervalo se define como la diferencia entre dos fechas y horas. Intervalos se expresan en uno de dos maneras diferentes. Uno es un *año mes* intervalo que expresa los intervalos en años y un número entero de meses. El otro es un *día y hora* intervalo que expresa los intervalos en días, minutos y segundos. Estos dos tipos de intervalos son distintos y no se pueden mezclar, porque meses pueden tener un número variable de días.  
  
 Un intervalo consta de un conjunto de campos. No hay un orden implícito entre los campos. Por ejemplo, en un intervalo de año y mes, el año aparece primero, seguido por mes. De forma similar, en un intervalo de días a minutos, los campos están en el orden día, hora y minuto. El primer campo de un tipo de intervalo se denomina el *iniciales* campo, o la *orden superior* campo. El último campo se denomina el *finales* campo.  
  
 En todos los intervalos, el campo inicial no está restringido por las reglas del calendario gregoriano. Por ejemplo, en un intervalo de horas y minutos, el campo de hora no está limitado a estar entre 0 y 23 (inclusive), ya que es normalmente. Los campos finales tras el campo inicial siguen las restricciones habituales del calendario gregoriano. Para obtener más información, consulte [restricciones del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), más adelante en este apéndice.  
  
 Hay 13 tipos de datos SQL de intervalo y 13 tipos de datos C de intervalo. Cada uno de los tipos de datos de intervalo C utiliza la misma estructura, SQL_INTERVAL_STRUCT, para contener el intervalo de datos. (Para obtener más información, consulte la sección siguiente, [estructura de intervalo de C](../../../odbc/reference/appendixes/c-interval-structure.md).) Para obtener más información sobre los tipos de datos SQL, consulte [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md); para obtener más información sobre los tipos de datos de C, vea [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md).  
  
|Identificador de tipo|Clase|Descripción|  
|---------------------|-----------|-----------------|  
|MONTH|Mes del año|Número de meses entre dos fechas.|  
|YEAR|Mes del año|Número de años entre dos fechas.|  
|YEAR_TO_MONTH|Mes del año|Número de años y meses entre dos fechas.|  
|DAY|Hora del día|Número de días entre dos fechas.|  
|HOUR|Hora del día|Número de horas entre dos fechas/horas.|  
|MINUTE|Hora del día|Número de minutos entre dos fechas/horas.|  
|SECOND|Hora del día|Número de segundos entre dos fechas/horas.|  
|DAY_TO_HOUR|Hora del día|Número de días y horas entre dos fechas/horas.|  
|DAY_TO_MINUTE|Hora del día|Número de días, horas o minutos entre dos fechas/horas.|  
|DAY_TO_SECOND|Hora del día|Número de días/horas/minutos/segundos entre dos fechas/horas.|  
|HOUR_TO_MINUTE|Hora del día|Número de horas o minutos entre dos fechas/horas.|  
|HOUR_TO_SECOND|Hora del día|Número de horas/minutos/segundos entre dos fechas/horas.|  
|MINUTE_TO_SECOND|Hora del día|Número de minutos/segundos entre dos fechas/horas.|  
  
 Esta sección contiene los temas siguientes.  
  
-   [Estructura de intervalo de C](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [Precisión del tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [Longitud del tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [Literales de intervalo](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [Reemplazar predeterminado inicial y la precisión de segundos para los tipos de datos Interval](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
