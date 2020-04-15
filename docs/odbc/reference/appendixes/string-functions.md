---
title: Funciones de cadena ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], string functions
- string functions [ODBC]
ms.assetid: 270f669e-8aab-4db0-95a4-f2b3c69538b3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d9323809028ad170a4811b1af8b6e276cdbb4293
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302846"
---
# <a name="string-functions"></a>Funciones de cadena
En la tabla siguiente se enumeran las funciones de manipulación de cadenas. Una aplicación puede determinar qué funciones de cadena son compatibles con un controlador mediante una llamada a **SQLGetInfo** con un tipo de *información* de SQL_STRING_FUNCTIONS.  
  
## <a name="remarks"></a>Observaciones  
 Los argumentos que se indican como *string_exp* pueden ser el nombre de una columna, un *carácter-cadena-literal*o el resultado de otra función escalar, donde el tipo de datos subyacente se puede representar como SQL_CHAR, SQL_VARCHAR o SQL_LONGVARCHAR.  
  
 Los argumentos que se indican como *character_exp* son una cadena de caracteres de longitud variable.  
  
 Los argumentos denotados como *start*, *length*o *count* pueden ser un *literal numérico* o el resultado de otra función escalar, donde el tipo de datos subyacente se puede representar como SQL_TINYINT, SQL_SMALLINT o SQL_INTEGER.  
  
 Las funciones de cadena enumeradas aquí están basadas en 1; es decir, el primer carácter de la cadena es el carácter 1.  
  
 Las funciones escalares de cadena BIT_LENGTH, CHAR_LENGTH, CHARACTER_LENGTH, OCTET_LENGTH y POSITION se han agregado en ODBC 3.0 para alinearse con SQL-92.  
  
|Función|Descripción|  
|--------------|-----------------|  
|**ASCII(** _string_exp_ **)** (ODBC 1.0)|Devuelve el valor de código ASCII del carácter más a la izquierda de *string_exp* como un entero.|  
|**BIT_LENGTH(** _string_exp_ **)** (ODBC 3.0)|Devuelve la longitud en bits de la expresión de cadena.<br /><br /> No funciona solo para tipos de datos de cadena, por lo tanto no convertirá implícitamente *string_exp* en cadena, sino que devolverá el tamaño (interno) del tipo de datos que se le dé.|  
|**CHAR(** _código_ **)** (ODBC 1.0)|Devuelve el carácter que tiene el valor de código ASCII especificado por *code*. El valor del *código* debe estar entre 0 y 255; de lo contrario, el valor devuelto depende del origen de datos.|  
|**CHAR_LENGTH(** _string_exp_ **)** (ODBC 3.0)|Devuelve la longitud en caracteres de la expresión de cadena, si la expresión de cadena es de un tipo de datos de carácter; de lo contrario, devuelve la longitud en bytes de la expresión de cadena (el entero más pequeño no menor que el número de bits divididos por 8). (Esta función es la misma que la función CHARACTER_LENGTH.)|  
|**CHARACTER_LENGTH(** _string_exp_ **)** (ODBC 3.0)|Devuelve la longitud en caracteres de la expresión de cadena, si la expresión de cadena es de un tipo de datos de carácter; de lo contrario, devuelve la longitud en bytes de la expresión de cadena (el entero más pequeño no menor que el número de bits divididos por 8). (Esta función es la misma que la función CHAR_LENGTH.)|  
|**CONCAT(** _string_exp1_,_string_exp2_**)** (ODBC 1.0)|Devuelve una cadena de caracteres que es el resultado de concatenar *string_exp2* a *string_exp1*. La cadena resultante es dependiente de DBMS. Por ejemplo, si la columna representada por *string_exp1* contiene un valor NULL, DB2 devolvería NULL pero SQL Serversql Server devolvería la cadena no NULL.|  
|**DIFFERENCE(** _string_exp1_,_string_exp2_**)** (ODBC 2.0)|Devuelve un valor entero que indica la diferencia entre los valores devueltos por la función SOUNDEX para *string_exp1* y *string_exp2*.|  
|**INSERT(** _string_exp1_, *start*, *length*, _string_exp2_**)** (ODBC 1.0)|Devuelve una cadena de caracteres donde se han eliminado caracteres de *longitud* de *string_exp1*, comenzando por *el inicio*y donde *string_exp2* se ha insertado en *string_exp,* comenzando por *el inicio.*|  
|**LCASE(** _string_exp_ **)** (ODBC 1.0)|Devuelve una cadena igual a la de *string_exp*, con todos los caracteres en mayúsculas convertidos a minúsculas.|  
|**IZQUIERDA(** _string_exp_, _recuento_**)** (ODBC 1.0)|Devuelve los caracteres de *recuento* más a la izquierda de *string_exp*.|  
|**LENGTH(** _string_exp_ **)** (ODBC 1.0)|Devuelve el número de caracteres de *string_exp,* excluyendo los espacios en blanco finales.<br /><br /> **LENGTH** solo acepta cadenas. Por lo tanto, se convertirá implícitamente *string_exp* en una cadena y devolver la longitud de esta cadena (no el tamaño interno del tipo de datos).|  
|**LOCATE(** _string_exp1_, *string_exp2*[, *start*]**)** (ODBC 1.0)|Devuelve la posición inicial de la primera aparición de *string_exp1* dentro de *string_exp2*. La búsqueda de la primera aparición de *string_exp1* comienza con la primera posición de carácter en *string_exp2* a menos que se especifique el argumento opcional, *start*, . Si se especifica *start,* la búsqueda comienza con la posición del carácter indicada por el valor de *start*. La primera posición de carácter en *string_exp2* se indica mediante el valor 1. Si no se encuentra *string_exp1* en *string_exp2*, se devuelve el valor 0.<br /><br /> Si una aplicación puede llamar a la función escalar LOCATE con los argumentos *string_exp1*, *string_exp2*e *start,* el controlador devuelve SQL_FN_STR_LOCATE cuando **SQLGetInfo** se llama con una *opción* de SQL_STRING_FUNCTIONS . Si la aplicación puede llamar a la función escalar LOCATE con solo los argumentos *string_exp1* y *string_exp2,* el controlador devuelve SQL_FN_STR_LOCATE_2 cuando **SQLGetInfo** se llama con una *opción* de SQL_STRING_FUNCTIONS. Los controladores que admiten la llamada a la función LOCATE con dos o tres argumentos devuelven SQL_FN_STR_LOCATE y SQL_FN_STR_LOCATE_2.|  
|**LTRIM(** _string_exp_ **)** (ODBC 1.0)|Devuelve los caracteres de *string_exp*, con espacios en blanco iniciales eliminados.|  
|**OCTET_LENGTH (** _string_exp_ **)** (ODBC 3.0)|Devuelve la longitud en bytes de la expresión de cadena. El resultado es el entero más pequeño que no es inferior al número de bits dividido por 8.<br /><br /> No funciona solo para tipos de datos de cadena, por lo tanto no convertirá implícitamente *string_exp* en cadena, sino que devolverá el tamaño (interno) del tipo de datos que se le dé.|  
|**POSITION(** _character_exp_ **IN** _character_exp_**)** (ODBC 3.0)|Devuelve la posición de la primera expresión de carácter en la segunda expresión de carácter. El resultado es un número exacto con una precisión definida por la implementación y una escala de 0.|  
|**REPEAT(** _string_exp,_ _count_**)** (ODBC 1.0)|Devuelve una cadena de caracteres compuesta por *string_exp* tiempos de *recuento* repetidos.|  
|**REPLACE(** _string_exp1_, *string_exp2*, _string_exp3_**)** (ODBC 1.0)|Buscar *string_exp1* de las ocurrencias de *string_exp2*y reemplazar con *string_exp3*.|  
|**DERECHA(** _string_exp_, _recuento_**)** (ODBC 1.0)|Devuelve los caracteres de *recuento* más a la derecha de *string_exp*.|  
|**RTRIM(** _string_exp_ **)** (ODBC 1.0)|Devuelve los caracteres de *string_exp* con los espacios en blanco finales eliminados.|  
|**SOUNDEX(** _string_exp_ **)** (ODBC 2.0)|Devuelve una cadena de caracteres dependiente del origen de datos que representa el sonido de las palabras *de string_exp*. Por ejemplo, SQL ServerSQL Server devuelve un código SOUNDEX de 4 dígitos; Oracle devuelve una representación fonética de cada palabra.|  
|**ESPACIO(** _recuento_ **)** (ODBC 2.0)|Devuelve una cadena de caracteres que consta de espacios de *recuento.*|  
|**SUBSTRING(** _string_exp_, *start*, length **)** (ODBC 1.0)|Devuelve una cadena de caracteres que se deriva de *string_exp*, comenzando en la posición de carácter especificada por *start* para los caracteres de *longitud.*|  
|**UCASE(** _string_exp_ **)** (ODBC 1.0)|Devuelve una cadena igual a la de *string_exp*, con todos los caracteres en minúsculas convertidos a mayúsculas.|
