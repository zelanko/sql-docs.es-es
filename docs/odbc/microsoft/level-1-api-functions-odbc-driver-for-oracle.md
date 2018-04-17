---
title: Funciones de API de nivel 1 (controlador ODBC para Oracle) | Documentos de Microsoft
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
ms.topic: article
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca3209029a1ac82e469c93299ecd284db44d8f4a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>Funciones de API de nivel 1 (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Admite las funciones en este nivel proporcionar conformidad de interfaz de núcleo más funcionalidad adicional, como transacciones.  
  
|Función de la API|Notas|  
|------------------|-----------|  
|**SQLColumns**|Crea un conjunto de resultados de una tabla, que es la lista de columnas para la tabla especificada o tablas. Cuando se piden columnas para un sinónimo público, debe tener establecido el atributo de conexión SYNONYMCOLUMNS y especificado una cadena vacía como el *szTableOwner* argumento. Cuando se devuelven columnas para PUBLIC synonyms, el controlador establece la columna de nombre de la tabla en una cadena vacía. El conjunto de resultados contiene una columna adicional, la posición ORDINAL, al final de cada fila. Este valor es la posición ordinal de la columna en la tabla.|  
|**SQLDriverConnect**|Se conecta a un origen de datos existente. Para obtener más información, consulte [formato de cadena de conexión y los atributos](../../odbc/microsoft/connection-string-format-and-attributes.md).|  
|**SQLGetConnectOption**|Devuelve el valor actual de una opción de conexión. Esta función se admite parcialmente. El controlador es compatible con todos los valores para la *fOption* argumento pero no es compatible con algunos *vParam* los valores para la *fOption* argumento [SQL_TXN_ISOLATION ](../../odbc/microsoft/connect-options.md). Para obtener más información, consulte [las opciones de conexión](../../odbc/microsoft/connect-options.md).|  
|**SQLGetData**|Recupera el valor de un único campo en el registro actual del conjunto de resultados determinado.|  
|**SQLGetFunctions**|Devuelve TRUE para todas las funciones compatibles. Implementado por el Administrador de controladores.|  
|**SQLGetInfo**|Devuelve información, incluidos SQLHDBC, SQLUSMALLINT, SQLPOINTER, SQLSMALLINT y SQLSMALLINT \*, sobre el controlador ODBC para Oracle y origen de datos asociado con un identificador de conexión, *hdbc*.|  
|**SQLGetStmtOption**|Devuelve el valor actual de una opción de instrucción. Para obtener más información, consulte [opciones de la instrucción](../../odbc/microsoft/statement-options.md).|  
|**SQLGetTypeInfo**|Devuelve información acerca de los tipos de datos admitidos por un origen de datos. El controlador devuelve la información en un conjunto de resultados SQL.|  
|**SQLParamData**|Usar junto con **SQLPutData** para especificar los datos de parámetro en tiempo de ejecución de la instrucción.|  
|**SQLPutData**|Permite que una aplicación enviar los datos para un parámetro o una columna para el controlador en tiempo de ejecución de la instrucción.|  
|**SQLSetConnectOption**|Proporciona acceso a las opciones que controlan aspectos de la conexión. Esta función se admite parcialmente: el controlador es compatible con todos los valores para la *fOption* argumento pero no es compatible con algunos *vParam* los valores para la *fOption* argumento [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). Para obtener más información, consulte [las opciones de conexión](../../odbc/microsoft/connect-options.md).|  
|**SQLSetStmtOption**|Establece opciones relacionadas con un identificador de instrucción, *hstmt*. Para obtener más información, consulte [opciones de la instrucción](../../odbc/microsoft/statement-options.md).|  
|**SQLSpecialColumns**|Recupera el conjunto óptimo de columnas que identifica de forma única una fila de la tabla.|  
|**SQLStatistics**|Recupera una lista de las estadísticas sobre una sola tabla y los índices o los nombres de etiqueta, asociados a la tabla. El controlador devuelve la información como un conjunto de resultados.|  
|**SQLTables**|Devuelve la lista de nombres de tabla especificado por el parámetro en el **SQLTables** instrucción. Si no se especifica ningún parámetro, devuelve los nombres de tabla que se almacenan en el origen de datos actual. El controlador devuelve la información como un conjunto de resultados.<br /><br /> Llamadas de tipo de enumeración no reciben una entrada de conjunto de resultados para las vistas remotas ni vistas con parámetros locales. Sin embargo, una llamada a **SQLTables** con una tabla única especificador de nombre encuentra ninguna coincidencia para esta vista, si está presente, con ese nombre, lo que permite la API para comprobar si hay conflictos de nombre antes de la creación de una nueva tabla.<br /><br /> Sinónimos públicos se devuelven con un valor TABLE_OWNER de "".<br /><br /> VISTAS que pertenecen a SYS o el sistema se identifican como vista del sistema.|
