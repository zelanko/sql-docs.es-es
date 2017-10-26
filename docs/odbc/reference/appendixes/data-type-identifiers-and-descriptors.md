---
title: Identificadores y descriptores de tipo de datos | Documentos de Microsoft
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
- data types [ODBC], identifiers
- identifiers [ODBC], data types
- descriptors [ODBC], data types
- verbose data types [ODBC]
- data types [ODBC], descriptors
- concise data types [ODBC]
ms.assetid: f0077c9b-8eb2-4b5f-8c4c-7436fdef37ab
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 93b813632c3a281e1ae0ba90e95545e28d07ed09
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="data-type-identifiers-and-descriptors"></a>Identificadores de tipo de datos y los descriptores de
Los tipos de datos enumeran en el [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) y [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md) secciones anteriormente en este apéndice son tipos de datos "concisa": cada identificador hace referencia a un tipo de datos único. Hay una correspondencia uno a uno entre el identificador y el tipo de datos. Descriptores, sin embargo, hacer no en todos los casos utilice un valor único para identificar los tipos de datos. En algunos casos, usan un tipo de datos "detallados" y un subcódigo de tipo. Para todos los tipos de datos excepto los tipos de datos datetime e interval, el identificador de tipo detallado es el mismo que el identificador de tipo concisa y el valor de SQL_DESC_DATETIME_INTERVAL_CODE es igual a 0. Para los tipos de datos datetime e interval, sin embargo, un tipo detallado (SQL_DATETIME o SQL_INTERVAL) se almacena en SQL_DESC_TYPE, un tipo conciso se almacena en SQL_DESC_CONCISE_TYPE y un subcódigo para cada tipo concisa se almacena en SQL_DESC_DATETIME_INTERVAL_CODE. Configuración de uno de estos campos afecta a los demás. Para obtener más información acerca de estos campos, vea el [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) descripción de la función.  
  
 Cuando se establece el campo SQL_DESC_TYPE o SQL_DESC_CONCISE_TYPE para algunos tipos de datos, los campos SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_LENGTH, SQL_DESC_PRECISION y SQL_DESC_SCALE se establecen automáticamente en valores predeterminados, según sea pertinente para los datos tipo. Para obtener más información, vea la descripción del campo SQL_DESC_TYPE en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Si cualquiera de los valores predeterminados establecidos no es adecuado, la aplicación debe establecer explícitamente el campo descriptor a través de una llamada a **SQLSetDescField**.  
  
 En la tabla siguiente se muestra el identificador de tipo concisa, el identificador de tipo detallado y el subcódigo de tipo para cada fecha y hora y el intervalo de SQL y el identificador de tipo de C. Tal y como se indica en esta tabla, para los tipos de datos datetime e interval, los campos SQL_DESC_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE tienen el mismo constantes de manifiesto para tipos de datos SQL (en los descriptores de implementación) y para los tipos de datos de C (en la aplicación descriptores).  
  
|Tipo SQL concisa|Tipo de C concisa|Tipo detallado|DATETIME_INTERVAL_CODE|  
|----------------------|--------------------|------------------|------------------------------|  
|SQL_TYPE_DATE|SQL_C_TYPE_DATE|SQL_DATETIME|SQL_CODE_DATE|  
|SQL_TYPE_TIME|SQL_C_TYPE_TIME|SQL_DATETIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_DATETIME|SQL_CODE_TIMESTAMP|  
|SQL_INTERVAL_MONTH|SQL_C_INTERVAL_MONTH|SQL_INTERVAL|SQL_CODE_MONTH|  
|SQL_INTERVAL_YEAR|SQL_C_INTERVAL_YEAR|SQL_INTERVAL|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_INTERVAL|SQL_CODE_YEAR_TO_MONTH|  
QL_INTERVAL_DAY|SQL_C_INTERVAL_DAY|SQL_INTERVAL|SQL_CODE_DAY|  
|SQL_INTERVAL_HOUR|SQL_C_INTERVAL_HOUR|SQL_INTERVAL|SQL_CODE_HOUR|  
|SQL_INTERVAL_MINUTE|SQL_C_INTERVAL_MINUTE|SQL_INTERVAL|SQL_CODE_MINUTE|  
|SQL_INTERVAL_SECOND|SQL_C_INTERVAL_SECOND|SQL_INTERVAL|SQL_CODE_SECOND|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_C_INTERVAL_DAY_TO_HOUR|SQL_INTERVAL|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE|SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_INTERVAL|SQL_CODE_DAY_TO_MINUTE|  
QL_INTERVAL_DAY_TO_SECOND|SQL_C_INTERVAL_DAY_TO_SECOND|SQL_INTERVAL|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR_TO_MINUTE|SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_INTERVAL|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND|SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_INTERVAL|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE_TO_SECOND|SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_INTERVAL|SQL_CODE_MINUTE_TO_SECOND|

