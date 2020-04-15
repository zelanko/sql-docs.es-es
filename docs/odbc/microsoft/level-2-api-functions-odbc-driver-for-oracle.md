---
title: Funciones de API de nivel 2 (controlador ODBC para Oracle) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- ODBC API functions [ODBC]
- API functions [ODBC]
- level 2 API functions [ODBC]
ms.assetid: d9f49520-72d7-4234-8635-260d0ce4199c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1e181c5863d6b906eaf9a3ba499728c595f0449
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284185"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>Funciones de API de nivel 2 (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Las funciones de este nivel proporcionan conformidad de interfaz de nivel 1, además de funcionalidad adicional, como compatibilidad con marcadores, parámetros dinámicos y ejecución asincrónica de funciones ODBC.  
  
|Función API|Notas|  
|------------------|-----------|  
|**SQLBindParameter**|Asocia un búfer con un marcador de parámetro en una instrucción SQL.|  
|**SQLBrowseConnect**|Devuelve niveles sucesivos de atributos y valores de atributo.|  
|**SQLDataSources**|Enumera los nombres de origen de datos. Implementado por el Administrador de controladores.|  
|**SQLDescribeParam**|Devuelve la descripción de un marcador de parámetro asociado a una instrucción SQL preparada.<br /><br /> Devuelve una mejor conjetura de lo que es el parámetro, basado en el análisis de la instrucción. Si no se puede determinar el tipo de parámetro, SQL_VARCHAR devuelve con la longitud 2000.|  
|**SQLDrivers**|Implementado por el Administrador de controladores.|  
|**SQLExtendedFetch**|Similar a **SQLFetch** pero devuelve varias filas mediante una matriz para cada columna. El conjunto de resultados se puede desplazar hacia delante y se puede hacer desplazable hacia atrás si el cursor se define como estático, no de solo avance. Para los cursores de solo avance con enlace de columna predeterminado, los datos de columna de conjuntos de datos mayores que el atributo de conexión BUFFERSIZE se capturan directamente en los búferes de datos. No admite marcadores de longitud variable y no admite la obtención de un conjunto de filas en un desplazamiento (distinto de 0) de un marcador.|  
|**SQLForeignKeys**|Devuelve una lista de claves externas en una sola tabla o una lista de claves externas en otras tablas que hacen referencia a una sola tabla.|  
|**SQLMoreResults**|Determina si hay más resultados pendientes en un identificador de instrucción, hstmt, que contiene instrucciones SELECT, UPDATE, INSERT o DELETE y, si es así, inicializa el procesamiento de esos resultados.<br /><br /> Oracle solo admite varios conjuntos de resultados de procedimientos almacenados, cuando se utilizan secuencias de escape .|  
|**SQLNativeSql**|Para obtener información sobre el uso, consulte [Devolución de parámetros de matriz desde procedimientos almacenados](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLNumParams**|Devuelve el número de parámetros de una instrucción SQL. El número de parámetros debe ser igual al número de signos de interrogación de la instrucción SQL pasada a **SQLPrepare**.|  
|**SQLPrimaryKeys**|Devuelve los nombres de columna que componen la clave principal de una tabla.|  
|**SQLProcedureColumns**|Devuelve una lista de parámetros de entrada y salida, el valor devuelto, las columnas del conjunto de resultados de un único procedimiento y dos columnas adicionales, OVERLOAD y ORDINAL_POSITION. OVERLOAD es la columna OVERLOAD de la tabla ALL_ARGUMENTS de la vista Diccionario de datos de Oracle. ORDINAL_POSITION es la columna SEQUENCE de la tabla ALL_ARGUMENTS de la vista Diccionario de datos de Oracle. Para los procedimientos empaquetados, la columna PROCEDURE NAME está en formato *packagename.procedurename.* No devuelve las columnas de procedimiento de un sinónimo creado que hace referencia a un procedimiento o función.|  
|**SQLProcedures**|Devuelve una lista de procedimientos en el origen de datos. Para los procedimientos empaquetados, la columna PROCEDURE NAME está en formato *packagename.procedurename.*<br /><br /> Dado que Oracle no proporciona una manera de distinguir los procedimientos empaquetados de las funciones empaquetadas, el controlador devuelve SQL_PT_UNKNOWN para la columna PROCEDURE_TYPE.|  
|**SQLSetPos**|Establece la posición del cursor en un conjunto de filas. Puede usar **SQLSetPos** con **SQLGetData** para recuperar filas de columnas sin enlazar después de colocar el cursor en una fila específica del conjunto de filas. Las filas agregadas al conjunto de resultados mediante *fOption* SQL_ADD se agregan después de la última fila del conjunto de resultados.|  
|**SQLSetScrollOptions**|Establece opciones que controlan el comportamiento de los cursores asociados a un identificador de instrucción, hstmt. Para obtener más información, vea Tipo de [cursor y Combinaciones](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)de simultaneidad .|
