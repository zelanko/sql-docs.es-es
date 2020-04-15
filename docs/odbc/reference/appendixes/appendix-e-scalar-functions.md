---
title: 'Apéndice E: Funciones escalares ? Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL-92 functions [ODBC]
- scalar functions [ODBC]
- functions [ODBC], scalar
ms.assetid: 59c7cd5e-32d6-43ab-bac3-7010322d105a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea354a7f882bd1a75c5f16fb19350d69ca11d375
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292495"
---
# <a name="appendix-e-scalar-functions"></a>Apéndice E: Funciones escalares
ODBC especifica los siguientes tipos de funciones escalares, con información detallada sobre cada uno de estos tipos de función proporcionados en las secciones correspondientes de este apéndice. Las descripciones de la función incluyen la sintaxis asociada.  
  
 Este apéndice contiene los siguientes temas.  
  
-   [Funciones de cadena](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [Funciones numéricas](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [Funciones de hora, fecha e intervalo](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [Funciones del sistema](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [Función de conversión de tipo de datos explícito](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [Función CAST de SQL-92](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC no exige un tipo de datos para los valores devueltos de funciones escalares porque las funciones son a menudo específicas del origen de datos. Las aplicaciones deben utilizar la función escalar CONVERT siempre que sea posible para forzar la conversión de tipos de datos.  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>Funciones escalares ODBC y SQL-92  
 Las tablas de este apéndice incluyen funciones que se han agregado en ODBC 3.0 para alinearse con SQL-92. Esas funciones agregadas para un tipo determinado de función escalar, tal como se define en ODBC, se indican en cada sección.  
  
 ODBC y SQL-92 clasifican sus funciones escalares de forma diferente. ODBC clasifica las funciones escalares por tipo de argumento; SQL-92 los clasifica por valor devuelto. Por ejemplo, ODBC clasifica la función EXTRACT como una función de fecha de tiempo, porque el argumento extract-field es una palabra clave datetime y el argumento extract-source es una expresión datetime o interval. SQL-92, por otro lado, clasifica EXTRACT como una función escalar numérica, porque el valor devuelto es numérico.  
  
 Una aplicación puede determinar qué funciones escalares admite un controlador llamando a **SQLGetInfo**. Los tipos de información se incluyen tanto para ODBC como para las clasificaciones SQL-92 de funciones escalares. Dado que estas clasificaciones son diferentes, la compatibilidad con algunas funciones escalares puede indicarse en tipos de información que no corresponden a ODBC y SQL-92. Por ejemplo, la compatibilidad con EXTRACT en ODBC se indica mediante el tipo de información SQL_TIMEDATE_FUNCTIONS; La compatibilidad con EXTRACT en SQL-92, por otro lado, se indica mediante el tipo de información SQL_SQL92_NUMERIC_VALUE_FUNCTIONS.
