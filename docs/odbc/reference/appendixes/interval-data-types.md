---
title: Tipos de datos de intervalo | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304971"
---
# <a name="interval-data-types"></a>Tipo de datos de intervalo
Un intervalo se define como la diferencia entre dos fechas y horas. Los intervalos se expresan de una de estas dos maneras diferentes. Uno es un intervalo del *año* que expresa los intervalos en términos de años y un número entero de meses. El otro es un intervalo de *tiempo* que expresa los intervalos en términos de días, minutos y segundos. Estos dos tipos de intervalos son distintos y no se pueden mezclar, porque los meses pueden tener un número variable de días.  
  
 Un intervalo consta de un conjunto de campos. Hay una ordenación implícita entre los campos. Por ejemplo, en un intervalo de un año a otro, el año viene primero, seguido del mes. Del mismo modo, en un intervalo de un día a otro, los campos se encuentran en el orden día, hora y minuto. El primer campo de un tipo de intervalo se denomina campo *inicial* o el campo de *orden superior* . El último campo se denomina campo *final* .  
  
 En todos los intervalos, el campo inicial no está restringido por las reglas del calendario gregoriano. Por ejemplo, en un intervalo de hora a minuto, el campo de hora no está restringido entre 0 y 23 (incluido), como suele ser. Los campos finales posteriores al campo inicial siguen las restricciones habituales del calendario gregoriano. Para obtener más información, vea [restricciones del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), más adelante en este apéndice.  
  
 Hay 13 tipos de datos SQL de intervalo y 13 tipos de datos de intervalo C. Cada uno de los tipos de datos de intervalo C utiliza la misma estructura, SQL_INTERVAL_STRUCT, para contener los datos de intervalo. (Para obtener más información, vea la sección siguiente, [estructura de intervalo de C](../../../odbc/reference/appendixes/c-interval-structure.md)). Para obtener más información sobre los tipos de datos de SQL, vea [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md); para obtener más información sobre los tipos de datos de C, vea [tipos de datos de c](../../../odbc/reference/appendixes/c-data-types.md).  
  
|Identificador de tipo|Clase|Descripción|  
|---------------------|-----------|-----------------|  
|MONTH|Año-mes|Número de meses entre dos fechas.|  
|YEAR|Año-mes|Número de años entre dos fechas.|  
|YEAR_TO_MONTH|Año-mes|Número de años y meses entre dos fechas.|  
|DAY|Fecha y hora|Número de días entre dos fechas.|  
|HOUR|Fecha y hora|Número de horas entre dos fechas/horas.|  
|MINUTE|Fecha y hora|Número de minutos entre dos fechas/horas.|  
|SECOND|Fecha y hora|Número de segundos entre dos fechas/horas.|  
|DAY_TO_HOUR|Fecha y hora|Número de días/horas entre dos fechas y horas.|  
|DAY_TO_MINUTE|Fecha y hora|Número de días/horas/minutos entre dos fechas y horas.|  
|DAY_TO_SECOND|Fecha y hora|Número de días/horas/minutos/segundos entre dos fechas/horas.|  
|HOUR_TO_MINUTE|Fecha y hora|Número de horas/minutos entre dos fechas/horas.|  
|HOUR_TO_SECOND|Fecha y hora|Número de horas/minutos/segundos entre dos fechas/horas.|  
|MINUTE_TO_SECOND|Fecha y hora|Número de minutos/segundos entre dos fechas/horas.|  
  
 Esta sección contiene los temas siguientes.  
  
-   [Estructura de intervalo de C](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [Precisión del tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [Longitud del tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [Literales de intervalo](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [Reemplazar predeterminado inicial y la precisión de segundos para los tipos de datos Interval](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
