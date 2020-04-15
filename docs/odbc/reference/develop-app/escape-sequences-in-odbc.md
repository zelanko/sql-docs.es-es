---
title: Secuencias de escape en ODBC Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d41b0c03ecbe6de63cba1a28a1f39f12a42dc86
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300425"
---
# <a name="escape-sequences-in-odbc"></a>Secuencias de escape de ODBC
Los DBMS suelen implementar varias características de lenguaje, como combinaciones externas y llamadas a funciones escalares. Sin embargo, las sintaxis de estas características tienden a ser específicas de DBMS, incluso cuando las sintaxis estándar son definidas por los distintos cuerpos de estándares. Por este motivo, ODBC define secuencias de escape que contienen sintaxis estándar para las siguientes características de lenguaje:  
  
-   Literales de fecha, hora, marca de tiempo e intervalo de fecha y hora  
  
-   Funciones escalares como funciones de conversión numérica, de cadena y de tipo de datos  
  
-   CARÁcter de escape predicado LIKE  
  
-   Combinaciones externas  
  
-   Llamadas de procedimiento  
  
 La secuencia de escape utilizada por ODBC es la siguiente:  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>Observaciones  
 La secuencia de escape es reconocida y analizada por los controladores, que reemplazan las secuencias de escape por la gramática específica de DBMS. Para obtener más información acerca de la sintaxis de secuencia de escape, vea [Secuencias](../../../odbc/reference/appendixes/odbc-escape-sequences.md) de escape ODBC en apéndice C: gramática SQL.  
  
> [!NOTE]  
>  En ODBC 2. *x*, esta era la sintaxis estándar de la secuencia de escape: **--(\*vendor(**_vendor-name_**), product(**_product-name_**)**_extension_ ** \*)--**  
>   
>  Además de esta sintaxis, se definió una sintaxis abreviada de la forma: **.**_extension_**}**  
>   
>  En ODBC 3. *x*, la forma larga de la secuencia de escape ha quedado en desuso, y la forma abreviada se utiliza exclusivamente.  
  
 Dado que el controlador asigna las secuencias de escape a sintaxis específicas de DBMS, una aplicación puede utilizar la secuencia de escape o la sintaxis específica de DBMS. Sin embargo, las aplicaciones que utilizan la sintaxis específica de DBMS no serán interoperables. Cuando se utiliza la secuencia de escape, las aplicaciones deben asegurarse de que el atributo de instrucción SQL_ATTR_NOSCAN está desactivado, que es de forma predeterminada. De lo contrario, la secuencia de escape se enviará directamente al origen de datos, donde generalmente provocará un error de sintaxis.  
  
 Los controladores solo admiten las secuencias de escape que pueden asignar a las entidades de lenguaje subyacentes. Por ejemplo, si el origen de datos no admite combinaciones externas, tampoco lo hará el controlador. Para determinar qué secuencias de escape se admiten, una aplicación llama a **SQLGetTypeInfo** y **SQLGetInfo**. Para obtener más información, consulte la siguiente sección, [Fecha, Hora y Literales](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)de marca de tiempo .  
  
 Esta sección contiene los temas siguientes.  
  
-   [Fecha, hora y marca de tiempo literales](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [Llamadas a funciones escalares](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [COMO carácter de Escape de predicado](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [Combinaciones externas](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [Llamadas a procedimientos](../../../odbc/reference/develop-app/procedure-calls.md)
