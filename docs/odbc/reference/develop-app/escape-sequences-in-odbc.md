---
title: Secuencias de escape en ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC]
- SQL statements [ODBC], escape sequences
- escape sequences [ODBC], about escape sequences
ms.assetid: cf229f21-6c38-4b5b-aca8-f1be0dfeb3d0
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36c0123f8b84f16b58ea1e26b77ea9f70ef0e052
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="escape-sequences-in-odbc"></a>Secuencias de escape de ODBC
Un número de características del lenguaje, como las combinaciones externas y llamadas a funciones escalares, normalmente se implementa los DBMS. Sin embargo, la sintaxis de estas características suelen ser específicos de DBMS, incluso cuando la sintaxis estándares se definen mediante los diferentes organismos de estándares. Por este motivo, ODBC define secuencias de escape que contienen sintaxis estándares para las siguientes características de lenguaje:  
  
-   Literales de intervalo de fecha, hora, marca de hora y fecha y hora  
  
-   Funciones escalares como numéricas, cadena y funciones de conversión de tipos de datos  
  
-   Al igual que el carácter de escape de predicado  
  
-   Combinaciones externas  
  
-   Llamadas a procedimientos  
  
 La secuencia de escape usada por ODBC es como sigue:  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>Comentarios  
 La secuencia de escape se reconocen y analizan los controladores, que sustituyen a las secuencias de escape con gramática específica del DBMS. Para obtener más información sobre la sintaxis de la secuencia de escape, vea [secuencias de Escape de ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) en Apéndice C: SQL gramática.  
  
> [!NOTE]  
>  En ODBC 2. *x*, era la sintaxis estándar de la secuencia de escape: **--(\*proveedor (***nombre de proveedor***), producto (***nombre de producto***) *** extensión*  **\*)--**  
>   
>  Además de esta sintaxis, sintaxis abreviada se definió el formato: **{***extensión***}**  
>   
>  En ODBC 3. *x*, la forma larga de la secuencia de escape está en desuso y la forma abreviada se utiliza exclusivamente.  
  
 Dado que las secuencias de escape se asignan por el controlador a la sintaxis específica de DBMS, una aplicación puede utilizar la secuencia de escape o la sintaxis específica del DBMS. Sin embargo, las aplicaciones que utilizan la sintaxis específica del DBMS no serán interoperables. Cuando se utiliza la secuencia de escape, las aplicaciones deben asegurarse de que el atributo de instrucción SQL_ATTR_NOSCAN está desactivado, lo que sucede de forma predeterminada. En caso contrario, la secuencia de escape se enviará directamente al origen de datos, donde generalmente provocará un error de sintaxis.  
  
 Controladores compatibles con las secuencias de escape que pueden asignar a las características de lenguaje subyacente. Por ejemplo, si el origen de datos no admite combinaciones externas, tampoco el controlador. Para determinar qué secuencias de escape son compatibles, llama a una aplicación **SQLGetTypeInfo** y **SQLGetInfo**. Para obtener más información, vea la sección siguiente, [fecha, hora y marca de tiempo literales](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Fecha, hora y marca de tiempo literales](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [Llamadas a funciones escalares](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [COMO carácter de Escape de predicado](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [Combinaciones externas](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [Llamadas a procedimientos](../../../odbc/reference/develop-app/procedure-calls.md)
