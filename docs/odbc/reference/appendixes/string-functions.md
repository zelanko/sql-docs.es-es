---
title: Funciones de cadena | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- functions [ODBC], string functions
- string functions [ODBC]
ms.assetid: 270f669e-8aab-4db0-95a4-f2b3c69538b3
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1a9afffd67b839b36e663404048ac741e068b015
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="string-functions"></a>Funciones de cadena
En la tabla siguiente se enumera las funciones de manipulación de cadena. Una aplicación puede determinar qué funciones de cadena son compatibles con un controlador mediante una llamada a **SQLGetInfo** con una *tipo de información* de SQL_STRING_FUNCTIONS.  
  
## <a name="remarks"></a>Comentarios  
 Argumentos que se denotan *string_exp* puede ser el nombre de una columna, una *literal de cadena de caracteres*, o el resultado de otra función escalar, donde se puede representar el tipo de datos subyacente como SQL_CHAR, SQL_ VARCHAR o SQL_LONGVARCHAR.  
  
 Argumentos que se denotan *character_exp* consisten en una cadena de caracteres de longitud variable.  
  
 Argumentos que se denotan *iniciar*, *longitud*, o *recuento* puede ser un *literal numérico* o el resultado de otra función escalar, donde el tipo de datos subyacente se puede representar como SQL_TINYINT, SQL_SMALLINT o SQL_INTEGER.  
  
 Las funciones de cadena que se enumeran aquí están basados en 1; es decir, el primer carácter de la cadena de carácter 1.  
  
 Se han agregado las funciones escalares de cadena BIT_LENGTH, CHAR_LENGTH, CHARACTER_LENGTH, OCTET_LENGTH y posición en ODBC 3.0 se alineen con SQL-92.  
  
|Función|Description|  
|--------------|-----------------|  
|**ASCII (** *string_exp* **)** (ODBC 1.0)|Devuelve el valor de código ASCII del carácter más a la izquierda de *string_exp* como un entero.|  
|**BIT_LENGTH (** *string_exp* **)** (ODBC 3.0)|Devuelve la longitud en bits de la expresión de cadena.<br /><br /> No funciona únicamente para los tipos de datos de cadena, por lo tanto no implícitamente le convert *string_exp* a cadena pero en su lugar, devolverá el tamaño (interno) de cualquier tipo de datos que se genera.|  
|**CHAR (** *código* **)** (ODBC 1.0)|Devuelve el carácter que tiene el ASCII especificado por el valor de código *código*. El valor de *código* debe estar entre 0 y 255; en caso contrario, el valor devuelto es: depende del origen de datos.|  
|**CHAR_LENGTH (** *string_exp* **)** (ODBC 3.0)|Devuelve la longitud en caracteres de la expresión de cadena, si la expresión de cadena es de un tipo de datos character; en caso contrario, devuelve la longitud en bytes de la expresión de cadena (el entero más pequeño no menor que el número de bits dividido por 8). (Esta función es igual a la función CHARACTER_LENGTH).|  
|**CHARACTER_LENGTH (** *string_exp* **)** (ODBC 3.0)|Devuelve la longitud en caracteres de la expresión de cadena, si la expresión de cadena es de un tipo de datos character; en caso contrario, devuelve la longitud en bytes de la expresión de cadena (el entero más pequeño no menor que el número de bits dividido por 8). (Esta función es igual a la función CHAR_LENGTH).|  
|**CONCAT (** *string_exp1*,*string_exp2***)** (ODBC 1.0)|Devuelve una cadena de caracteres que es el resultado de la concatenación de *string_exp2* a *string_exp1*. La cadena resultante es dependiente de DBMS. Por ejemplo, si la columna representada por *string_exp1* contiene un valor NULL, DB2 devuelto NULL, pero SQL Server se devolvería la cadena no nulo.|  
|**DIFERENCIA (** *string_exp1*,*string_exp2***)** (ODBC 2.0)|Devuelve un valor entero que indica la diferencia entre los valores devueltos por la función SOUNDEX para *string_exp1* y *string_exp2*.|  
|**Insertar (** *string_exp1*, *iniciar*, *longitud*, *string_exp2***)** (ODBC 1.0)|Devuelve un carácter de una cadena where *longitud* caracteres que se haya eliminado de *string_exp1*, empezando en *iniciar*y dónde *string_exp2* se ha insertado en *string_exp,* empezando por *iniciar*.|  
|**LCASE (** *string_exp* **)** (ODBC 1.0)|Devuelve una cadena igual que en *string_exp*, con todas las mayúsculas convertida en minúsculas.|  
|**IZQUIERDA (** *string_exp*, *recuento***)** (ODBC 1.0)|Devuelve el extremo izquierdo *recuento* caracteres de *string_exp*.|  
|**LONGITUD (** *string_exp* **)** (ODBC 1.0)|Devuelve el número de caracteres de *string_exp,* excluyendo los espacios en blanco.<br /><br /> **LONGITUD** solo acepta cadenas. Por lo tanto, convertirá implícitamente *string_exp* a una cadena y devuelve la longitud de esta cadena (no el tamaño interno del tipo de datos).|  
|**Buscar (** *string_exp1*, *string_exp2*[, *iniciar*]**)** (ODBC 1.0)|Devuelve la posición inicial de la primera aparición de *string_exp1* en *string_exp2*. La búsqueda de la primera aparición de *string_exp1* comienza con la posición del primer carácter en *string_exp2* a menos que el argumento opcional, *iniciar*, se especifica. Si *iniciar* se especifica, la búsqueda comienza con la posición de carácter indicada por el valor de *iniciar*. El primer carácter que se coloque en *string_exp2* se indica mediante el valor 1. Si *string_exp1* no se encuentra en *string_exp2*, se devuelve el valor 0.<br /><br /> Si una aplicación puede llamar a la función escalar de buscar con el *string_exp1*, *string_exp2*, y *iniciar* argumentos, el controlador devuelve SQL_FN_STR_LOCATE cuando ** SQLGetInfo** se llama con un *opción* de SQL_STRING_FUNCTIONS. Si la aplicación puede llamar a la función escalar de buscar solamente con el *string_exp1* y *string_exp2* argumentos, el controlador devuelve SQL_FN_STR_LOCATE_2 cuando **SQLGetInfo**se llama con un *opción* de SQL_STRING_FUNCTIONS. Los controladores compatibles con una llamada a la función Buscar con dos o tres argumentos devuelven SQL_FN_STR_LOCATE y SQL_FN_STR_LOCATE_2.|  
|**LTRIM (** *string_exp* **)** (ODBC 1.0)|Devuelve los caracteres de *string_exp*, precedido de los espacios en blanco iniciales.|  
|**OCTET_LENGTH (** *string_exp* **)** (ODBC 3.0)|Devuelve la longitud en bytes de la expresión de cadena. El resultado es el entero más pequeño que no es inferior al número de bits dividido por 8.<br /><br /> No funciona únicamente para los tipos de datos de cadena, por lo tanto no implícitamente le convert *string_exp* a cadena pero en su lugar, devolverá el tamaño (interno) de cualquier tipo de datos que se genera.|  
|**POSICIÓN (** *character_exp* **IN** *character_exp***)** (ODBC 3.0)|Devuelve la posición de la primera expresión de caracteres en la segunda expresión de caracteres. El resultado es un valor numérico exacto con una precisión definido por la implementación y una escala de 0.|  
|**Repita (** *string_exp,* *recuento***)** (ODBC 1.0)|Devuelve una cadena de caracteres que se compone de *string_exp* repite *recuento* veces.|  
|**Reemplazar (** *string_exp1*, *string_exp2*, *string_exp3***)** (ODBC 1.0)|Búsqueda *string_exp1* foroccurrences de *string_exp2*y reemplace por *string_exp3*.|  
|**DERECHA (** *string_exp*, *recuento***)** (ODBC 1.0)|Devuelve el extremo derecho *recuento* caracteres de *string_exp*.|  
|**RTRIM (** *string_exp* **)** (ODBC 1.0)|Devuelve los caracteres de *string_exp* con quita los espacios en blanco a la derecha.|  
|**SOUNDEX (** *string_exp* **)** (ODBC 2.0)|Devuelve una cadena de caracteres depende del origen de datos que representa el sonido de las palabras en *string_exp*. Por ejemplo, SQL Server devuelve un código SOUNDEX de 4 dígitos; Oracle devuelve una representación fonética de cada palabra.|  
|**ESPACIO (** *recuento* **)** (ODBC 2.0)|Devuelve una cadena de caracteres que se compone de *recuento* espacios.|  
|**SUBSTRING (** *string_exp*, *iniciar*, longitud**)** (ODBC 1.0)|Devuelve una cadena de caracteres que se deriva de *string_exp*, empezando en la posición de carácter especificada por *iniciar* para *longitud* caracteres.|  
|**UCASE (** *string_exp* **)** (ODBC 1.0)|Devuelve una cadena igual que en *string_exp*, con todos los caracteres convertidas en mayúsculas de minúsculas.|

