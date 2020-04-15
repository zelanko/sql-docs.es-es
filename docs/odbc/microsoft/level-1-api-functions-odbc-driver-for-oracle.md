---
title: Funciones de API de nivel 1 (controlador ODBC para Oracle) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37305ee75ebeb0686bafe039f1102cb3c6e18674
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299955"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>Funciones de API de nivel 1 (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Las funciones de este nivel proporcionan conformidad de interfaz principal, además de funcionalidad adicional, como la compatibilidad con transacciones.  
  
|Función API|Notas|  
|------------------|-----------|  
|**SQLColumns**|Crea un conjunto de resultados para una tabla, que es la lista de columnas para la tabla o tablas especificadas. Al solicitar columnas para un sinónimo PUBLIC, debe haber establecido el atributo de conexión SYNONYMCOLUMNS y especificado una cadena vacía como el *argumento szTableOwner.* Al devolver columnas para sinónimos PUBLIC, el controlador establece la columna NOMBRE DE TABLA en una cadena vacía. El conjunto de resultados contiene una columna adicional, ORDINAL POSITION, al final de cada fila. Este valor es la posición ordinal de la columna de la tabla.|  
|**SQLDriverConnect**|Se conecta a un origen de datos existente. Para obtener más información, consulte [Formato y atributos](../../odbc/microsoft/connection-string-format-and-attributes.md)de cadena de conexión .|  
|**SQLGetConnectOption**|Devuelve la configuración actual de una opción de conexión. Esta función es parcialmente compatible. El controlador admite todos los valores para el *fOption* argumento pero no admite algunos *vParam* valores para el *fOption* argumento [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). Para obtener más información, consulte [Opciones de conexión](../../odbc/microsoft/connect-options.md).|  
|**SQLGetData**|Recupera el valor de un único campo en el registro actual del conjunto de resultados especificado.|  
|**SQLGetFunctions**|Devuelve TRUE para todas las funciones admitidas. Implementado por el Administrador de controladores.|  
|**SQLGetInfo**|Devuelve información, incluidos SQLHDBC, SQLUSMALLINT, SQLPOINTER, SQLSMALLINT \*y SQLSMALLINT , sobre el controlador ODBC para Oracle y el origen de datos asociado a un identificador de conexión, *hdbc*.|  
|**SQLGetStmtOption**|Devuelve la configuración actual de una opción de instrucción. Para obtener más información, consulte Opciones de [instrucción](../../odbc/microsoft/statement-options.md).|  
|**SQLGetTypeInfo**|Devuelve información sobre los tipos de datos admitidos por un origen de datos. El controlador devuelve la información de un conjunto de resultados SQL.|  
|**SQLParamData**|Se utiliza junto con **SQLPutData** para especificar datos de parámetro en tiempo de ejecución de instrucciones.|  
|**SQLPutData**|Permite que una aplicación envíe datos de un parámetro o columna al controlador en tiempo de ejecución de la instrucción.|  
|**SQLSetConnectOption**|Proporciona acceso a opciones que rigen los aspectos de la conexión. Esta función se admite parcialmente: el controlador admite todos los valores para el argumento *fOption,* pero no admite algunos valores *vParam* para el argumento *fOption* [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). Para obtener más información, consulte [Opciones de conexión](../../odbc/microsoft/connect-options.md).|  
|**SQLSetStmtOption**|Establece las opciones relacionadas con un identificador de instrucción, *hstmt*. Para obtener más información, consulte Opciones de [instrucción](../../odbc/microsoft/statement-options.md).|  
|**SQLSpecialColumns**|Recupera el conjunto óptimo de columnas que identifica de forma única una fila de la tabla.|  
|**SQLStatistics**|Recupera una lista de estadísticas sobre una sola tabla y los índices, o nombres de etiqueta, asociados a la tabla. El controlador devuelve la información como un conjunto de resultados.|  
|**SQLTables**|Devuelve la lista de nombres de tabla especificados por el parámetro en la instrucción **SQLTables.** Si no se especifica ningún parámetro, devuelve los nombres de tabla almacenados en el origen de datos actual. El controlador devuelve la información como un conjunto de resultados.<br /><br /> Las llamadas de tipo de enumeración no recibirán una entrada de conjunto de resultados para vistas remotas o vistas parametrizadas locales. Sin embargo, una llamada a **SQLTables** con un especificador de nombre de tabla único encontrará una coincidencia para dicha vista, si está presente, con ese nombre; esto permite que la API compruebe si hay conflictos de nombres antes de crear una nueva tabla.<br /><br /> Los sinónimos PUBLIC se devuelven con un valor TABLE_OWNER de "".<br /><br /> LAS VISTAS propiedad de SYS o SYSTEM se identifican como SYSTEM VIEW.|
