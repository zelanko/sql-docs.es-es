---
title: Secuencias de escape de ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC]
- SQL statements [ODBC], escape sequences
- escape sequences [ODBC], about escape sequences
ms.assetid: cf229f21-6c38-4b5b-aca8-f1be0dfeb3d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33259a56faa19dda2403996b6d6d8930ec2a87be
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706003"
---
# <a name="escape-sequences-in-odbc"></a>Secuencias de escape de ODBC
Un número de características del lenguaje, como las combinaciones externas y llamadas a funciones escalares, normalmente se implementa los DBMS. Sin embargo, la sintaxis para estas características suelen ser específicos para DBMS, incluso cuando la sintaxis estándares se definen mediante los diversos organismos de estándares. Por este motivo, ODBC define secuencias de escape que contienen sintaxis estándares para las siguientes características de lenguaje:  
  
-   Literales de intervalo de fecha, hora, marca de hora y fecha y hora  
  
-   Funciones escalares como numérica, cadena y funciones de conversión de tipos de datos  
  
-   Al igual que el carácter de escape de predicado  
  
-   Combinaciones externas  
  
-   Llamadas a procedimientos  
  
 La secuencia de escape que utiliza ODBC es como sigue:  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>Comentarios  
 La secuencia de escape se reconocen y se analizan los controladores, que sustituyen a las secuencias de escape con gramática específicos para DBMS. Para obtener más información sobre la sintaxis de la secuencia de escape, consulte [secuencias de Escape ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) en Apéndice C: SQL gramática.  
  
> [!NOTE]  
>  En ODBC 2. *x*, esto fue la sintaxis estándar de la secuencia de escape: **--(\*proveedor (***nombre de proveedor***), producto (***nombre de producto***) *** extensión*  **\*)--**  
>   
>  Además de esta sintaxis, se definió una sintaxis abreviada del formulario: **{***extensión***}**  
>   
>  En ODBC 3. *x*, el formato largo de la secuencia de escape en desuso y la forma abreviada se utiliza exclusivamente.  
  
 Dado que las secuencias de escape se asignan por el controlador para sintaxis específicos para DBMS, una aplicación puede usar la secuencia de escape o sintaxis específicos para DBMS. Sin embargo, las aplicaciones que utilizan la sintaxis específica del DBMS no será interoperables. Cuando se usa la secuencia de escape, las aplicaciones deben asegurarse de que el atributo de instrucción SQL_ATTR_NOSCAN está desactivado, lo que sucede de forma predeterminada. En caso contrario, la secuencia de escape se enviarán directamente al origen de datos, donde generalmente provocará un error de sintaxis.  
  
 Controladores son compatibles con solo esas secuencias de escape que pueden asignar a las características de lenguaje subyacente. Por ejemplo, si el origen de datos no admite combinaciones externas, tampoco el controlador. Para determinar qué secuencias de escape son compatibles, una aplicación llama a **SQLGetTypeInfo** y **SQLGetInfo**. Para obtener más información, consulte la sección siguiente, [fecha, hora y marca de tiempo literales](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Fecha, hora y marca de tiempo literales](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [Llamadas a funciones escalares](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [COMO carácter de Escape de predicado](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [Combinaciones externas](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [Llamadas a procedimientos](../../../odbc/reference/develop-app/procedure-calls.md)
