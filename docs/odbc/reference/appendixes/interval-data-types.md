---
title: Tipos de datos de intervalo ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee4a6e845e0bc0830f514b2e768075dd75bcf6e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304971"
---
# <a name="interval-data-types"></a>Tipo de datos de intervalo
Un intervalo se define como la diferencia entre dos fechas y horas. Los intervalos se expresan de dos maneras diferentes. Uno es un intervalo *año-mes* que expresa intervalos en términos de años y un número integral de meses. El otro es un intervalo *de tiempo y día* que expresa intervalos en términos de días, minutos y segundos. Estos dos tipos de intervalos son distintos y no se pueden mezclar, porque los meses pueden tener un número variable de días.  
  
 Un intervalo consta de un conjunto de campos. Hay un orden implícito entre los campos. Por ejemplo, en un intervalo de año a mes, el año es el primero, seguido del mes. Del mismo modo, en un intervalo de día a minuto, los campos están en el día, la hora y los minutos del pedido. El primer campo de un tipo de intervalo se denomina campo *inicial* o campo *de orden superior.* El último campo se denomina campo *final.*  
  
 En todos los intervalos, el campo inicial no está restringido por las reglas del calendario gregoriano. Por ejemplo, en un intervalo de hora a minuto, el campo de hora no está restringido a estar entre 0 y 23 (incluido), como lo es normalmente. Los campos finales posteriores al campo inicial siguen las restricciones habituales del calendario gregoriano. Para obtener más información, consulte [Restricciones del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), más adelante en este apéndice.  
  
 Hay 13 tipos de datos SQL de intervalo y 13 tipos de datos de intervalo C. Cada uno de los tipos de datos de intervalo C utiliza la misma estructura, SQL_INTERVAL_STRUCT, para contener los datos de intervalo. (Para obtener más información, consulte la siguiente sección, Estructura de [intervalo C](../../../odbc/reference/appendixes/c-interval-structure.md).) Para obtener más información sobre los tipos de datos SQL, vea [Tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md); Para obtener más información sobre los tipos de datos de C, vea [Tipos de datos de C](../../../odbc/reference/appendixes/c-data-types.md).  
  
|Identificador de tipo|Clase|Descripción|  
|---------------------|-----------|-----------------|  
|MONTH|Año-Mes|Número de meses entre dos fechas.|  
|YEAR|Año-Mes|Número de años entre dos fechas.|  
|YEAR_TO_MONTH|Año-Mes|Número de años y meses entre dos fechas.|  
|DAY|Día-Tiempo|Número de días entre dos fechas.|  
|HOUR|Día-Tiempo|Número de horas entre dos fechas/horas.|  
|MINUTE|Día-Tiempo|Número de minutos entre dos fechas/horas.|  
|SECOND|Día-Tiempo|Número de segundos entre dos fechas/horas.|  
|DAY_TO_HOUR|Día-Tiempo|Número de días/horas entre dos fechas/horas.|  
|DAY_TO_MINUTE|Día-Tiempo|Número de días/horas/minutos entre dos fechas/horas.|  
|DAY_TO_SECOND|Día-Tiempo|Número de días/horas/minutos/segundos entre dos fechas/horas.|  
|HOUR_TO_MINUTE|Día-Tiempo|Número de horas/minutos entre dos fechas/horas.|  
|HOUR_TO_SECOND|Día-Tiempo|Número de horas/minutos/segundos entre dos fechas/horas.|  
|MINUTE_TO_SECOND|Día-Tiempo|Número de minutos/segundos entre dos fechas/horas.|  
  
 Esta sección contiene los temas siguientes.  
  
-   [Estructura de intervalo de C](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [Precisión del tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [Longitud del tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [Literales de intervalo](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [Reemplazar predeterminado inicial y la precisión de segundos para los tipos de datos Interval](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
