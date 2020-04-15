---
title: Transferir la longitud del octeto ? Microsoft Docs
ms.custom: ''
ms.date: 10/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- data types [ODBC], transfer octet length
ms.assetid: 9fdc9762-e203-4cff-9212-54f450bf18d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4204b47816747506a5672241eeeef736eca54856
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302816"
---
# <a name="transfer-octet-length"></a>Transferir la longitud en octetos
La longitud del octeto de transferencia de una columna es el número máximo de bytes devueltos a la aplicación cuando los datos se transfieren a su tipo de datos C predeterminado. Para los datos de caracteres, la longitud del octeto de transferencia no incluye espacio para el carácter de terminación nula. La longitud del octeto de transferencia de una columna puede ser diferente del número de bytes necesarios para almacenar los datos en el origen de datos.  
  
 La longitud de octeto de transferencia definida para cada tipo de datos SQL ODBC se muestra en la tabla siguiente.  
  
|Identificador de tipo SQL|Length|  
|-------------------------|------------|  
|Todos los tipos de caracteres[a]|La longitud definida o máxima (para el tipo de variable) de la columna en bytes. Este es el mismo valor que el campo descriptor SQL_DESC_OCTET_LENGTH.|  
|SQL_DECIMAL<br />SQL_NUMERIC|El número de bytes necesarios para contener la representación de caracteres de estos datos si el juego de caracteres es ANSI y el doble de este número si el juego de caracteres es UNICODE. Este es el número máximo de dígitos más dos, porque los datos se devuelven como una cadena de caracteres y se necesitan caracteres para los dígitos, un signo y un punto decimal. Por ejemplo, la longitud de transferencia de una columna definida como NUMERIC(10,3) es 12.|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT| 8 |  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|Todos los tipos binarios[a]|El número de bytes necesarios para contener el número definido (para tipos fijos) o máximo (para tipos variables) de caracteres.|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (el tamaño de la estructura SQL_DATE_STRUCT o SQL_TIME_STRUCT).|  
|SQL_TYPE_TIMESTAMP|16 (el tamaño de la estructura SQL_TIMESTAMP_STRUCT).|  
|Todos los tipos de datos de intervalo|34 (el tamaño de la estructura de intervalos).|  
|SQL_GUID|16 (el tamaño de la estructura GUID).|  
| &nbsp; | &nbsp; |

 [a] Si el controlador no puede determinar la longitud de columna o parámetro para tipos de variables, devuelve SQL_NO_TOTAL.
