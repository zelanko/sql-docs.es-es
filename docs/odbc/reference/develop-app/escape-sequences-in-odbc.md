---
title: Secuencias de escape en ODBC | Microsoft Docs
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
ms.openlocfilehash: 17183a7eacdc5348eea0ddcd7aee4cc493249e77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68051121"
---
# <a name="escape-sequences-in-odbc"></a>Secuencias de escape de ODBC
Una serie de características de lenguaje, como las combinaciones externas y las llamadas a funciones escalares, las implementa normalmente DBMS. Sin embargo, las sintaxis de estas características tienden a ser específicas de DBMS, incluso cuando las sintaxis estándar están definidas por los distintos cuerpos de estándares. Por ello, ODBC define secuencias de escape que contienen sintaxis estándar para las siguientes características de lenguaje:  
  
-   Literales de fecha, hora, marca de tiempo y DateTime Interval  
  
-   Funciones escalares como funciones numéricas, de cadena y de conversión de tipos de datos  
  
-   LIKE (carácter de escape de predicado)  
  
-   Combinaciones externas  
  
-   Llamadas a procedimientos  
  
 La secuencia de escape utilizada por ODBC es la siguiente:  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>Observaciones  
 Los controladores reconocen y analizan la secuencia de escape, que reemplazan las secuencias de escape por una gramática específica del DBMS. Para obtener más información sobre la sintaxis de secuencia de escape, vea [secuencias de escape ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) en el Apéndice C: gramática de SQL.  
  
> [!NOTE]  
>  En ODBC 2. *x*, esta era la sintaxis estándar de la secuencia de escape: **--\*(proveedor (**_nombre-proveedor_**),**_extensión_ __**** ** \*** producto (nombre-producto))--  
>   
>  Además de esta sintaxis, se definió una sintaxis abreviada con la forma: **{**_Extension_**}**  
>   
>  En ODBC 3. *x*, la forma larga de la secuencia de escape está en desuso y la forma abreviada se usa exclusivamente.  
  
 Dado que el controlador asigna las secuencias de escape a las sintaxis específicas de DBMS, una aplicación puede utilizar la secuencia de escape o la sintaxis específica del DBMS. Sin embargo, las aplicaciones que usan la sintaxis específica de DBMS no serán interoperables. Cuando se usa la secuencia de escape, las aplicaciones deben asegurarse de que el atributo de instrucción SQL_ATTR_NOSCAN esté desactivado, que es de forma predeterminada. De lo contrario, la secuencia de escape se enviará directamente al origen de datos, donde normalmente producirá un error de sintaxis.  
  
 Los controladores solo admiten las secuencias de escape que se pueden asignar a las características del lenguaje subyacentes. Por ejemplo, si el origen de datos no admite combinaciones externas, ninguno de ellos será el controlador. Para determinar qué secuencias de escape se admiten, una aplicación llama a **SQLGetTypeInfo** y **SQLGetInfo**. Para obtener más información, vea la sección siguiente, [fecha, hora y literales de marca de tiempo](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Fecha, hora y marca de tiempo literales](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [Llamadas a funciones escalares](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [COMO carácter de Escape de predicado](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [Combinaciones externas](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [Llamadas a procedimientos](../../../odbc/reference/develop-app/procedure-calls.md)
