---
title: Capturar datos de resultados | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-results
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLFetchScroll function
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], fetching
- SQLBindCol function
- result sets [ODBC], fetching
- fetching [ODBC]
- ODBC data types, fetching
- SQLFetch function
- SQL Server Native Client ODBC driver, data types
- SQLGetData function
ms.assetid: b289c7fb-5017-4d7e-a2d3-19401e9fc4cd
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8f1c828f3e63e3167a0685f450e318055a9b71fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="fetching-result-data"></a>Capturar datos de resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Una aplicación ODBC tiene tres opciones para capturar los datos de resultados.  
  
 La primera opción se basa en [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md). Antes de capturar el resultado establecido, la aplicación usa **SQLBindCol** para enlazar cada columna en el conjunto de resultados a una variable de programa. Después de las columnas se han enlazado, el controlador transfiere los datos de la fila actual a las variables que se enlazarán a las columnas del conjunto de resultados cada vez la aplicación llama **SQLFetch** o [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). El controlador administra las conversiones de datos si la columna de conjunto de resultados y la variable de programa tienen tipos de datos distintos. Si la aplicación tiene SQL_ATTR_ROW_ARRAY_SIZE establece mayor que 1, se pueden enlazar las columnas de resultados a las matrices de variables, que se llenarán todas en cada llamada a **SQLFetchScroll**.  
  
 La segunda opción se basa en [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). La aplicación no usa **SQLBindCol** enlazar el resultado de establece las columnas a variables de programa. Después de cada llamada a **SQLFetch**, la aplicación llama **SQLGetData** una vez para cada columna en el resultado de establecer. **SQLGetData** indica al controlador que transfiera los datos de una columna del conjunto de resultados específico a una variable de programa específico y especifica los tipos de datos de la columna y la variable. Esto permite al controlador convertir los datos si la columna de resultado y la variable de programa tienen tipos de datos distintos. **Texto**, **ntext**, y **imagen** columnas normalmente son demasiado grandes para caber en una variable de programa pero todavía se puede recuperar mediante **SQLGetData**. Si el **texto**, **ntext**, o **imagen** datos en la columna de resultados es mayor que la variable de programa, **SQLGetData** devuelve SQL_SUCCESS_ WITH_INFO y SQLSTATE 01004 (datos de cadena, truncados por la derecha). Las llamadas sucesivas a **SQLGetData** devuelven los fragmentos sucesivos de la **texto** o **imagen** datos. Cuando se alcanza el final de los datos, **SQLGetData** devuelve SQL_SUCCESS. Cada captura devuelve un conjunto de filas, si SQL_ATTR_ROW_ARRAY_SIZE es mayor que 1. Antes de usar **SQLGetData**, primero debe usar **SQLSetPos** para especificar una fila específica en el conjunto de filas como la fila actual.  
  
 La tercera opción consiste en utilizar una combinación de **SQLBindCol** y **SQLGetData**. Una aplicación podría, por ejemplo, enlazar las diez primeras columnas de un conjunto de resultados y, a continuación, en cada captura, llame a **SQLGetData** tres veces para recuperar los datos de tres columnas independientes. Esto lo que normalmente se utiliza cuando un conjunto de resultados contiene uno o varios **texto** o **imagen** columnas.  
  
 Según las opciones de cursor establecidas para el conjunto de resultados, una aplicación también puede utilizar las opciones de desplazamiento de **SQLFetchScroll** para desplazarse por el conjunto de resultados.  
  
 El uso excesivo de **SQLBindCol** para enlazar un resultado de conjunto de columnas a una variable de programa es caro porque **SQLBindCol** hace que un controlador ODBC asignar memoria. Al enlazar una columna de resultados a una variable, ese enlace permanece en vigor hasta que llame a [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para liberar el identificador de instrucción o llamada [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con *fOption* establecido en SQL_UNBIND. Los enlaces no se deshacen automáticamente cuando se completa la instrucción.  
  
 Esta lógica le permite solucionar eficazmente la ejecución de la misma instrucción SELECT varias veces con parámetros diferentes. Dado que el conjunto de resultados mantiene la misma estructura, puede enlazar una vez el conjunto de resultados, procesar todas las instrucciones SELECT y, a continuación, llame a **SQLFreeStmt** con *fOption* establecido en SQL_UNBIND después de la última ejecución. No debería llamar a **SQLBindCol** para enlazar las columnas de un conjunto de resultados sin antes de llamar a **SQLFreeStmt** con *fOption* establecido en SQL_UNBIND para liberar cualquier enlace anterior.  
  
 Cuando se usa **SQLBindCol**, puede hacer un modo de fila o enlace. El enlace de modo de fila es algo más rápido que el enlace de modo de columna.  
  
 Puede usar **SQLGetData** para recuperar datos según una columna por columna en lugar de enlazar el resultado conjunto de columnas mediante **SQLBindCol**. Si un conjunto de resultados contiene solamente algunas filas, utilizando **SQLGetData** en lugar de **SQLBindCol** es más rápido; en caso contrario, **SQLBindCol** proporciona el máximo rendimiento. Si no siempre coloca los datos en el mismo conjunto de variables, debe usar **SQLGetData** en lugar de volver a enlazar constantemente. Solo se puede usar **SQLGetData** en columnas que se encuentran en la lista de selección después de que todas las columnas se enlazan con **SQLBindCol**. La columna debe aparecer también después de las columnas en el que ya ha usado **SQLGetData**.  
  
 Las funciones ODBC que solucionan mover datos hacia o desde variables de programa, como **SQLGetData**, **SQLBindCol**, y [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), admiten tipos de datos implícitas conversión. Por ejemplo, si una aplicación enlaza una columna entera a una variable de programa de cadena de caracteres, el controlador convierte automáticamente los datos enteros en caracteres antes de incluirlos en la variable de programa.  
  
 Se debe minimizar la conversión de los datos en las aplicaciones. A menos que se requiera la conversión de datos para el procesamiento realizado por la aplicación, las aplicaciones deben enlazar las columnas y los parámetros a las variables de programa del mismo tipo de datos. Si los datos se deben convertir de un tipo a otro, sin embargo, es más eficaz hacer que el controlador haga la conversión que hacerla en la aplicación. El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client normalmente solo transfiere directamente los datos desde los búferes de la red a las variables de la aplicación. La solicitud al controlador de realizar la conversión de datos fuerza al controlador a almacenar en búfer los datos y usar los ciclos de CPU para convertir los datos.  
  
 Deben ser lo suficientemente grandes como para contener los datos transferidos desde una columna, excepto para las variables de programa **texto**, **ntext**, y **imagen** datos. Si una aplicación intenta recuperar datos del conjunto de resultados y colocarlos en una variable que es demasiado pequeña para contenerlos, el controlador genera una advertencia. Esto obliga al controlador a asignar memoria para el mensaje y los dos, el controlador y la aplicación, tienen que utilizar ciclos de CPU para procesar el mensaje y realizar el tratamiento de errores. La aplicación debe asignar una variable bastante grande para contener los datos que se van a recuperar o usar la función SUBSTRING de la lista de selección para reducir el tamaño de la columna del conjunto de resultados.  
  
 Se deben extremar las precauciones al utilizar SQL_C_DEFAULT para especificar el tipo de la variable C. SQL_C_DEFAULT especifica que el tipo de la variable C coincide con el tipo de datos SQL de la columna o parámetro. Si se especifica SQL_C_DEFAULT para un **ntext**, **nchar**, o **nvarchar** columna, se devuelven datos Unicode a la aplicación. Esto puede producir varios problemas si la aplicación no ha estado codificada para administrar los datos Unicode. Los mismos tipos de problemas pueden producirse con la **uniqueidentifier** tipo de datos (SQL_GUID).  
  
 **texto**, **ntext**, y **imagen** datos normalmente es demasiado grandes para caber en una sola variable de programa y normalmente se procesan con **SQLGetData** en lugar de **SQLBindCol**. Cuando se utilizan cursores de servidor, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client está optimizado para no transmitir los datos sin delimitar **texto**, **ntext**, o **imagen** columnas en la tiempo que se recopila la fila. El **texto**, **ntext**, o **imagen** datos no se recuperan realmente desde el servidor hasta que los problemas de aplicaciones **SQLGetData** para la columna.  
  
 Esta optimización se puede aplicar a las aplicaciones para que no **texto**, **ntext**, o **imagen** se muestran los datos mientras un usuario se desplaza arriba y abajo un cursor. Cuando el usuario selecciona una fila, la aplicación puede llamar a **SQLGetData** para recuperar la **texto**, **ntext**, o **imagen** datos. Esto ahorra la transmisión del **texto**, **ntext**, o **imagen** datos para cualquiera de las filas que el usuario no selecciona y puede ahorrar la transmisión de grandes cantidades de datos.  
  
## <a name="see-also"></a>Vea también  
 [Procesar resultados &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
