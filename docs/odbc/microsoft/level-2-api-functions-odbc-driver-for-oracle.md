---
title: Funciones de la API de nivel 2 (controlador ODBC para Oracle) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284185"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>Funciones de API de nivel 2 (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Las funciones en este nivel proporcionan el cumplimiento de la interfaz de nivel 1 más funcionalidad adicional, como la compatibilidad con marcadores, parámetros dinámicos y la ejecución asincrónica de funciones ODBC.  
  
|Función de API|Notas|  
|------------------|-----------|  
|**SQLBindParameter**|Asocia un búfer a un marcador de parámetro en una instrucción SQL.|  
|**SQLBrowseConnect**|Devuelve los niveles sucesivos de atributos y valores de atributo.|  
|**SQLDataSources**|Muestra los nombres de los orígenes de datos. Implementado por el administrador de controladores.|  
|**SQLDescribeParam**|Devuelve la descripción de un marcador de parámetro asociado a una instrucción SQL preparada.<br /><br /> Devuelve una mejor aproximación de lo que es el parámetro, en función del análisis de la instrucción. Si no se puede determinar el tipo de parámetro, SQL_VARCHAR devuelve con la longitud 2000.|  
|**SQLDrivers**|Implementado por el administrador de controladores.|  
|**SQLExtendedFetch**|Similar a **SQLFetch** pero devuelve varias filas utilizando una matriz para cada columna. El conjunto de resultados es desplazable hacia delante y se puede desplazar hacia atrás si el cursor se define como estático, no solo hacia delante. En el caso de los cursores de solo avance con enlace de columna predeterminado, los datos de columna de conjuntos de datos mayores que el atributo de conexión BUFFERSIZE se capturan directamente en los búferes de datos. No admite marcadores de longitud variable y no admite la captura de un conjunto de filas en un desplazamiento (distinto de 0) de un marcador.|  
|**SQLForeignKeys**|Devuelve una lista de claves externas en una sola tabla o una lista de claves externas de otras tablas que hacen referencia a una sola tabla.|  
|**SQLMoreResults**|Determina si hay más resultados pendientes en un identificador de instrucción, hstmt, que contiene las instrucciones SELECT, UPDATE, INSERT o DELETE, y si es así, inicializa el procesamiento de esos resultados.<br /><br /> Oracle solo admite varios conjuntos de resultados de procedimientos almacenados, cuando se usan secuencias de escape {ResultSet...}.|  
|**SQLNativeSql**|Para obtener información sobre el uso, vea [devolver parámetros de matriz a partir de procedimientos almacenados](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLNumParams**|Devuelve el número de parámetros de una instrucción SQL. El número de parámetros debe ser igual al número de signos de interrogación en la instrucción SQL que se pasa a **SQLPrepare**.|  
|**SQLPrimaryKeys**|Devuelve los nombres de columna que componen la clave principal de una tabla.|  
|**SQLProcedureColumns**|Devuelve una lista de parámetros de entrada y salida, el valor devuelto, las columnas del conjunto de resultados de un único procedimiento y dos columnas adicionales, OVERLOAD y ORDINAL_POSITION. OVERLOAD es la columna de sobrecarga de la tabla ALL_ARGUMENTS de la vista del Diccionario de datos de Oracle. ORDINAL_POSITION es la columna SEQUENCE de la tabla ALL_ARGUMENTS de la vista del Diccionario de datos de Oracle. En el caso de los procedimientos empaquetados, la columna Nombre del procedimiento está en formato *packagename. nombreprocedimiento* . No devuelve las columnas de procedimiento de un sinónimo creado que hace referencia a un procedimiento o función.|  
|**SQLProcedures**|Devuelve una lista de procedimientos en el origen de datos. En el caso de los procedimientos empaquetados, la columna Nombre del procedimiento está en formato *packagename. nombreprocedimiento* .<br /><br /> Dado que Oracle no proporciona una manera de distinguir los procedimientos empaquetados de las funciones empaquetadas, el controlador devuelve SQL_PT_UNKNOWN para la columna PROCEDURE_TYPE.|  
|**SQLSetPos**|Establece la posición del cursor en un conjunto de filas. Puede usar **SQLSetPos** con **SQLGetData** para recuperar filas de columnas sin enlazar después de colocar el cursor en una fila específica del conjunto de filas. Las filas agregadas al conjunto de resultados mediante *fOption* SQL_ADD se agregan después de la última fila del conjunto de resultados.|  
|**SQLSetScrollOptions**|Establece las opciones que controlan el comportamiento de los cursores asociados a un identificador de instrucción, hstmt. Para obtener más información, vea [tipos de cursor y combinaciones de simultaneidad](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|
