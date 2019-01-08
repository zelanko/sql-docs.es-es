---
title: 'Apéndice E: Funciones escalares | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71c80efdb2f4a87537d472ee4b6dc6bdc65af70f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540509"
---
# <a name="appendix-e-scalar-functions"></a>Apéndice E: Funciones escalares
ODBC especifica los siguientes tipos de funciones escalares, con información detallada sobre cada uno de estos tipos de función proporcionados en las secciones correspondientes de este apéndice. Las descripciones de la función incluir sintaxis asociada.  
  
 Este apéndice contiene los temas siguientes.  
  
-   [Funciones de cadena](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [Funciones numéricas](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [Funciones de hora, fecha e intervalo](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [Funciones del sistema](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [Función de conversión de tipo de datos explícito](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [Función de conversión de SQL-92](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC no impone un tipo de datos para los valores devueltos de funciones escalares, porque a menudo, las funciones son específicas del origen de datos. Las aplicaciones deben usar la función escalar de CONVERT siempre que sea posible forzar la conversión de tipos de datos.  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>Funciones escalares de ODBC y SQL-92  
 Las tablas de este apéndice incluyen funciones que se han agregado en ODBC 3.0 para alinearse con SQL-92. Las funciones de agregado para un tipo concreto de una función escalar, como se define en ODBC, se indican en cada sección.  
  
 ODBC y SQL-92 clasifican sus funciones escalares de manera diferente. ODBC clasifica las funciones escalares por tipo de argumento; SQL-92 clasifica por el valor devuelto. Por ejemplo, la función EXTRACT se clasifica como una función timedate por ODBC, porque el argumento de extracción campo es una palabra clave de fecha y hora y el argumento de origen de extracción es una expresión de intervalo o datetime. SQL-92, clasifica por otro lado, extraer como una función escalar numérica, porque el valor devuelto es un valor numérico.  
  
 Una aplicación puede determinar qué funciones escalares que admite un controlador mediante una llamada a **SQLGetInfo**. Tipos de información se incluyen tanto para ODBC para SQL-92 clasificaciones de las funciones escalares. Dado que estas clasificaciones son diferentes, se puede indicar la compatibilidad con algunas funciones escalares en tipos de información que no corresponden a ODBC y SQL-92. Por ejemplo, el tipo de información SQL_TIMEDATE_FUNCTIONS; indica la compatibilidad para la extracción de ODBC soporte técnico para las acciones EXTRACT en SQL-92, por otro lado, se indica mediante el tipo de información SQL_SQL92_NUMERIC_VALUE_FUNCTIONS.
