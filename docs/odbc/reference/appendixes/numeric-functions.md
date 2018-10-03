---
title: Funciones numéricas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], numeric functions
- numeric functions [ODBC]
ms.assetid: 4fa548dc-e8b0-4179-92ff-81d6a79d10c3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca33d451fe5e1431d9bc4fb29196b98adcfb933f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620373"
---
# <a name="numeric-functions"></a>Funciones numéricas
En la tabla siguiente se describe las funciones numéricas que se incluyen en el conjunto de funciones escalares de ODBC. Mediante una llamada a **SQLGetInfo** con un *tipo de información* de SQL_NUMERIC_FUNCTIONS, una aplicación puede determinar qué funciones numéricas son compatibles con un controlador.  
  
 Todas las funciones numéricas los valores devuelven de tipo de datos SQL_FLOAT excepto ABS, ROUND, TRUNCATE, inicio de sesión, FLOOR y CEILING, que devuelven valores de los mismos datos que se escriba como los parámetros de entrada.  
  
 Argumentos que se indican como *numeric_exp* puede ser el nombre de una columna, el resultado de otra función escalar, o un *numérico litera*l, donde el tipo de datos subyacente podría representarse como SQL_NUMERIC, SQL_ DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL o SQL_DOUBLE.  
  
 Argumentos que se indican como *float_exp* puede ser el nombre de una columna, el resultado de otra función escalar, o un *literales numéricos*, donde el tipo de datos subyacente se puede representar como SQL_FLOAT.  
  
 Argumentos que se indican como *integer_exp* puede ser el nombre de una columna, el resultado de otra función escalar, o un *literales numéricos*, donde el tipo de datos subyacente se puede representar como SQL_TINYINT, SQL_ SMALLINT, SQL_INTEGER o SQL_BIGINT.  
  
 Se agregaron las funciones escalares CURRENT_TIMESTAMP, CURRENT_TIME y CURRENT_DATE ODBC 3.0 para alinearse con SQL-92.  
  
|Función|Descripción|  
|--------------|-----------------|  
|**ABS (** *numeric_exp* **)** (ODBC 1.0)|Devuelve el valor absoluto de *numeric_exp*.|  
|**ACOS (** *float_exp* **)** (ODBC 1.0)|Devuelve el arcocoseno de *float_exp* como un ángulo, expresado en radianes.|  
|**ASIN (** *float_exp* **)** (ODBC 1.0)|Devuelve el arcoseno de *float_exp* como un ángulo, expresado en radianes.|  
|**ATAN (** *float_exp* **)** (ODBC 1.0)|Devuelve el arco tangente de *float_exp* como un ángulo, expresado en radianes.|  
|**ATAN2 (** *float_exp1*, *float_exp2 ***)** (ODBC 2.0)|Devuelve el arco tangente de la *x* y *y* coordenadas, especificadas por *float_exp1* y *float_exp2*, respectivamente, como un ángulo, expresado en radianes.|  
|**CEILING (** *numeric_exp* **)** (ODBC 1.0)|Devuelve el entero más pequeño mayor o igual a *numeric_exp*. El valor devuelto es del mismo tipo de datos como parámetro de entrada.|  
|**COS (** *float_exp* **)** (ODBC 1.0)|Devuelve el coseno de *float_exp*, donde *float_exp* es el ángulo, expresado en radianes.|  
|**COT (** *float_exp* **)** (ODBC 1.0)|Devuelve la cotangente de *float_exp*, donde *float_exp* es el ángulo, expresado en radianes.|  
|**GRADOS (** *numeric_exp* **)** (ODBC 2.0)|Devuelve el número de grados convertido a partir de *numeric_exp* radianes.|  
|**EXP (** *float_exp* **)** (ODBC 1.0)|Devuelve el valor exponencial de *float_exp*.|  
|**FLOOR (** *numeric_exp* **)** (ODBC 1.0)|Devuelve el entero más grande menor o igual a *numeric_exp*. El valor devuelto es del mismo tipo de datos como parámetro de entrada.|  
|**REGISTRO (** *float_exp* **)** (ODBC 1.0)|Devuelve el logaritmo natural de *float_exp*.|  
|**LOG10 (** *float_exp* **)** (ODBC 2.0)|Devuelve la base 10 logaritmo de *float_exp*.|  
|**MOD (** *integer_exp1*, *integer_exp2 ***)** (ODBC 1.0)|Devuelve el resto (módulo) de *integer_exp1* dividido por *integer_exp2*.|  
|**PI ()** (ODBC 1.0)|Devuelve el valor constante de pi como un valor de punto flotante.|  
|**POWER (** *numeric_exp*, *integer_exp ***)** (ODBC 2.0)|Devuelve el valor de *numeric_exp* a la potencia de *integer_exp*.|  
|**RADIANS (** *numeric_exp* **)** (ODBC 2.0)|Devuelve el número de radianes convertido a partir de *numeric_exp* grados.|  
|**RAND (**[*integer_exp*]**)** (ODBC 1.0)|Devuelve un valor de punto flotante aleatorio con *integer_exp* como el valor de inicialización opcional.|  
|**ROUND (** *numeric_exp*, *integer_exp ***)** (ODBC 2.0)|Devuelve *numeric_exp* redondeado a *integer_exp* coloca a la derecha del separador decimal. Si *integer_exp* es negativo, *numeric_exp* se redondea a &#124; *integer_exp* &#124; coloca a la izquierda del separador decimal.|  
|**Inicio de sesión (** *numeric_exp* **)** (ODBC 1.0)|Devuelve un indicador de la sesión de *numeric_exp*. Si *numeric_exp* es menor que cero, – 1 se devuelve. Si *numeric_exp* es igual a cero, se devuelve 0. Si *numeric_exp* es mayor que cero, se devuelve 1.|  
|**SENO (** *float_exp* **)** (ODBC 1.0)|Devuelve el seno de *float_exp*, donde *float_exp* es el ángulo, expresado en radianes.|  
|**SQRT (** *float_exp* **)** (ODBC 1.0)|Devuelve la raíz cuadrada de *float_exp*.|  
|**TAN (** *float_exp* **)** (ODBC 1.0)|Devuelve la tangente de *float_exp*, donde *float_exp* es el ángulo, expresado en radianes.|  
|**TRUNCATE (** *numeric_exp*, *integer_exp ***)** (ODBC 2.0)|Devuelve *numeric_exp* truncado a *integer_exp* coloca a la derecha del separador decimal. Si *integer_exp* es negativo, *numeric_exp* se trunca a &#124; *integer_exp* &#124; coloca a la izquierda del separador decimal.|
