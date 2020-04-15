---
title: Identificadores y descriptores de tipo de datos ( Data Type Identifiers and Descriptors) Microsoft Docs
ms.custom: ''
ms.date: 02/02/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
- descriptors [ODBC], data types
- verbose data types [ODBC]
- data types [ODBC], descriptors
- concise data types [ODBC]
ms.assetid: f0077c9b-8eb2-4b5f-8c4c-7436fdef37ab
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f65bc86213f99112daf17c67a4ca522490d32149
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284488"
---
# <a name="data-type-identifiers-and-descriptors"></a>Identificadores y descriptores de tipo de datos
Los tipos de datos enumerados en las secciones Tipos de [datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) y Tipos de [datos C](../../../odbc/reference/appendixes/c-data-types.md) anteriores en este apéndice son tipos de datos "concisos": cada identificador hace referencia a un único tipo de datos. Hay una correspondencia uno a uno entre el identificador y el tipo de datos. Los descriptores, sin embargo, no utilizan en todos los casos un solo valor para identificar tipos de datos. En algunos casos, usan un tipo de datos "detallado" y un subcódigo de tipo. Para todos los tipos de datos excepto los tipos de datos datetime e interval, el identificador de tipo detallado es el mismo que el identificador de tipo conciso y el valor de SQL_DESC_DATETIME_INTERVAL_CODE es igual a 0. Para los tipos de datos datetime e interval, sin embargo, se almacena un tipo detallado (SQL_DATETIME o SQL_INTERVAL) en SQL_DESC_TYPE, se almacena un tipo conciso en SQL_DESC_CONCISE_TYPE y se almacena un subcódigo para cada tipo conciso en SQL_DESC_DATETIME_INTERVAL_CODE. Establecer uno de estos campos afecta a los demás. Para obtener más información acerca de estos campos, vea la descripción de la función [SQLSetDescField.](../../../odbc/reference/syntax/sqlsetdescfield-function.md)  
  
 Cuando se establece el SQL_DESC_TYPE o SQL_DESC_CONCISE_TYPE campo para algunos tipos de datos, los campos SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_LENGTH, SQL_DESC_PRECISION y SQL_DESC_SCALE se establecen automáticamente en valores predeterminados, según corresponda para el tipo de datos. Para obtener más información, vea la descripción del campo SQL_DESC_TYPE en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Si alguno de los valores predeterminados establecidos no es adecuado, la aplicación debe establecer explícitamente el campo descriptor mediante una llamada a **SQLSetDescField**.  
  
 En la tabla siguiente se muestra el identificador de tipo conciso, el identificador de tipo detallado y el subcódigo de tipo para cada identificador de tipo datetime e interval SQL y C. Como indica esta tabla, para los tipos de datos datetime e interval, los campos SQL_DESC_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE tienen las mismas constantes de manifiesto tanto para los tipos de datos SQL (en descriptores de implementación) como para los tipos de datos C (en descriptores de aplicación).  
  
|Tipo SQL conciso|Tipo C conciso|Tipo detallado|DATETIME_INTERVAL_CODE|  
|----------------------|--------------------|------------------|------------------------------|  
|SQL_TYPE_DATE|SQL_C_TYPE_DATE|SQL_DATETIME|SQL_CODE_DATE|  
|SQL_TYPE_TIME|SQL_C_TYPE_TIME|SQL_DATETIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_DATETIME|SQL_CODE_TIMESTAMP|  
|SQL_INTERVAL_MONTH|SQL_C_INTERVAL_MONTH|SQL_INTERVAL|SQL_CODE_MONTH|  
|SQL_INTERVAL_YEAR|SQL_C_INTERVAL_YEAR|SQL_INTERVAL|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_INTERVAL|SQL_CODE_YEAR_TO_MONTH|  
|SQL_INTERVAL_DAY|SQL_C_INTERVAL_DAY|SQL_INTERVAL|SQL_CODE_DAY|  
|SQL_INTERVAL_HOUR|SQL_C_INTERVAL_HOUR|SQL_INTERVAL|SQL_CODE_HOUR|  
|SQL_INTERVAL_MINUTE|SQL_C_INTERVAL_MINUTE|SQL_INTERVAL|SQL_CODE_MINUTE|  
|SQL_INTERVAL_SECOND|SQL_C_INTERVAL_SECOND|SQL_INTERVAL|SQL_CODE_SECOND|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_C_INTERVAL_DAY_TO_HOUR|SQL_INTERVAL|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE|SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_INTERVAL|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND|SQL_C_INTERVAL_DAY_TO_SECOND|SQL_INTERVAL|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR_TO_MINUTE|SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_INTERVAL|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND|SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_INTERVAL|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE_TO_SECOND|SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_INTERVAL|SQL_CODE_MINUTE_TO_SECOND|
