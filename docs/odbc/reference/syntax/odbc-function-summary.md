---
title: Resumen de funciones ODBC | Documentos de Microsoft
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
- functions [ODBC], listed by task
ms.assetid: 7aa635da-e6b7-439f-8e9b-c3860e24de5e
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc994a3e3ec3e0e41a7b18958c013f1876f38c86
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32921850"
---
# <a name="odbc-function-summary"></a>Resumen de funciones ODBC
En la tabla siguiente se enumera las funciones ODBC, agrupadas por tipo de tarea e incluye la designación de conformidad y una breve descripción de la finalidad de cada función. Para obtener más información acerca de las designaciones de conformidad, vea [ODBC y la CLI estándar](../../../odbc/reference/odbc-and-the-standard-cli.md). Para obtener más información sobre la sintaxis y semántica para cada función, consulte [referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Una aplicación puede llamar a la **SQLGetInfo** función para obtener información de conformidad acerca de un controlador. Para obtener información sobre la compatibilidad con una función específica en un controlador, una aplicación puede llamar a **SQLGetFunctions**.  
  
|Tarea|Nombre de función|Conformidad|Finalidad|  
|----------|-------------------|-----------------|-------------|  
|Conectar a un origen de datos|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|ISO 92|Obtiene un identificador de entorno, conexión, instrucción o descriptor.|  
||[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|ISO 92|Se conecta a un controlador específico por nombre de origen de datos, Id. de usuario y contraseña.|  
||[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|ODBC|Se conecta a un controlador específico por la cadena de conexión o las solicitudes que el Administrador de controladores y el controlador mostrar cuadros de diálogo de conexión para el usuario.|  
||[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|ODBC|Devuelve los niveles sucesivos de atributos de conexión y valores de atributo válido. Cuando se ha especificado un valor para cada atributo de conexión, se conecta al origen de datos.|  
|Obtener información acerca de un controlador y un origen de datos|[SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)<br /><br /> [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|ISO 92<br /><br /> ODBC|Devuelve la lista de orígenes de datos disponibles.<br /><br /> Devuelve la lista de controladores instalados y sus atributos.|  
||[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|ISO 92|Devuelve información sobre un origen de datos y el controlador específico.|  
||[SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)|ISO 92|Devuelve admite las funciones del controlador.|  
||[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|ISO 92|Devuelve información acerca de los tipos de datos admitidos.|  
|Establecer y recuperar atributos de controladores|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)<br /><br /> [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|ISO 92<br /><br /> ISO 92|Establece un atributo de conexión.<br /><br /> Devuelve el valor de un atributo de conexión.|  
||[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|ISO 92|Establece un atributo de entorno.|  
||[SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|ISO 92|Devuelve el valor de un atributo de entorno.|  
||[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|ISO 92|Establece un atributo de instrucción.|  
||[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|ISO 92|Devuelve el valor de un atributo de instrucción.|  
|Establecer y recuperar los campos de descriptor|[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)<br /><br /> [SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|ISO 92<br /><br /> ISO 92|Devuelve el valor de un campo único descriptor.<br /><br /> Devuelve los valores de varios campos de descriptor.|  
||[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|ISO 92|Establece un campo único descriptor.|  
||[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|ISO 92|Establece varios campos de descriptor.|  
||[SQLCopyDesc](../../../odbc/reference/syntax/sqlcopydesc-function.md)|ISO 92|Copia información del descriptor de identificador de descriptor de uno a otro.|  
|Solicitudes de preparación de SQL|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|ISO 92|Prepara una instrucción SQL para su ejecución posterior.|  
||[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|ODBC|Asigna almacenamiento para un parámetro en una instrucción SQL.|  
||[SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|ISO 92|Devuelve el nombre de cursor asociado con un identificador de instrucción.|  
||[SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|ISO 92|Especifica un nombre de cursor.|  
||[SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|ODBC|Establece las opciones que controlan el comportamiento del cursor.|  
|Envío de solicitudes|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)<br /><br /> [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|ISO 92<br /><br /> ISO 92|Ejecuta una instrucción preparada.<br /><br /> Ejecuta una instrucción.|  
||[SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)|ODBC|Devuelve el texto de una instrucción SQL traducida por el controlador.|  
||[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|ODBC|Devuelve la descripción para un parámetro concreto en una instrucción.|  
||[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|ISO 92|Devuelve el número de parámetros en una instrucción.|  
||[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|ISO 92|Usar junto con **SQLPutData** para proporcionar datos de parámetro en tiempo de ejecución. (Útil para los valores de datos de tipo long).|  
||[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|ISO 92|Envía parte o la totalidad de un valor de datos para un parámetro. (Útil para los valores de datos de tipo long).|  
|Recuperar información acerca de los resultados y resultados|[SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)<br /><br /> [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|ISO 92<br /><br /> ISO 92|Devuelve el número de filas afectadas por la inserción, actualización o solicitud de eliminación.<br /><br /> Devuelve el número de columnas del conjunto de resultados.|  
||[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|ISO 92|Describe una columna del conjunto de resultados.|  
||[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|ISO 92|Describe los atributos de una columna del conjunto de resultados.|  
||[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|ISO 92|Asigna almacenamiento para una columna de resultados y especifica el tipo de datos.|  
||[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|ISO 92|Devuelve varias filas de resultados.|  
||[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|ISO 92|Devuelve las filas de resultados desplazables.|  
||[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|ISO 92|Devuelve parte o la totalidad de una columna de una fila de un resultado de conjunto. (Útil para los valores de datos de tipo long).|  
||[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|ODBC|Coloca un cursor dentro de un bloque de datos capturado y permite que una aplicación para actualizar los datos del conjunto de filas o actualizar o eliminar datos en el conjunto de resultados.|  
||[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|ODBC|Realiza inserciones masivas y marcador de forma masiva las operaciones, incluida la actualización, eliminar y capturar por marcador.|  
||[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|ODBC|Determina si hay más resultados disponibles conjuntos y, si es así, inicializa el procesamiento del siguiente conjunto de resultados.|  
||[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|ISO 92|Devuelve información de diagnóstico adicional (un único campo de la estructura de datos de diagnóstico).|  
||[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|ISO 92|Devuelve información de diagnóstico adicional (varios campos de la estructura de datos de diagnóstico).|  
|Obtener información acerca de las tablas del origen de datos del sistema (funciones de catálogo)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)<br /><br /> [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|ODBC<br /><br /> Abrir grupo|Devuelve una lista de columnas y los privilegios asociados para una o varias tablas.<br /><br /> Devuelve la lista de nombres de columna en las tablas especificadas.|  
||[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|ODBC|Devuelve una lista de nombres de las columnas que componen las claves externas, si existen para una tabla especificada.|  
||[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|ODBC|Devuelve la lista de nombres de las columnas que componen la clave principal de una tabla.|  
||[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|ODBC|Devuelve la lista de entrada y parámetros de salida, así como las columnas que componen el conjunto de resultados de los procedimientos especificados.|  
||[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|ODBC|Devuelve la lista de nombres de procedimientos almacenados en un origen de datos específico.|  
||[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|Abrir grupo|Devuelve información sobre el conjunto óptimo de columnas que identifica de forma única una fila de una tabla especificada o las columnas que se actualizan automáticamente cuando una transacción actualiza cualquier valor de la fila.|  
||[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|ISO 92|Devuelve estadísticas sobre una sola tabla y la lista de índices asociados a la tabla.|  
||[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|ODBC|Devuelve una lista de tablas y los privilegios asociados con cada tabla.|  
||[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|Abrir grupo|Devuelve la lista de nombres de tabla almacenada en un origen de datos específico.|  
|Terminar una instrucción|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|ISO 92|Finaliza el procesamiento de la instrucción, descarta los resultados pendientes y, opcionalmente, libera todos los recursos asociados con el identificador de instrucción.|  
||[SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|ISO 92|Cierra un cursor que se ha abierto en un identificador de instrucción.|  
||[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|ISO 92|Cancela el procesamiento en una instrucción.|  
||[SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|ODBC|Cancela el procesamiento en una instrucción o la conexión.|  
||[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|ISO 92|Confirma o revierte una transacción.|  
|Terminar una conexión|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|ISO 92<br /><br /> ISO 92|Cierra la conexión.<br /><br /> Libera un identificador de entorno, conexión, instrucción o descriptor.|
