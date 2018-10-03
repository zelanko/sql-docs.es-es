---
title: Funciones de cadena | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0eeccf4e9c972592f8efecb622fc71f4f3c87a0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720063"
---
# <a name="string-functions"></a>Funciones de cadena
En la tabla siguiente se enumera las funciones de manipulación de cadena. Una aplicación puede determinar qué funciones de cadena son compatibles con un controlador mediante una llamada a **SQLGetInfo** con un *tipo de información* de SQL_STRING_FUNCTIONS.  
  
## <a name="remarks"></a>Comentarios  
 Argumentos que se indican como *string_exp* puede ser el nombre de una columna, una *literal de cadena de caracteres*, o el resultado de otra función escalar, donde el tipo de datos subyacente puede representarse como SQL_CHAR, SQL_ VARCHAR o SQL_LONGVARCHAR.  
  
 Argumentos que se indican como *character_exp* son una cadena de caracteres de longitud variable.  
  
 Argumentos que se indican como *iniciar*, *longitud*, o *recuento* puede ser un *literales numéricos* o el resultado de otra función escalar, donde el tipo de datos subyacente puede representarse como SQL_TINYINT, SQL_SMALLINT o SQL_INTEGER.  
  
 Las funciones de cadena que se muestran aquí son basado en 1; es decir, el primer carácter de la cadena es 1 carácter.  
  
 Las funciones escalares de cadena BIT_LENGTH, CHAR_LENGTH, CHARACTER_LENGTH, OCTET_LENGTH y posición se agregaron en ODBC 3.0 para alinearse con SQL-92.  
  
|Función|Descripción|  
|--------------|-----------------|  
|**ASCII (** *string_exp* **)** (ODBC 1.0)|Devuelve el valor del código ASCII del carácter más a la izquierda de *string_exp* como un entero.|  
|**BIT_LENGTH (** *string_exp* **)** (ODBC 3.0)|Devuelve la longitud en bits de la expresión de cadena.<br /><br /> No solo funcionan en tipos de datos de cadena, por lo tanto no implícitamente le convert *string_exp* en una cadena, pero en su lugar, devolverá el tamaño (interno) de cualquier tipo de datos se le asigna.|  
|**CHAR (** *código* **)** (ODBC 1.0)|Devuelve el carácter que tiene el ASCII especificado por el valor de código *código*. El valor de *código* debe estar comprendido entre 0 y 255; en caso contrario, el valor devuelto es depende del origen de datos.|  
|**CHAR_LENGTH (** *string_exp* **)** (ODBC 3.0)|Devuelve la longitud en caracteres de la expresión de cadena, si la expresión de cadena es de un tipo de datos de caracteres; en caso contrario, devuelve la longitud en bytes de la expresión de cadena (el entero más pequeño no inferior al número de bits dividido por 8). (Esta función es igual a la función CHARACTER_LENGTH).|  
|**CHARACTER_LENGTH (** *string_exp* **)** (ODBC 3.0)|Devuelve la longitud en caracteres de la expresión de cadena, si la expresión de cadena es de un tipo de datos de caracteres; en caso contrario, devuelve la longitud en bytes de la expresión de cadena (el entero más pequeño no inferior al número de bits dividido por 8). (Esta función es igual a la función CHAR_LENGTH).|  
|**CONCAT (** *string_exp1*,*string_exp2 ***)** (ODBC 1.0)|Devuelve una cadena de caracteres que es el resultado de concatenar *string_exp2* a *string_exp1*. La cadena resultante es dependiente de DBMS. Por ejemplo, si la columna representada por *string_exp1* contiene un valor NULL, DB2 devuelto NULL, pero SQL Server se devolvería la cadena no nula.|  
|**DIFERENCIA (** *string_exp1*,*string_exp2 ***)** (ODBC 2.0)|Devuelve un valor entero que indica la diferencia entre los valores devueltos por la función SOUNDEX para *string_exp1* y *string_exp2*.|  
|**Insertar (** *string_exp1*, *iniciar*, *longitud*, *string_exp2 ***)** (ODBC 1.0)|Devuelve un carácter de una cadena where *longitud* caracteres se han eliminado de *string_exp1*, comenzando en *iniciar*y donde *string_exp2* se ha insertado en *string_exp,* comenzando por *iniciar*.|  
|**LCASE (** *string_exp* **)** (ODBC 1.0)|Devuelve una cadena igual que en *string_exp*, con todas mayúsculas se convierten a minúsculas.|  
|**IZQUIERDA (** *string_exp*, *recuento ***)** (ODBC 1.0)|Devuelve el extremo izquierdo *recuento* caracteres de *string_exp*.|  
|**LONGITUD (** *string_exp* **)** (ODBC 1.0)|Devuelve el número de caracteres de *string_exp,* excluyendo los espacios en blanco.<br /><br /> **LONGITUD** solo acepta cadenas. Por lo tanto, convertirá implícitamente *string_exp* a una cadena y devuelve la longitud de esta cadena (no el tamaño interno del tipo de datos).|  
|**Buscar (** *string_exp1*, *string_exp2*[, *iniciar*]**)** (ODBC 1.0)|Devuelve la posición inicial de la primera aparición de *string_exp1* en *string_exp2*. La búsqueda de la primera aparición de *string_exp1* comienza con la posición del primer carácter en *string_exp2* a menos que el argumento opcional, *iniciar*, se especifica. Si *iniciar* se especifica, la búsqueda comienza con la posición del carácter indicada por el valor de *iniciar*. Posición del primer carácter en *string_exp2* está indicado por el valor 1. Si *string_exp1* no se encuentra dentro de *string_exp2*, se devuelve el valor 0.<br /><br /> Si una aplicación puede llamar a la función escalar de buscar con el *string_exp1*, *string_exp2*, y *iniciar* argumentos, el controlador devuelve SQL_FN_STR_LOCATE cuando  **SQLGetInfo** se denomina con un *opción* de SQL_STRING_FUNCTIONS. Si la aplicación puede llamar a la función escalar de buscar solamente con la *string_exp1* y *string_exp2* argumentos, el controlador devuelve SQL_FN_STR_LOCATE_2 cuando **SQLGetInfo**se llama con un *opción* de SQL_STRING_FUNCTIONS. Los controladores compatibles con una llamada a la función Buscar con dos o tres argumentos devuelven SQL_FN_STR_LOCATE y SQL_FN_STR_LOCATE_2.|  
|**LTRIM (** *string_exp* **)** (ODBC 1.0)|Devuelve los caracteres de *string_exp*, con los principales quitadas los espacios en blanco.|  
|**OCTET_LENGTH (** *string_exp* **)** (ODBC 3.0)|Devuelve la longitud en bytes de la expresión de cadena. El resultado es el entero más pequeño que no es inferior al número de bits dividido por 8.<br /><br /> No solo funcionan en tipos de datos de cadena, por lo tanto no implícitamente le convert *string_exp* en una cadena, pero en su lugar, devolverá el tamaño (interno) de cualquier tipo de datos se le asigna.|  
|**POSICIÓN (** *character_exp* **IN** *character_exp ***)** (ODBC 3.0)|Devuelve la posición de la primera expresión de carácter en la segunda expresión de caracteres. El resultado es un valor numérico exacto con una precisión definido por la implementación y una escala de 0.|  
|**Repita (** *string_exp,* *recuento ***)** (ODBC 1.0)|Devuelve una cadena de caracteres que se compone de *string_exp* repite *recuento* veces.|  
|**Reemplazar (** *string_exp1*, *string_exp2*, *string_exp3 ***)** (ODBC 1.0)|Búsqueda *string_exp1* foroccurrences de *string_exp2*y reemplace con *string_exp3*.|  
|**DERECHA (** *string_exp*, *recuento ***)** (ODBC 1.0)|Devuelve el extremo derecho *recuento* caracteres de *string_exp*.|  
|**RTRIM (** *string_exp* **)** (ODBC 1.0)|Devuelve los caracteres de *string_exp* con finales quitadas los espacios en blanco.|  
|**SOUNDEX (** *string_exp* **)** (ODBC 2.0)|Devuelve una cadena de caracteres depende del origen de datos que representa el sonido de las palabras de *string_exp*. Por ejemplo, SQL Server devuelve un código SOUNDEX de 4 dígitos; Oracle devuelve una representación fonética de cada palabra.|  
|**ESPACIO (** *recuento* **)** (ODBC 2.0)|Devuelve una cadena de caracteres formado por *recuento* espacios.|  
|**SUBSTRING (** *string_exp*, *iniciar*, longitud **)** (ODBC 1.0)|Devuelve una cadena de caracteres que se deriva de *string_exp*, comenzando en la posición del carácter especificada por *iniciar* para *longitud* caracteres.|  
|**UCASE (** *string_exp* **)** (ODBC 1.0)|Devuelve una cadena igual que en *string_exp*, con todos los caracteres convertidos en mayúsculas de minúsculas.|
