---
title: Funciones de API de nivel 1 (controlador ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cb1771f88987073b1ef0bcc106f8de28549affe6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085475"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>Funciones de API de nivel 1 (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 Admite las funciones en este nivel proporcionar cumplimiento de la interfaz principal además de funcionalidad adicional, como la transacción.  
  
|Función de la API|Notas|  
|------------------|-----------|  
|**SQLColumns**|Crea un conjunto de resultados de una tabla, que es la lista de columnas de la tabla especificada o tablas. Cuando se solicita las columnas para un sinónimo público, debe tener establecido el atributo de conexión SYNONYMCOLUMNS y especificado una cadena vacía como el *szTableOwner* argumento. Cuando se devuelven las columnas para sinónimos PUBLIC, el controlador establece la columna de nombre de tabla en una cadena vacía. El conjunto de resultados contiene una columna adicional, la posición ORDINAL, al final de cada fila. Este valor es la posición ordinal de la columna en la tabla.|  
|**SQLDriverConnect**|Se conecta a un origen de datos existente. Para obtener más información, consulte [formato de cadena de conexión y los atributos](../../odbc/microsoft/connection-string-format-and-attributes.md).|  
|**SQLGetConnectOption**|Devuelve el valor actual de una opción de conexión. Esta función se admite parcialmente. El controlador es compatible con todos los valores para el *fOption* argumento pero no admite algunos *vParam* valores para el *fOption* argumento [SQL_TXN_ISOLATION ](../../odbc/microsoft/connect-options.md). Para obtener más información, consulte [las opciones de conexión](../../odbc/microsoft/connect-options.md).|  
|**SQLGetData**|Recupera el valor de un único campo en el registro actual del conjunto de resultados determinado.|  
|**SQLGetFunctions**|Devuelve TRUE para todas las funciones compatibles. Implementado por el Administrador de controladores.|  
|**SQLGetInfo**|Devuelve información, incluidos SQLHDBC SQLUSMALLINT, SQLPOINTER, SQLSMALLINT y SQLSMALLINT \*, sobre el controlador ODBC para Oracle y origen de datos asociado con un identificador de conexión, *hdbc*.|  
|**SQLGetStmtOption**|Devuelve el valor actual de una opción de instrucción. Para obtener más información, consulte [opciones de la instrucción](../../odbc/microsoft/statement-options.md).|  
|**SQLGetTypeInfo**|Devuelve información sobre los tipos de datos admitidos por un origen de datos. El controlador devuelve la información en un conjunto de resultados SQL.|  
|**SQLParamData**|Usar junto con **SQLPutData** para especificar los datos de parámetro en tiempo de ejecución de la instrucción.|  
|**SQLPutData**|Permite que una aplicación enviar datos de un parámetro o columna a del controlador en el tiempo de ejecución de la instrucción.|  
|**SQLSetConnectOption**|Proporciona acceso a las opciones que controlan aspectos de la conexión. Esta función se admite parcialmente: El controlador es compatible con todos los valores para el *fOption* argumento pero no admite algunos *vParam* valores para el *fOption* argumento [SQL_TXN_ISOLATION ](../../odbc/microsoft/connect-options.md). Para obtener más información, consulte [las opciones de conexión](../../odbc/microsoft/connect-options.md).|  
|**SQLSetStmtOption**|Establece las opciones relacionadas con un identificador de instrucción, *hstmt*. Para obtener más información, consulte [opciones de la instrucción](../../odbc/microsoft/statement-options.md).|  
|**SQLSpecialColumns**|Recupera el conjunto óptimo de columnas que identifica de forma única una fila en la tabla.|  
|**SQLStatistics**|Recupera una lista de las estadísticas sobre una sola tabla y los índices o los nombres de etiqueta, asociados a la tabla. El controlador devuelve la información como un conjunto de resultados.|  
|**SQLTables**|Devuelve la lista de nombres de tabla especificado por el parámetro en el **SQLTables** instrucción. Si se especifica ningún parámetro, devuelve los nombres de tabla que se almacenan en el origen de datos actual. El controlador devuelve la información como un conjunto de resultados.<br /><br /> Las llamadas de tipo de enumeración no reciben una entrada de conjunto de resultados para las vistas remotas ni vistas con parámetros locales. Sin embargo, una llamada a **SQLTables** con una tabla única especificador de nombre encuentre una coincidencia para esa vista, si está presente, con ese nombre; Esto permite que la API para comprobar si hay conflictos de nombre antes de crear una nueva tabla.<br /><br /> Sinónimos públicos se devuelven con un valor TABLE_OWNER "".<br /><br /> Las vistas que pertenecen a SYS o del sistema se identifican como vista del sistema.|
