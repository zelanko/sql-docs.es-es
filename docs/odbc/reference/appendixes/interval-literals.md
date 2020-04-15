---
title: Literales de intervalos ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1761ac0acb57b3f375a7d19e9371384c000eca5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304946"
---
# <a name="interval-literals"></a>Literales de intervalo
ODBC requiere que todos los controladores admitan la conversión del tipo de datos SQL_CHAR o SQL_VARCHAR a todos los tipos de datos de intervalo de C. Sin embargo, si el origen de datos subyacente no admite tipos de datos de intervalo, el controlador debe conocer el formato correcto del valor en el campo SQL_CHAR para admitir estas conversiones. De forma similar, ODBC requiere que cualquier tipo ODBC C sea convertible a SQL_CHAR o SQL_VARCHAR, por lo que un controlador debe saber qué formato debe tener un intervalo almacenado en el campo de caracteres. En esta sección se describe la sintaxis de los literales de intervalo, que el escritor de controladores debe usar para validar los campos de SQL_CHAR durante la conversión a o desde tipos de datos de intervalo C.  
  
> [!NOTE]  
>  La sintaxis BNF completa para literales de intervalo se muestra en la sección [Sintaxis literal](../../../odbc/reference/appendixes/interval-literal-syntax.md) de intervalo en Apéndice C: Gramática SQL.  
  
 Para pasar literales de intervalo como parte de una instrucción SQL, se define una sintaxis de cláusula de escape para los literales de intervalo. Para obtener más información, consulte Literales de [fecha, hora y marca](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)de tiempo .  
  
 Un literal de intervalo tiene la forma:  
  
```  
INTERVAL[<sign>] 'value' <interval qualifier>  
```  
  
 donde "INTERVAL" indica que el literal de carácter es un intervalo. El signo puede ser más o menos; está fuera de la cadena de intervalo y es opcional.  
  
 El calificador de intervalo puede ser un único campo datetime o \<estar compuesto por dos campos datetime, en el formulario: *campo inicial*> campo TO \< *final*>.  
  
-   Cuando el intervalo se compone de un solo campo, el campo único puede ser un campo que no sea segundo y que puede ir acompañado de una precisión inicial opcional entre paréntesis. El único campo datetime también puede ser un segundo campo que puede ir acompañado de la precisión inicial opcional, la precisión de fracciones de segundo opcional entre paréntesis o ambos. Si una precisión inicial y una precisión de fracciones de segundo están presentes durante un campo de segundos, se separan por comas. Si el campo de segundos tiene una precisión de fracciones de segundo, también debe tener una precisión inicial.  
  
-   Cuando el intervalo se compone de campos iniciales y finales, el campo inicial es un campo no segundo que puede ir acompañado de la precisión del campo inicial del intervalo entre paréntesis. El campo final puede ser un campo que no sea segundo o un segundo campo que puede ir acompañado de una precisión de fraccionamiento-segundos de intervalo entre paréntesis.  
  
 La cadena de intervalo en *el valor* se incluye entre comillas simples. Puede ser un literal de un mes de año o un literal de día. El formato de la cadena en *value* viene determinado por las siguientes reglas:  
  
-   La cadena contiene un valor decimal para \<cada campo que está implícito en el *calificador* de *intervalo*>.  
  
-   Si la precisión del intervalo incluye los campos YEAR y MONTH, los valores de estos campos se separan mediante un signo menos.  
  
-   Si la precisión del intervalo incluye los campos DAY y HOUR, los valores de estos campos están separados por un espacio.  
  
-   Si la precisión del intervalo incluye el campo HOUR y los campos de orden inferior (MINUTE y SECOND), los valores de estos campos están separados por dos puntos.  
  
-   Si la precisión del intervalo incluye un campo SECOND y la precisión de segundos expresa o implícita es distinta de cero, el carácter inmediatamente antes del primer dígito de la parte fraccionaria del segundo es un punto.  
  
-   Ningún campo puede tener más de dos dígitos, excepto:  
  
    -   El valor del campo inicial puede ser siempre que la precisión inicial del intervalo expresa o implícita.  
  
    -   La parte fraccionaria del campo SECOND puede ser siempre y cuando la precisión de segundos expresa o implícita.  
  
    -   Los campos finales siguen las restricciones habituales del calendario gregoriano. (Consulte [Restricciones del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md).)  
  
 En la tabla siguiente se muestran ejemplos de literales de intervalo válidos tal como se incluyen en la cláusula de escape ODBC para intervalos. La sintaxis de la cláusula escape es la siguiente:  
  
> [!NOTE]  
>  *•INTERVAL sign interval-string interval-qualifier ?*  
  
|Cláusula de escape literal|Intervalo especificado|  
|---------------------------|------------------------|  
|•INTERVAL '326' YEAR(4)|Especifica un intervalo de 326 años. La precisión inicial del intervalo es 4.|  
|•INTERVAL '326' MES(3)|Especifica un intervalo de 326 meses. La precisión inicial del intervalo es 3.|  
|•INTERVAL '3261' DIA(4)|Especifica un intervalo de 3261 días. La precisión inicial del intervalo es 4.|  
|•INTERVALO '163' HORA(3)|Especifica un intervalo de 163 días. La precisión inicial del intervalo es 3.|  
|•INTERVAL '163' MINUTE(3) ?|Especifica un intervalo de 163 minutos. La precisión inicial del intervalo es 3.|  
|•INTERVAL '223.16' SEGUNDO(3,2)|Especifica un intervalo de 223,16 segundos. La precisión inicial del intervalo es 3, y la precisión de segundos es 2.|  
|•INTERVAL '163-11' AÑO(3) A MES|Especifica un intervalo de 163 años y 11 meses. La precisión inicial del intervalo es 3.|  
|•INTERVALO '163 12' DIA(3) A HORA ?|Especifica un intervalo de 163 días y 12 horas. La precisión inicial del intervalo es 3.|  
|•INTERVALO '163 12:39' DIA(3) A MINUTOS ?|Especifica un intervalo de 163 días, 12 horas y 39 minutos. La precisión inicial del intervalo es 3.|  
|•INTERVALO '163 12:39:59.163' DIA(3) A SEGUNDO(3)|Especifica un intervalo de 163 días, 12 horas, 39 minutos y 59.163 segundos. La precisión inicial del intervalo es 3, y la precisión de los segundos es 3.|  
|•INTERVALO '163:39' HORA(3) A MINUTO ?|Especifica un intervalo de 163 horas y 39 minutos. La precisión inicial del intervalo es 3.|  
|•INTERVALO '163:39:59.163' HORA(3) A SEGUNDO(4)|Especifica un intervalo de 163 horas, 39 minutos y 59.163 segundos. La precisión inicial del intervalo es 3, y la precisión de los segundos es 4.|  
|•INTERVAL '163:59.163' MINUTO(3) A SEGUNDO(5) ?|Especifica un intervalo de 163 minutos y 59.163 segundos. La precisión inicial del intervalo es 3, y la precisión de los segundos es 5.|  
|•INTERVAL -'16 23:39:56.23' DIA A SEGUNDO?|Especifica un intervalo de menos 16 días, 23 horas, 39 minutos y 56,23 segundos. La precisión inicial implícita es 2, y la precisión de segundos implícita es 6.|  
  
 En la tabla siguiente se muestran ejemplos de literales de intervalo no válidos:  
  
|Cláusula de escape literal|Motivo por el que no es válido|  
|---------------------------|------------------------|  
|•INTERVAL '163' HORA(2) ?|La precisión inicial del intervalo es 2, pero el valor del campo inicial es 163.|  
|•INTERVAL '223.16' SEGUNDO(2,2)<br /><br /> •INTERVAL '223.16' SEGUNDO(3,1)|En el primer ejemplo, la precisión inicial es demasiado pequeña y, en el segundo ejemplo, la precisión de los segundos es demasiado pequeña.|  
|•INTERVAL '223.16' SEGUNDO<br /><br /> •INTERVAL '223' YEAR ?|Dado que la precisión inicial no está especificada, el valor predeterminado es 2, que es demasiado pequeño para contener el literal especificado.|  
|•INTERVAL '22.1234567' SEGUNDO|La precisión de los segundos no se especifica, por lo que el valor predeterminado es 6. El literal tiene siete dígitos después del punto decimal.|  
|•INTERVAL '163-13' AÑO(3) A MES<br /><br /> •INTERVALO '163 65' DIA(3) A HORA ?<br /><br /> •INTERVALO '163 62:39' DIA(3) A MINUTOS ?<br /><br /> •INTERVALO '163 12:125:59.163' DIA(3) A SEGUNDO(3)<br /><br /> •INTERVALO '163:144' HORA(3) A MINUTO ?<br /><br /> •INTERVALO '163:567:234.163' HORA(3) A SEGUNDO(4)<br /><br /> •INTERVAL '163:591.163' MINUTO(3) A SEGUNDO(5)|El campo final no sigue las reglas del calendario gregoriano.|
