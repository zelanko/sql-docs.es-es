---
description: Establecer valores de parámetro
title: Establecer valores de parámetro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af2992ea66601ec0ae4804e327863e6abb285d73
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476427"
---
# <a name="setting-parameter-values"></a>Establecer valores de parámetro
Para establecer el valor de un parámetro, la aplicación simplemente establece el valor de la variable enlazada al parámetro. No es importante cuando se establece este valor, siempre y cuando se establezca antes de que se ejecute la instrucción. La aplicación puede establecer el valor antes o después de enlazar la variable, y puede cambiar el valor tantas veces como desee. Cuando se ejecuta la instrucción, el controlador simplemente recupera el valor actual de la variable. Esto es especialmente útil cuando una instrucción preparada se ejecuta más de una vez. la aplicación establece nuevos valores para algunas o todas las variables cada vez que se ejecuta la instrucción. Para obtener un ejemplo de esto, vea [ejecución preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md), anteriormente en esta sección.  
  
 Si un búfer de longitud/indicador se enlazó en la llamada a **SQLBindParameter**, debe establecerse en uno de los siguientes valores antes de que se ejecute la instrucción:  
  
-   Longitud de bytes de los datos de la variable enlazada. El controlador comprueba esta longitud solo si la variable es un carácter o binario (*ValueType* es SQL_C_CHAR o SQL_C_BINARY).  
  
-   SQL_NTS. Los datos son una cadena terminada en NULL.  
  
-   SQL_NULL_DATA. El valor de los datos es NULL y el controlador omite el valor de la variable enlazada.  
  
-   SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC. El valor del parámetro se va a enviar con **SQLPutData**. Para obtener más información, vea [envío de datos largos](../../../odbc/reference/develop-app/sending-long-data.md), más adelante en esta sección.  
  
 En la tabla siguiente se muestran los valores de la variable enlazada y el búfer de longitud/indicador que establece la aplicación para una variedad de valores de parámetro.  
  
|Parámetro<br /><br /> value|Parámetro<br /><br /> Server<br /><br /> tipo de datos|Variable (C)<br /><br /> tipo de datos|Valor de <br /><br /> enlazadas<br /><br /> variable|Valor de <br /><br /> longitud/indicador<br /><br /> búfer [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|SQL_NTS o 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10 \ 0 [a]|SQL_NTS o 2|  
|1 P.M.|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13, 0, 0 [b]|--|  
|1 P.M.|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13:00:00 '} \ 0 [a], [c]|SQL_NTS o 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\ 0" representa un carácter de terminación null. El carácter de terminación null solo es necesario si el valor del búfer de longitud/indicador es SQL_NTS.  
  
 [b] los números de esta lista son los números almacenados en los campos de la estructura TIME_STRUCT.  
  
 [c] la cadena usa la cláusula de escape ODBC Date. Para obtener más información, vea [literales de fecha, hora y marca de tiempo](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 [d] los controladores siempre deben comprobar este valor para ver si se trata de un valor especial, como SQL_NULL_DATA.  
  
 Lo que hace un controlador con un valor de parámetro en tiempo de ejecución depende del controlador. Si es necesario, el controlador convierte el valor del tipo de datos C y la longitud de bytes de la variable enlazada al tipo de datos SQL, la precisión y la escala del parámetro. En la mayoría de los casos, el controlador envía el valor al origen de datos. En algunos casos, da formato al valor como texto y lo inserta en la instrucción SQL antes de enviar la instrucción al origen de datos.
