---
title: Literales de intervalo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval literals [ODBC]
- interval data type [ODBC], literals
ms.assetid: f9e6c3c7-4f98-483f-89d8-ebc5680f021b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc5d09bca83724bb956d39512c51c3dc47db1bad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188804"
---
# <a name="interval-literals"></a>Literales de intervalo
ODBC exige que todos los controladores para admiten la conversión del tipo de datos SQL_CHAR o SQL_VARCHAR a todos los tipos de datos de intervalo de C. Sin embargo, si el origen de datos subyacente no admite tipos de datos interval, el controlador necesita conocer el formato correcto del valor en el campo SQL_CHAR para admitir estas conversiones. De forma similar, ODBC requiere que se debe tener cualquier tipo ser convertible a SQL_CHAR o SQL_VARCHAR, por lo que necesita saber qué formato de un intervalo que se almacena en el campo de carácter un controlador de C de ODBC. En esta sección se describe la sintaxis de literales de intervalo, que debe usar para validar los campos SQL_CHAR durante la conversión a o desde tipos de datos de intervalo de C el escritor de controlador.  
  
> [!NOTE]  
>  La sintaxis completa de BNF para literales de intervalo se muestra en la sección [sintaxis de literales de intervalo](../../../odbc/reference/appendixes/interval-literal-syntax.md) en el apéndice C: Gramática de SQL.  
  
 Para pasar los literales de intervalo como parte de una instrucción SQL, se define una sintaxis de cláusulas de escape para literales de intervalo. Para obtener más información, consulte [fecha, hora y marca de tiempo literales](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Un literal de intervalo tiene el formato:  
  
```  
INTERVAL[<sign>] 'value' <interval qualifier>  
```  
  
 donde "INTERVAL" indica que el literal de carácter es un intervalo. El inicio de sesión puede ser más o menos; está fuera de la cadena de intervalo y es opcional.  
  
 El calificador de intervalo puede ser un campo datetime único o estar formada por dos campos de fecha y hora, en el formulario: \< *campo inicial*> TO \< *campo final*>.  
  
-   Cuando el intervalo se compone de un solo campo, el campo solo puede ser un campo de segundos no puede estar acompañado por una precisión inicial opcional entre paréntesis. El campo datetime único puede ser también un segundo campo que puede estar acompañado por la precisión inicial opcional, la precisión en segundos fraccionaria opcional entre paréntesis o ambos. Si hay una precisión inicial y una precisión de fracciones de segundos para un campo de segundos, están separados por comas. Si el campo de segundos tiene una precisión de fracciones de segundos, también debe tener una precisión inicial.  
  
-   Cuando el intervalo se compone de campos iniciales y finales, el campo inicial es un campo de segundos no puede estar acompañado por el intervalo inicial de precisión del campo entre paréntesis. El campo al final puede ser un campo que no son segundos o un segundo campo que puede estar acompañado por una precisión de fracciones de segundos de intervalo entre paréntesis.  
  
 La cadena de intervalo en *valor* se encierra entre comillas simples. Puede ser un literal de mes del año o un literal de hora del día. El formato de la cadena en *valor* viene determinada por las reglas siguientes:  
  
-   La cadena contiene un valor decimal para cada campo que está implícito en el \< *intervalo* *calificador*>.  
  
-   Si la precisión de intervalo incluye los campos de año y mes, los valores de estos campos están separados por un signo menos.  
  
-   Si la precisión de intervalo incluye los campos de día y hora, los valores de estos campos están separados por un espacio.  
  
-   Si la precisión de intervalo incluye el campo de hora y los campos de orden inferior (minuto y segundo), los valores de estos campos están separados por dos puntos.  
  
-   Si la precisión de intervalo incluye un segundo campo y la precisión de segundos expresa o implícita es distinto de cero, el carácter inmediatamente antes del primer dígito de la parte fraccionaria de segundo es un punto.  
  
-   Ningún campo puede ser más de dos dígitos, excepto:  
  
    -   El valor del campo inicial puede ser tan largo como el intervalo expresado o implícito de precisión del principio.  
  
    -   La parte fraccionaria del segundo campo puede ser tan larga como la precisión de segundos expresas o implícitas.  
  
    -   Los campos finales siguen las restricciones habituales del calendario gregoriano. (Consulte [restricciones del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md).)  
  
 En la tabla siguiente se muestra ejemplos de literales de intervalo válido, tal como se incluye en la cláusula de escape ODBC para los intervalos. La sintaxis de la cláusula de escape es como sigue:  
  
> [!NOTE]  
>  *{Cadena del intervalo de inicio de sesión de intervalo intervalo-qualifier}*  
  
|Cláusula de escape literal|Intervalo especificado|  
|---------------------------|------------------------|  
|{YEAR(4) INTERVALO '326'}|Especifica un intervalo de años 326. El intervalo de precisión inicial es 4.|  
|{MONTH(3) INTERVALO '326'}|Especifica un intervalo de meses 326. El intervalo de precisión inicial es 3.|  
|{DAY(4) INTERVALO '3261'}|Especifica un intervalo de días 3261. El intervalo de precisión inicial es 4.|  
|{HOUR(3) INTERVALO '163'}|Especifica un intervalo de días 163. El intervalo de precisión inicial es 3.|  
|{MINUTE(3) INTERVALO '163'}|Especifica un intervalo de minutos 163. El intervalo de precisión inicial es 3.|  
|{SECOND(3,2) INTERVALO '223.16'}|Especifica un intervalo de segundos 223.16. La precisión de intervalo inicial es 3, y la precisión de segundos es 2.|  
|{INTERVALO ' 163-11' AÑO (3) AL MES}|Especifica un intervalo de 163 años y 11 meses. El intervalo de precisión inicial es 3.|  
|{INTERVALO 163 ' 12' DAY(3) HORA}|Especifica un intervalo de 163 días y 12 horas. El intervalo de precisión inicial es 3.|  
|{INTERVALO ' 163 12:39 ' DAY(3) AL MINUTO}|Especifica un intervalo de 163 días, 12 horas y 39 minutos. El intervalo de precisión inicial es 3.|  
|{INTERVALO '163 12:39:59.163' DAY(3) A SECOND(3)}|Especifica un intervalo de 163 días, 12 horas, 39 minutos y 59.163 segundos. La precisión de intervalo inicial es 3, y la precisión de segundos es 3.|  
|{INTERVALO HOUR(3) AL MINUTO ' 163:39'}|Especifica un intervalo de 163 horas y 39 minutos. El intervalo de precisión inicial es 3.|  
|{INTERVALO '163:39:59.163' HOUR(3) A SECOND(4)}|Especifica un intervalo de 163 horas, 39 minutos y 59.163 segundos. La precisión de intervalo inicial es 3, y la precisión de segundos es 4.|  
|{INTERVALO '163:59.163' MINUTE(3) A SECOND(5)}|Especifica un intervalo de 163 minutos y 59.163 segundos. La precisión de intervalo inicial es 3, y la precisión de segundos es 5.|  
|{INTERVAL-'16 23:39:56.23' DÍA A SEGUNDO}|Especifica un intervalo de menos de 16 días, 23 horas, 39 minutos y 56.23 segundos. La precisión inicial implícita es 2, y la precisión de segundos implícito es 6.|  
  
 En la tabla siguiente se enumera algunos ejemplos de literales de intervalo no válido:  
  
|Cláusula de escape literal|Motivo por qué no válido|  
|---------------------------|------------------------|  
|{HOUR(2) INTERVALO '163'}|La precisión de intervalo inicial es 2, pero el valor del campo inicial es 163.|  
|{SECOND(2,2) INTERVALO '223.16'}<br /><br /> {SECOND(3,1) INTERVALO '223.16'}|En el primer ejemplo, la precisión inicial es demasiado pequeña y, en el segundo ejemplo, la precisión de segundos es demasiado pequeña.|  
|{INTERVALO '223.16' SEGUNDO}<br /><br /> {INTERVALO '223' YEAR}|Dado que la precisión inicial no se especifica, el valor predeterminado es 2, que es demasiado pequeño para contener el literal especificado.|  
|{INTERVALO '22.1234567' SEGUNDO}|Por lo que el valor predeterminado es 6, no se especifica, la precisión de segundos. El literal tiene siete dígitos después del separador decimal.|  
|{INTERVALO ' 163-13' AÑO (3) AL MES}<br /><br /> {INTERVALO ' 163 65' DAY(3) HORA}<br /><br /> {INTERVALO '163 62:39' DAY(3) AL MINUTO}<br /><br /> {INTERVALO '163 12:125:59.163' DAY(3) A SECOND(3)}<br /><br /> {INTERVALO HOUR(3) AL MINUTO ' 163:144'}<br /><br /> {INTERVALO '163:567:234.163' HOUR(3) A SECOND(4)}<br /><br /> {INTERVALO '163:591.163' MINUTE(3) A SECOND(5)}|El campo al final no sigue las reglas del calendario gregoriano.|
