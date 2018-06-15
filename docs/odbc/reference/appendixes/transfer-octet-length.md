---
title: Transferir la longitud en octetos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- data types [ODBC], transfer octet length
ms.assetid: 9fdc9762-e203-4cff-9212-54f450bf18d9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 157dbea8954dd7823888360c7d9cf74d9c8db74d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909765"
---
# <a name="transfer-octet-length"></a>Longitud de bytes de transferencia
La longitud de bytes de transferencia de una columna es el número máximo de bytes que se devuelven a la aplicación cuando se transfieren datos a su tipo de datos C predeterminado. Para datos de caracteres, la longitud de bytes de transferencia no incluye espacio para el carácter de terminación null. La longitud de octeto de transferencia de una columna puede ser diferente del número de bytes necesarios para almacenar los datos en el origen de datos.  
  
 La longitud de octeto de transferencia definida para cada tipo de datos SQL de ODBC se muestra en la tabla siguiente.  
  
|Identificador de tipo SQL|Longitud|  
|-------------------------|------------|  
|Todos los tipos de caracteres [a]|Las personalizaciones definidas o la longitud máxima (por tipo de variable) de la columna en bytes. Este es el mismo valor que el campo descriptor SQL_DESC_OCTET_LENGTH.|  
|SQL_DECIMAL<br />SQL_NUMERIC|El número de bytes necesario para contener la representación de caracteres de estos datos si el juego de caracteres es ANSI y dos veces este número si el juego de caracteres es UNICODE. Este es el número máximo de dígitos y dos, porque los datos se devuelven como una cadena de caracteres y caracteres son necesarios para los dígitos, un inicio de sesión y un separador decimal. Por ejemplo, la longitud de la transferencia de una columna definida como NUMERIC(10,3) es 12.|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT|El número de bytes necesario para contener la representación de caracteres de estos datos si el juego de caracteres es ANSI y dos veces este número si el juego de caracteres es UNICODE, porque este tipo de datos se devuelve como una cadena de caracteres de forma predeterminada. La representación de caracteres que se compone de 20 caracteres: 19 dígitos y un inicio de sesión, si firmado o 20 dígitos, si no firmado. Por lo tanto, la longitud es 20.|  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|Todos los tipos binarios [a]|El número de bytes necesarios para almacenar las personalizaciones definidas (para tipos fijos) o el número máximo (para tipos de variables) de caracteres.|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (el tamaño de la estructura SQL_DATE_STRUCT o SQL_TIME_STRUCT).|  
|SQL_TYPE_TIMESTAMP|16 (el tamaño de la estructura SQL_TIMESTAMP_STRUCT).|  
|Todos los tipos de datos de intervalo|34 (el tamaño de la estructura de intervalo).|  
|SQL_GUID|16 (el tamaño de la estructura GUID).|  
  
 [a] si el controlador no puede determinar la longitud de columna o parámetro de tipos de variables, devuelve SQL_NO_TOTAL.
