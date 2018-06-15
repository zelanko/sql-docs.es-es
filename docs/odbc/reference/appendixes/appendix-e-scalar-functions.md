---
title: 'Apéndice E: funciones escalares | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL-92 functions [ODBC]
- scalar functions [ODBC]
- functions [ODBC], scalar
ms.assetid: 59c7cd5e-32d6-43ab-bac3-7010322d105a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: acaab68fab32c25ab101f65ccd196abe7ebceef2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914490"
---
# <a name="appendix-e-scalar-functions"></a>Apéndice E: funciones escalares
ODBC especifica los siguientes tipos de funciones escalares, con información detallada sobre cada uno de estos tipos de función proporcionados en las secciones de este apéndice. Las descripciones de la función incluir sintaxis asociada.  
  
 Este apéndice contiene los temas siguientes.  
  
-   [Funciones de cadena](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [Funciones numéricas](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [Funciones de hora, fecha e intervalo](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [Funciones del sistema](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [Función de conversión de tipo de datos explícito](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [Función de conversión de SQL-92](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC no impone un tipo de datos para los valores devueltos de funciones escalares porque las funciones suelen ser específico del origen de datos. Las aplicaciones deben utilizar la función escalar CONVERT siempre que sea posible forzar la conversión de tipo de datos.  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>Funciones escalares de ODBC y SQL-92  
 Las tablas de este apéndice incluyen funciones que se han agregado en ODBC 3.0 se alineen con SQL-92. Las funciones de agregado para un determinado tipo de función escalar, como se define en ODBC, se indican en cada sección.  
  
 ODBC y SQL-92 clasifican sus funciones escalares de manera diferente. ODBC clasifica las funciones escalares por tipo de argumento; SQL-92 clasifica por valor devuelto. Por ejemplo, la función EXTRACT se clasifica como una función timedate por ODBC, porque el argumento de extracción campo es una palabra clave de fecha y hora y el argumento de origen de extracción es una expresión de fecha y hora o intervalo. SQL-92, clasifica por otro lado, extraer como una función escalar numérica, porque el valor devuelto es un valor numérico.  
  
 Una aplicación puede determinar qué funciones escalares que admite un controlador mediante una llamada a **SQLGetInfo**. Tipos de información se incluyen para ODBC y para las clasificaciones de SQL-92 de funciones escalares. Dado que estas clasificaciones son diferentes, la compatibilidad para algunas funciones escalares puede indicarse en los tipos de información que no se corresponden con ODBC y SQL-92. Por ejemplo, el tipo de información SQL_TIMEDATE_FUNCTIONS; indica la compatibilidad para la extracción de ODBC soporte técnico para la extracción en SQL-92, por otro lado, se indica mediante el tipo de información de SQL_SQL92_NUMERIC_VALUE_FUNCTIONS.
