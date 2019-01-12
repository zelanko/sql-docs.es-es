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
ms.openlocfilehash: 47711a7e974373e9da4ac8068295029d88accaf6
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54125625"
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
|**ABS (** _numeric_exp_ **)** (ODBC 1.0)|Devuelve el valor absoluto de *numeric_exp*.|  
|**ACOS (** _float_exp_ **)** (ODBC 1.0)|Devuelve el arcocoseno de *float_exp* como un ángulo, expresado en radianes.|  
|**ASIN (** _float_exp_ **)** (ODBC 1.0)|Devuelve el arcoseno de *float_exp* como un ángulo, expresado en radianes.|  
|**ATAN (** _float_exp_ **)** (ODBC 1.0)|Devuelve el arco tangente de *float_exp* como un ángulo, expresado en radianes.|  
|**ATAN2 (** _float_exp1_, _float_exp2_**)** (ODBC 2.0)|Devuelve el arco tangente de la *x* y *y* coordenadas, especificadas por *float_exp1* y *float_exp2*, respectivamente, como un ángulo, expresado en radianes.|  
|**CEILING (** _numeric_exp_ **)** (ODBC 1.0)|Devuelve el entero más pequeño mayor o igual a *numeric_exp*. El valor devuelto es del mismo tipo de datos como parámetro de entrada.|  
|**COS (** _float_exp_ **)** (ODBC 1.0)|Devuelve el coseno de *float_exp*, donde *float_exp* es el ángulo, expresado en radianes.|  
|**COT (** _float_exp_ **)** (ODBC 1.0)|Devuelve la cotangente de *float_exp*, donde *float_exp* es el ángulo, expresado en radianes.|  
|**GRADOS (** _numeric_exp_ **)** (ODBC 2.0)|Devuelve el número de grados convertido a partir de *numeric_exp* radianes.|  
|**EXP (** _float_exp_ **)** (ODBC 1.0)|Devuelve el valor exponencial de *float_exp*.|  
|**FLOOR (** _numeric_exp_ **)** (ODBC 1.0)|Devuelve el entero más grande menor o igual a *numeric_exp*. El valor devuelto es del mismo tipo de datos como parámetro de entrada.|  
|**REGISTRO (** _float_exp_ **)** (ODBC 1.0)|Devuelve el logaritmo natural de *float_exp*.|  
|**LOG10 (** _float_exp_ **)** (ODBC 2.0)|Devuelve la base 10 logaritmo de *float_exp*.|  
|**MOD (** _integer_exp1_, _integer_exp2_**)** (ODBC 1.0)|Devuelve el resto (módulo) de *integer_exp1* dividido por *integer_exp2*.|  
|**PI ()** (ODBC 1.0)|Devuelve el valor constante de pi como un valor de punto flotante.|  
|**POWER (** _numeric_exp_, _integer_exp_**)** (ODBC 2.0)|Devuelve el valor de *numeric_exp* a la potencia de *integer_exp*.|  
|**RADIANS (** _numeric_exp_ **)** (ODBC 2.0)|Devuelve el número de radianes convertido a partir de *numeric_exp* grados.|  
|**RAND (**[*integer_exp*]**)** (ODBC 1.0)|Devuelve un valor de punto flotante aleatorio con *integer_exp* como el valor de inicialización opcional.|  
|**ROUND (** _numeric_exp_, _integer_exp_**)** (ODBC 2.0)|Devuelve *numeric_exp* redondeado a *integer_exp* coloca a la derecha del separador decimal. Si *integer_exp* es negativo, *numeric_exp* se redondea a &#124; *integer_exp* &#124; coloca a la izquierda del separador decimal.|  
|**Inicio de sesión (** _numeric_exp_ **)** (ODBC 1.0)|Devuelve un indicador de la sesión de *numeric_exp*. Si *numeric_exp* es menor que cero, -1 se devuelve. Si *numeric_exp* es igual a cero, se devuelve 0. Si *numeric_exp* es mayor que cero, se devuelve 1.|  
|**SENO (** _float_exp_ **)** (ODBC 1.0)|Devuelve el seno de *float_exp*, donde *float_exp* es el ángulo, expresado en radianes.|  
|**SQRT (** _float_exp_ **)** (ODBC 1.0)|Devuelve la raíz cuadrada de *float_exp*.|  
|**TAN (** _float_exp_ **)** (ODBC 1.0)|Devuelve la tangente de *float_exp*, donde *float_exp* es el ángulo, expresado en radianes.|  
|**TRUNCATE (** _numeric_exp_, _integer_exp_**)** (ODBC 2.0)|Devuelve *numeric_exp* truncado a *integer_exp* coloca a la derecha del separador decimal. Si *integer_exp* es negativo, *numeric_exp* se trunca a &#124; *integer_exp* &#124; coloca a la izquierda del separador decimal.|
