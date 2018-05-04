---
title: Establecer valores de parámetro | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0e41f775ef6640f4f82aa16cea038becc305bf5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setting-parameter-values"></a>Establecer valores de parámetro
Para establecer el valor de un parámetro, la aplicación simplemente establece el valor de la variable enlazado al parámetro. No es importante cuando se establece este valor, siempre y cuando se establece antes de que se ejecuta la instrucción. La aplicación puede establecer el valor antes o después de enlazar la variable y puede cambiar el valor tantas veces como desee. Cuando se ejecuta la instrucción, el controlador simplemente recupera el valor actual de la variable. Esto es especialmente útil cuando se ejecuta una instrucción preparada varias veces; la aplicación establece nuevos valores para algunas o todas las variables de cada vez que se ejecuta la instrucción. Para obtener un ejemplo de esto, consulte [ejecución preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md), anteriormente en esta sección.  
  
 Si se enlaza un búfer de longitud/indicador en la llamada a **SQLBindParameter**, debe establecerse en uno de los siguientes valores antes de que se ejecuta la instrucción:  
  
-   La longitud de bytes de los datos de la variable enlazada. El controlador comprueba esta longitud sólo si la variable es de carácter o binario (*ValueType* es SQL_C_CHAR o SQL_C_BINARY).  
  
-   SQL_NTS. Los datos están una cadena terminada en null.  
  
-   SQL_NULL_DATA. El valor de datos es NULL y el controlador omite el valor de la variable enlazada.  
  
-   SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC. El valor del parámetro es se envíe con **SQLPutData**. Para obtener más información, consulte [enviar datos largos](../../../odbc/reference/develop-app/sending-long-data.md), más adelante en esta sección.  
  
 En la tabla siguiente se muestra los valores de la variable enlazada y del búfer de longitud/indicador que la aplicación se configura para una amplia variedad de valores de parámetro.  
  
|Parámetro<br /><br /> value|Parámetro<br /><br /> (SQL)<br /><br /> tipo de datos|Variable (C)<br /><br /> tipo de datos|Valor de<br /><br /> enlazadas<br /><br /> variable|Valor de<br /><br /> indicador de longitud<br /><br /> búferes [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|SQL_NTS o 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10\0 [a]|SQL_NTS o 2|  
|1 P. M.|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0 [b]|--|  
|1 P. M.|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13: 00:00'} \0 [a], [c]|SQL_NTS o 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\0" representa un carácter de terminación null. Se requiere el carácter de terminación null solo si el valor en el búfer de longitud/indicador es SQL_NTS.  
  
 [b] los números de esta lista son los números almacenados en los campos de la estructura TIME_STRUCT.  
  
 [c] la cadena utiliza la cláusula de escape de fecha ODBC. Para obtener más información, consulte [fecha, hora y marca de tiempo literales](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 [d] controladores siempre deben comprobar este valor para ver si se trata de un valor especial, como SQL_NULL_DATA.  
  
 Lo que hace un controlador con un valor de parámetro en tiempo de ejecución depende del controlador. Si es necesario, el controlador convierte el valor de la longitud de bytes y de tipo de datos de C de la variable enlazada al tipo de datos SQL, precisión y escala del parámetro. En la mayoría de los casos, el controlador, a continuación, envía el valor al origen de datos. En algunos casos, se da formato al valor como texto y se inserta en la instrucción SQL antes de enviar la instrucción al origen de datos.
