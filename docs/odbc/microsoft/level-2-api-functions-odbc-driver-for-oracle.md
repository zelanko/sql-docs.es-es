---
title: Funciones de API de nivel 2 (controlador ODBC para Oracle) | Documentos de Microsoft
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
- ODBC level 2 API functions [ODBC]
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- ODBC API functions [ODBC]
- API functions [ODBC]
- level 2 API functions [ODBC]
ms.assetid: d9f49520-72d7-4234-8635-260d0ce4199c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08850dd2311d40e740a033bafb935db8d3890822
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>Funciones de API de nivel 2 (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Funciones en este nivel proporcionan funcionalidad adicional, como la compatibilidad con marcadores, los parámetros dinámicos y ejecución asincrónica de funciones ODBC además de conformidad de la interfaz de nivel 1.  
  
|Función de la API|Notas|  
|------------------|-----------|  
|**SQLBindParameter**|Asocia un búfer con un marcador de parámetro en una instrucción SQL.|  
|**SQLBrowseConnect**|Devuelve los niveles sucesivos de atributos y valores de atributo.|  
|**SQLDataSources**|Enumera los nombres de origen de datos. Implementado por el Administrador de controladores.|  
|**SQLDescribeParam**|Devuelve la descripción de un marcador de parámetro asociado con una instrucción SQL preparada.<br /><br /> Devuelve un cálculo aproximado de qué el parámetro es, basándose en el análisis de la instrucción. Si no se puede determinar el tipo de parámetro, devuelve SQL_VARCHAR con longitud 2000.|  
|**SQLDrivers**|Implementado por el Administrador de controladores.|  
|**SQLExtendedFetch**|Similar a **SQLFetch** pero devuelve varias filas utilizando una matriz para cada columna. El conjunto de resultados se puede desplazar hacia delante y puede realizarse con versiones anteriores desplazable si el cursor se define como estático, no de solo avance. Para los cursores de solo avance con enlace de columna de manera predeterminada, se recuperan datos de las columnas de conjuntos de datos mayores que el atributo de conexión BUFFERSIZE directamente en los búferes de datos. No es compatible con marcadores de longitud variable y no admite la obtención de un conjunto de filas en un desplazamiento (distinto de 0) de un marcador.|  
|**SQLForeignKeys**|Devuelve una lista de las claves externas en una única tabla o una lista de las claves externas de otras tablas que hacen referencia a una sola tabla.|  
|**SQLMoreResults**|Determina si hay más resultados pendientes en un identificador de instrucción, hstmt, que contiene las instrucciones SELECT, UPDATE, INSERT o DELETE y si es así, inicializa el procesamiento de esos resultados.<br /><br /> Oracle admite varios conjuntos de resultados solo de los procedimientos almacenados, al utilizar secuencias de escape {resultset...}.|  
|**SQLNativeSql**|Para obtener información sobre el uso, consulte [devolver los parámetros de matriz de procedimientos almacenados](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLNumParams**|Devuelve el número de parámetros en una instrucción SQL. El número de parámetros debe ser igual al número de signos de interrogación en la instrucción SQL que se pasa a **SQLPrepare**.|  
|**SQLPrimaryKeys**|Devuelve los nombres de columna que componen la clave principal de una tabla.|  
|**SQLProcedureColumns**|Devuelve una lista de entrada y parámetros de salida, el valor devuelto, las columnas del conjunto de resultados de un único procedimiento y dos columnas adicionales, sobrecarga y ORDINAL_POSITION. SOBRECARGA es la columna de la sobrecarga de la tabla ALL_ARGUMENTS de la vista de diccionario de datos de Oracle. ORDINAL_POSITION es la columna de secuencia de la tabla ALL_ARGUMENTS de la vista de diccionario de datos de Oracle. Para ver los procedimientos empaquetados, es la columna de nombre del procedimiento en *packagename.procedurename* formato. No se devuelven las columnas de procedimiento de un sinónimo creado que hace referencia a un procedimiento o función.|  
|**SQLProcedures**|Devuelve una lista de procedimientos en el origen de datos. Para ver los procedimientos empaquetados, es la columna de nombre del procedimiento en *packagename.procedurename* formato.<br /><br /> Dado que Oracle no proporciona una manera de distinguir procedimientos empaquetados de funciones empaquetadas, el controlador devuelve SQL_PT_UNKNOWN para la columna PROCEDURE_TYPE.|  
|**SQLSetPos**|Establece la posición del cursor en un conjunto de filas. Puede usar **SQLSetPos** con **SQLGetData** para recuperar filas de columnas sin enlazar después de colocar el cursor a una fila específica en el conjunto de filas. Filas agregadas en el conjunto de resultados mediante *fOption* SQL_ADD se agregan después de la última fila del conjunto de resultados.|  
|**SQLSetScrollOptions**|Establece las opciones que controlan el comportamiento de los cursores asociado con un identificador de instrucción, hstmt. Para obtener más información, consulte [combinaciones de simultaneidad y el tipo de Cursor](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|
