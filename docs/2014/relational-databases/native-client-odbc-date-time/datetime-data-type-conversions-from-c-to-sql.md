---
title: Conversiones de C a SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], C to SQL
ms.assetid: 7ac098db-9147-4883-8da9-a58ab24a0d31
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 638f3acea8ba4d9925851a26bd84ab20f76c38c9
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37410083"
---
# <a name="conversions-from-c-to-sql"></a>Conversiones de C a SQL
  En este tema se enumera los problemas para tener en cuenta al convertir de tipos C [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de fecha y hora.  
  
 Las conversiones descritas en la tabla siguiente se aplican a conversiones realizadas en el cliente. En los casos en que el cliente especifica para un parámetro una precisión de fracciones de segundo diferente de la definida en el servidor, la conversión puede llegar a realizarse en el cliente pero el servidor devolverá un error cuando se llame a `SQLExecute` o `SQLExecuteDirect`. Concretamente, ODBC trata cualquier truncamiento de fracciones de segundo como un error, mientras que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza un redondeo; por ejemplo, el redondeo se produce cuando se pasa de `datetime2(6)` a `datetime2(2)`. Los valores de las columnas datetime se redondean a la fracción 1/300 de segundo, mientras que para las columnas smalldatetime, el servidor establece los segundos en cero.  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
||SQL_TYPE_DATE|SQL_TYPE_TIME|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|SQL_CHAR|SQL_WCHAR|  
|SQL_C_DATE|1|-|-|1,6|1,5,6|1,13|1,13|  
|SQL_C_TIME|-|1|1|1,7|1,5,7|1,13|1,13|  
|SQL_C_SS_TIME2|-|1,3|1,10|1,7|1,5,7|1,13|1,13|  
|SQL_C_BINARY (SQL_SS_TIME2_STRUCT)|N/D|N/D|1,10,11|N/D|N/D|N/D|N/D|  
|SQL_C_TYPE_TIMESTAMP|1,2|1,3,4|1,4,10|1,10|1,5,10|1,13|1,13|  
|SQL_C_SS_TIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10|1,10|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIMESTAMPOFFSET_STRUCT)|N/D|N/D|N/D|N/D|1,10,11|N/D|N/D|  
|SQL_C_CHAR/SQL_WCHAR (date)|9|9|9|9,6|9,5,6|N/D|N/D|  
|SQL_C_CHAR/SQL_WCHAR (time2)|9|9,3|9,10|9,7,10|9,5,7,10|N/D|N/D|  
|SQL_C_CHAR/SQL_WCHAR (datetime)|9,2|9,3,4|9,4,10|9,10|9,5,10|N/D|N/D|  
|SQL_C_CHAR/SQL_WCHAR (datetimeoffset)|9,2,8|9,3,4,8|9,4,8,10|9,8,10|9,10|N/D|N/D|  
|SQL_C_BINARY(SQL_DATE_STRUCT)|1,11|N/D|N/D|N/D|N/D|N/D|N/D|  
|SQL_C_BINARY(SQL_TIME_STRUCT)|N/D|N/D|N/D|N/D|N/D|N/D|N/D|  
|SQL_C_BINARY(SQL_TIMESTAMP_STRUCT)|N/D|N/D|N/D|N/D|N/D|N/D|N/D|  
  
## <a name="key-to-symbols"></a>Clave de los símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|-|No se admite la conversión. Se genera un registro de diagnóstico con SQLSTATE 07006 y el mensaje "Infracción del atributo de tipo de datos restringido".|  
|1|Si los datos proporcionados no son válidos, se genera un registro de diagnóstico con SQLSTATE 22007 y el mensaje "Formato de fecha y hora no válido".|  
|2|Los campos de hora deben ser cero o, de lo contrario, se genera un registro de diagnóstico con SQLSTATE 22008 y el mensaje "Truncamiento fraccionario".|  
|3|Las fracciones de segundo deben ser cero o, de lo contrario, se genera un registro de diagnóstico con SQLSTATE 22008 y el mensaje "Truncamiento fraccionario".|  
|4|Se omite el componente de fecha.|  
|5|La zona horaria se establece en el valor de zona horaria del cliente.|  
|6|La hora se establece en cero.|  
|7|La fecha se establece en la fecha actual.|  
|8|La hora se convierte de la zona horaria del cliente a UTC. Si se produce un error durante esta conversión, se genera un registro de diagnóstico con SQLSTATE 22008 y el mensaje "Desbordamiento del campo DateTime".|  
|9|La cadena se analiza y se convierte en un valor date, datetime, datetimeoffset o time, dependiendo del primer carácter de puntuación encontrado y de la presencia de otros componentes. A continuación, la cadena se convierte al tipo de destino, siguiendo las reglas de la tabla anterior para el tipo de origen detectado por este proceso. Si se detecta un error mientras se analizan los datos, se genera un registro de diagnóstico con SQLSTATE 22018 y el mensaje "Valor de carácter no válido para especificación cast". Para los parámetros datetime y smalldatetime, si el año está fuera del intervalo admitido por estos tipos, se genera un registro de diagnóstico con SQLSTATE 22007 y el mensaje "Formato de fecha y hora no válido".<br /><br /> Para datetimeoffset, el valor debe estar comprendido dentro del intervalo después de la conversión a UTC, aunque no se haya solicitado ninguna conversión a UTC. Esto se debe a que la secuencia de datos tabulares (TDS) y el servidor siempre normalizan la hora en valores datetimeoffset para UTC, de modo que el cliente tenga que comprobar que los componentes de hora están dentro del intervalo admitido después de la conversión a UTC. Si el valor no está dentro del intervalo UTC admitido, se genera un registro de diagnóstico con SQLSTATE 22007 y el mensaje "Formato de fecha y hora no válido".|  
|10|Si se produce un truncamiento con pérdida de datos, se genera un registro de diagnóstico con SQLSTATE 22008 y el mensaje "Formato de hora no válido". Este error también se produce si el valor está fuera del intervalo que puede representarse mediante el intervalo UTC utilizado por el servidor.|  
|11|Si la longitud de bytes de los datos no coincide con el tamaño de la estructura requerida por el tipo SQL, se genera un registro de diagnóstico con SQLSTATE 22003 y el mensaje "Valor numérico fuera del intervalo".|  
|12|Si la longitud de bytes de los datos es 4 u 8, los datos se envían al servidor en formato datetime o smalldatetime TDS sin procesar. Si la longitud de bytes de los datos coincide exactamente con el tamaño de SQL_TIMESTAMP_STRUCT, los datos se convierten al formato TDS para datetime2.|  
|13|Si se produce un truncamiento con pérdida de datos, se genera un registro de diagnóstico con SQLSTATE 22001 y el mensaje "Cadena truncada por la derecha".<br /><br /> El número de dígitos de fracciones de segundo (la escala) se determina a partir de tamaño de la columna de destino según lo siguiente:<br /><br /> **Tipo:** SQL_C_TYPE_TIMESTAMP<br /><br /> Escala supuesta<br /><br /> 0<br /><br /> 19<br /><br /> Escala supuesta<br /><br /> 1..9<br /><br /> 21..29<br /><br /> Sin embargo, para SQL_C_TYPE_TIMESTAMP, si las fracciones de segundo se pueden representar con tres dígitos sin perder datos y el tamaño de columna es 23 o superior, se generan exactamente tres dígitos de fracciones de segundo. Este comportamiento asegura la compatibilidad con versiones anteriores para aplicaciones desarrolladas utilizando controladores ODBC anteriores.<br /><br /> Si el tamaño de las columnas es mayor que el intervalo de la tabla, se presupone una escala de 9. Esta conversión debe permitir hasta nueve dígitos de fracciones de segundo, el máximo permitido por ODBC.<br /><br /> Un tamaño de columna igual a cero implica un tamaño ilimitado de los tipos de caracteres de longitud variable en ODBC (9 dígitos, a menos que sea aplicable la regla de 3 dígitos para SQL_C_TYPE_TIMESTAMP). Especificar un tamaño de columna igual a cero con un tipo de caracteres de longitud fija es un error.|  
|N/D|Se mantiene el comportamiento de las versiones actuales y anteriores de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
  
## <a name="see-also"></a>Vea también  
 [Mejoras de fecha y hora &#40;ODBC&#41;](date-and-time-improvements-odbc.md)  
  
  
