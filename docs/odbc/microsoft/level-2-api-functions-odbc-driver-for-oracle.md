---
title: Funciones de API de nivel 2 (controlador ODBC para Oracle) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be472a4a99324927128514fa9f8cbf19d44d49cc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825909"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>Funciones de API de nivel 2 (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 Las funciones en este nivel proporcionan una funcionalidad adicional como la compatibilidad con marcadores de parámetros dinámicos y ejecución asincrónica de las funciones ODBC además de cumplimiento de la interfaz de nivel 1.  
  
|Función de la API|Notas|  
|------------------|-----------|  
|**SQLBindParameter**|Asocia un búfer con un marcador de parámetro en una instrucción SQL.|  
|**SQLBrowseConnect**|Devuelve los niveles sucesivos de atributos y valores de atributo.|  
|**SQLDataSources**|Enumera los nombres de origen de datos. Implementado por el Administrador de controladores.|  
|**SQLDescribeParam**|Devuelve la descripción de un marcador de parámetro asociado con una instrucción SQL preparada.<br /><br /> Devuelve un cálculo aproximado de lo que el parámetro es, en función del análisis de la instrucción. Si no se puede determinar el tipo de parámetro, devuelve SQL_VARCHAR con longitud 2000.|  
|**SQLDrivers**|Implementado por el Administrador de controladores.|  
|**SQLExtendedFetch**|Similar a **SQLFetch** pero devuelve varias filas utilizando una matriz para cada columna. El conjunto de resultados es desplazable de avance y se puede realizar con versiones anteriores desplazable si el cursor se define como estático, no sólo hacia delante. Para los cursores de solo avance con enlace de columna predeterminado, se capturan datos de la columna de conjuntos de datos mayores que el atributo de conexión BUFFERSIZE directamente en los búferes de datos. No admite marcadores de longitud variable y no se admite la obtención de un conjunto de filas con un desplazamiento (distinto de 0) de un marcador.|  
|**SQLForeignKeys**|Devuelve una lista de claves externas en una sola tabla o una lista de las claves externas de otras tablas que hacen referencia a una sola tabla.|  
|**SQLMoreResults**|Determina si más resultados están pendientes en un identificador de instrucción hstmt, que contiene las instrucciones SELECT, UPDATE, INSERT o DELETE y si es así, inicializa el procesamiento de esos resultados.<br /><br /> Oracle admite varios conjuntos de resultados solo de los procedimientos almacenados, al utilizar secuencias de escape {resultset...}.|  
|**SQLNativeSql**|Para obtener información sobre el uso, consulte [devolver los parámetros de matriz de los procedimientos almacenados](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLNumParams**|Devuelve el número de parámetros en una instrucción SQL. El número de parámetros debe igual al número de signos de interrogación en la instrucción SQL que se pasa a **SQLPrepare**.|  
|**SQLPrimaryKeys**|Devuelve los nombres de columna que componen la clave principal de una tabla.|  
|**SQLProcedureColumns**|Devuelve una lista de entrada y los parámetros de salida, el valor devuelto, las columnas del conjunto de resultados de un procedimiento único y dos columnas adicionales, sobrecarga y ORDINAL_POSITION. SOBRECARGA es la columna de la sobrecarga de la tabla ALL_ARGUMENTS de la vista de diccionario de datos de Oracle. ORDINAL_POSITION es la columna de secuencia de la tabla ALL_ARGUMENTS de la vista de diccionario de datos de Oracle. Para los procedimientos empaquetados, la columna de nombre de procedimiento está en *packagename.procedurename* formato. No se devuelven las columnas de procedimiento de un sinónimo creado que hace referencia a un procedimiento o función.|  
|**SQLProcedures**|Devuelve una lista de procedimientos en el origen de datos. Para los procedimientos empaquetados, la columna de nombre de procedimiento está en *packagename.procedurename* formato.<br /><br /> Dado que Oracle no proporciona una manera de distinguir los procedimientos empaquetados de funciones empaquetadas, el controlador devuelve SQL_PT_UNKNOWN para la columna PROCEDURE_TYPE.|  
|**SQLSetPos**|Establece la posición del cursor en un conjunto de filas. Puede usar **SQLSetPos** con **SQLGetData** para recuperar filas de las columnas sin enlazar después de colocar el cursor a una fila específica en el conjunto de filas. Filas agregadas para el conjunto de resultados mediante *fOption* SQL_ADD se agregan después de la última fila del conjunto de resultados.|  
|**SQLSetScrollOptions**|Establece las opciones que controlan el comportamiento de los cursores asociado con un identificador de instrucción hstmt. Para obtener más información, consulte [tipo de Cursor y combinaciones de simultaneidad](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|
