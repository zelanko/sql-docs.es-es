---
title: Funciones numéricas ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 03da5b6644e0f7df3dc4e5e16a211cb503023bad
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299875"
---
# <a name="numeric-functions"></a>Funciones numéricas
En la tabla siguiente se describen las funciones numéricas que se incluyen en el conjunto de funciones escalares ODBC. Al llamar a **SQLGetInfo** con un tipo de *información* de SQL_NUMERIC_FUNCTIONS, una aplicación puede determinar qué funciones numéricas son compatibles con un controlador.  
  
 Todas las funciones numéricas devuelven valores de tipo de datos SQL_FLOAT excepto ABS, ROUND, TRUNCATE, SIGN, FLOOR y CEILING, que devuelven valores del mismo tipo de datos que los parámetros de entrada.  
  
 Los argumentos que se indican como *numeric_exp* pueden ser el nombre de una columna, el resultado de otra función escalar o una *literall,* donde el tipo de datos subyacente se puede representar como SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL o SQL_DOUBLE.  
  
 Los argumentos que se indican como *float_exp* pueden ser el nombre de una columna, el resultado de otra función escalar o un *literal numérico,* donde el tipo de datos subyacente se puede representar como SQL_FLOAT.  
  
 Los argumentos que se indican como *integer_exp* pueden ser el nombre de una columna, el resultado de otra función escalar o un *literal numérico,* donde el tipo de datos subyacente se puede representar como SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER o SQL_BIGINT.  
  
 Las funciones escalares CURRENT_DATE, CURRENT_TIME y CURRENT_TIMESTAMP se han agregado en ODBC 3.0 para alinearse con SQL-92.  
  
|Función|Descripción|  
|--------------|-----------------|  
|**ABS(** _numeric_exp_ **)** (ODBC 1.0)|Devuelve el valor absoluto de *numeric_exp*.|  
|**ACOS(** _float_exp_ **)** (ODBC 1.0)|Devuelve la arccosina de *float_exp* como un ángulo, expresado en radianes.|  
|**ASIN(** _float_exp_ **)** (ODBC 1.0)|Devuelve el arcoseno de *float_exp* como un ángulo, expresado en radianes.|  
|**ATAN(** _float_exp_ **)** (ODBC 1.0)|Devuelve el arco tangente de *float_exp* como un ángulo, expresado en radianes.|  
|**ATAN2(** _float_exp1_, _float_exp2_**)** (ODBC 2.0)|Devuelve el arco tangente de las coordenadas *x* e *y,* especificado por *float_exp1* y *float_exp2*, respectivamente, como un ángulo, expresado en radianes.|  
|**CEILING(** _numeric_exp_ **)** (ODBC 1.0)|Devuelve el entero más pequeño mayor o igual que *numeric_exp*. El valor devuelto es del mismo tipo de datos que el parámetro de entrada.|  
|**COS(** _float_exp_ **)** (ODBC 1.0)|Devuelve el coseno de *float_exp*, donde *float_exp* es un ángulo expresado en radianes.|  
|**COT(** _float_exp_ **)** (ODBC 1.0)|Devuelve la cotangente de *float_exp*, donde *float_exp* es un ángulo expresado en radianes.|  
|**DEGREES(** _numeric_exp_ **)** (ODBC 2.0)|Devuelve el número de grados convertidos desde *numeric_exp* radianes.|  
|**EXP(** _float_exp_ **)** (ODBC 1.0)|Devuelve el valor exponencial de *float_exp*.|  
|**PLANTA(** _numeric_exp_ **)** (ODBC 1.0)|Devuelve el entero más grande menor o igual que *numeric_exp*. El valor devuelto es del mismo tipo de datos que el parámetro de entrada.|  
|**LOG(** _float_exp_ **)** (ODBC 1.0)|Devuelve el ritmoaritmo natural de *float_exp*.|  
|**LOG10(** _float_exp_ **)** (ODBC 2.0)|Devuelve el logarritmo base 10 de *float_exp*.|  
|**MOD(** _integer_exp1_, _integer_exp2_**)** (ODBC 1.0)|Devuelve el resto (módulo) de *integer_exp1* dividido por *integer_exp2*.|  
|**PI( )** (ODBC 1.0)|Devuelve el valor constante de pi como un valor de punto flotante.|  
|**POWER(** _numeric_exp_, _integer_exp_**)** (ODBC 2.0)|Devuelve el valor de *numeric_exp* a la potencia de *integer_exp*.|  
|**RADIANS(** _numeric_exp_ **)** (ODBC 2.0)|Devuelve el número de radianes convertidos a partir de *numeric_exp* grados.|  
|**RAND(**[*integer_exp*]**)** (ODBC 1.0)|Devuelve un valor de punto flotante aleatorio mediante *integer_exp* como valor de semilla opcional.|  
|**ROUND(** _numeric_exp_, _integer_exp_**)** (ODBC 2.0)|Devuelve *numeric_exp* redondeado a *integer_exp* lugares a la derecha del punto decimal. Si *integer_exp* es negativo, *numeric_exp* se redondea a &#124;*integer_exp*&#124; lugares a la izquierda del punto decimal.|  
|**SIGN(** _numeric_exp_ **)** (ODBC 1.0)|Devuelve un indicador del signo de *numeric_exp*. Si *numeric_exp* es menor que cero, se devuelve -1. Si *numeric_exp* es igual a cero, se devuelve 0. Si *numeric_exp* es mayor que cero, se devuelve 1.|  
|**SIN(** _float_exp_ **)** (ODBC 1.0)|Devuelve el seno de *float_exp,* donde *float_exp* es un ángulo expresado en radianes.|  
|**SQRT(** _float_exp_ **)** (ODBC 1.0)|Devuelve la raíz cuadrada de *float_exp*.|  
|**TAN(** _float_exp_ **)** (ODBC 1.0)|Devuelve la tangente de *float_exp*, donde *float_exp* es un ángulo expresado en radianes.|  
|**TRUNCATE(** _numeric_exp_, _integer_exp_**)** (ODBC 2.0)|Devuelve *numeric_exp* truncaa a *integer_exp* lugares a la derecha del punto decimal. Si *integer_exp* es negativo, *numeric_exp* se trunca en &#124;*integer_exp*&#124; lugares a la izquierda del punto decimal.|
