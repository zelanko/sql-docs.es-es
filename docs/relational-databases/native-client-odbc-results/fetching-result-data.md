---
title: Capturando datos de resultados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 00a3245009d7f7db437a990fdf5dc814d6b19f7d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724995"
---
# <a name="fetching-result-data"></a>Capturar datos de resultados
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Una aplicación ODBC tiene tres opciones para capturar los datos de resultados.  
  
 La primera opción se basa en [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md). Antes de obtener el conjunto de resultados, la aplicación usa **SQLBindCol** para enlazar cada columna del conjunto de resultados a una variable de programa. Una vez enlazadas las columnas, el controlador transfiere los datos de la fila actual a las variables enlazadas a las columnas del conjunto de resultados cada vez que la aplicación llama a **SQLFetch** o a [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). El controlador administra las conversiones de datos si la columna de conjunto de resultados y la variable de programa tienen tipos de datos distintos. Si la aplicación tiene SQL_ATTR_ROW_ARRAY_SIZE establecido en un valor mayor que 1, puede enlazar columnas de resultados a matrices de variables, que se rellenarán en cada llamada a **SQLFetchScroll**.  
  
 La segunda opción se basa en [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). La aplicación no usa **SQLBindCol** para enlazar columnas del conjunto de resultados a variables de programa. Después de cada llamada a **SQLFetch**, la aplicación llama a **SQLGetData** una vez para cada columna del conjunto de resultados. **SQLGetData** indica al controlador que transfiera los datos de una columna de conjunto de resultados específica a una variable de programa concreta y especifica los tipos de datos de la columna y la variable. Esto permite al controlador convertir los datos si la columna de resultado y la variable de programa tienen tipos de datos distintos. Las columnas **Text**, **ntext**e **Image** suelen ser demasiado grandes para caber en una variable de programa, pero todavía se pueden recuperar mediante **SQLGetData**. Si los datos de tipo **Text**, **ntext**o **Image** de la columna de resultados son mayores que la variable de programa, **SQLGetData** devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01004 (datos de cadena, truncados a la derecha). Las llamadas sucesivas a **SQLGetData** devuelven fragmentos sucesivos de los datos de **texto** o **imagen** . Cuando se alcanza el final de los datos, **SQLGetData** devuelve SQL_SUCCESS. Cada captura devuelve un conjunto de filas, si SQL_ATTR_ROW_ARRAY_SIZE es mayor que 1. Antes de usar **SQLGetData**, primero debe usar **SQLSetPos** para especificar una fila concreta dentro del conjunto de filas como la fila actual.  
  
 La tercera opción es usar una combinación de **SQLBindCol** y **SQLGetData**. Una aplicación podría, por ejemplo, enlazar las diez primeras columnas de un conjunto de resultados y, a continuación, en cada captura, llamar a **SQLGetData** tres veces para recuperar los datos de tres columnas sin enlazar. Normalmente se utilizaría cuando un conjunto de resultados contiene una o más columnas **Text** o **Image** .  
  
 Dependiendo de las opciones de cursor establecidas para el conjunto de resultados, una aplicación también puede usar las opciones de desplazamiento de **SQLFetchScroll** para desplazarse por el conjunto de resultados.  
  
 El uso excesivo de **SQLBindCol** para enlazar una columna de conjunto de resultados a una variable de programa es costoso porque **SQLBindCol** hace que un controlador ODBC asigne memoria. Al enlazar una columna de resultados a una variable, ese enlace permanece en vigor hasta que se llama a [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para liberar el identificador de instrucción o llamar a [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con *fOption* establecido en SQL_UNBIND. Los enlaces no se deshacen automáticamente cuando se completa la instrucción.  
  
 Esta lógica le permite solucionar eficazmente la ejecución de la misma instrucción SELECT varias veces con parámetros diferentes. Dado que el conjunto de resultados mantiene la misma estructura, puede enlazar el conjunto de resultados una vez, procesar todas las instrucciones SELECT y, a continuación, llamar a **SQLFreeStmt** con *fOption* establecido en SQL_UNBIND después de la última ejecución. No debe llamar a **SQLBindCol** para enlazar las columnas de un conjunto de resultados sin llamar primero a **SQLFreeStmt** con *fOption* establecido en SQL_UNBIND para liberar cualquier enlace anterior.  
  
 Al usar **SQLBindCol**, puede realizar un enlace de modo de fila o de modo de columna. El enlace de modo de fila es algo más rápido que el enlace de modo de columna.  
  
 Puede usar **SQLGetData** para recuperar datos columna por columna en lugar de enlazar columnas del conjunto de resultados mediante **SQLBindCol**. Si un conjunto de resultados contiene solo unas pocas filas, el uso de **SQLGetData** en lugar de **SQLBindCol** es más rápido; de lo contrario, **SQLBindCol** proporciona el mejor rendimiento. Si no coloca siempre los datos en el mismo conjunto de variables, debe utilizar **SQLGetData** en lugar de volver a enlazar constantemente. Solo puede utilizar **SQLGetData** en las columnas que se encuentran en la lista de selección después de que todas las columnas se enlacen con **SQLBindCol**. La columna también debe aparecer después de cualquier columna en la que ya haya utilizado **SQLGetData**.  
  
 Las funciones ODBC que se ocupan de mover datos hacia o desde variables de programa, como **SQLGetData**, **SQLBindCol**y [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), admiten la conversión implícita de tipos de datos. Por ejemplo, si una aplicación enlaza una columna entera a una variable de programa de cadena de caracteres, el controlador convierte automáticamente los datos enteros en caracteres antes de incluirlos en la variable de programa.  
  
 Se debe minimizar la conversión de los datos en las aplicaciones. A menos que se requiera la conversión de datos para el procesamiento realizado por la aplicación, las aplicaciones deben enlazar las columnas y los parámetros a las variables de programa del mismo tipo de datos. Si los datos se deben convertir de un tipo a otro, sin embargo, es más eficaz hacer que el controlador haga la conversión que hacerla en la aplicación. El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client normalmente solo transfiere directamente los datos desde los búferes de la red a las variables de la aplicación. La solicitud al controlador de realizar la conversión de datos fuerza al controlador a almacenar en búfer los datos y usar los ciclos de CPU para convertir los datos.  
  
 Las variables de programa deben ser lo suficientemente grandes como para contener los datos transferidos desde una columna, salvo los datos **Text**, **ntext**e **Image** . Si una aplicación intenta recuperar datos del conjunto de resultados y colocarlos en una variable que es demasiado pequeña para contenerlos, el controlador genera una advertencia. Esto obliga al controlador a asignar memoria para el mensaje y los dos, el controlador y la aplicación, tienen que utilizar ciclos de CPU para procesar el mensaje y realizar el tratamiento de errores. La aplicación debe asignar una variable bastante grande para contener los datos que se van a recuperar o usar la función SUBSTRING de la lista de selección para reducir el tamaño de la columna del conjunto de resultados.  
  
 Se deben extremar las precauciones al utilizar SQL_C_DEFAULT para especificar el tipo de la variable C. SQL_C_DEFAULT especifica que el tipo de la variable C coincide con el tipo de datos SQL de la columna o parámetro. Si se especifica SQL_C_DEFAULT para una columna **ntext**, **nchar**o **nvarchar** , los datos Unicode se devuelven a la aplicación. Esto puede producir varios problemas si la aplicación no ha estado codificada para administrar los datos Unicode. Se pueden producir los mismos tipos de problemas con el tipo de datos **uniqueidentifier** (SQL_GUID).  
  
 los datos **Text**, **ntext**e **Image** suelen ser demasiado grandes para caber en una sola variable de programa y normalmente se procesan con **SQLGetData** en lugar de **SQLBindCol**. Cuando se utilizan cursores de servidor, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client está optimizado para no transmitir los datos de las columnas **Text**, **ntext**o **Image** sin enlazar en el momento en que se captura la fila. Los datos **Text**, **ntext**o **Image** no se recuperan realmente del servidor hasta que la aplicación emite **SQLGetData** para la columna.  
  
 Esta optimización se puede aplicar a las aplicaciones para que no se muestre ningún dato **Text**, **ntext**o **Image** mientras un usuario se desplaza hacia arriba y hacia abajo un cursor. Una vez que el usuario selecciona una fila, la aplicación puede llamar a **SQLGetData** para recuperar los datos **Text**, **ntext**o **Image** . Esto guarda la transmisión de los datos **Text**, **ntext**o **Image** para cualquiera de las filas que el usuario no selecciona y puede ahorrar la transmisión de cantidades muy grandes de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Procesar los resultados &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
