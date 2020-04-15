---
title: Obtención de datos de resultados ? Microsoft Docs
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
ms.openlocfilehash: e1d9fdfcd7bcc4f86afacc75dff5b40b77bb7b2a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304623"
---
# <a name="fetching-result-data"></a>Capturar datos de resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Una aplicación ODBC tiene tres opciones para capturar los datos de resultados.  
  
 La primera opción se basa en [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md). Antes de capturar el conjunto de resultados, la aplicación utiliza **SQLBindCol** para enlazar cada columna del conjunto de resultados a una variable de programa. Una vez enlazadas las columnas, el controlador transfiere los datos de la fila actual a las variables enlazadas a las columnas del conjunto de resultados cada vez que la aplicación llama a **SQLFetch** o [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). El controlador administra las conversiones de datos si la columna de conjunto de resultados y la variable de programa tienen tipos de datos distintos. Si la aplicación tiene SQL_ATTR_ROW_ARRAY_SIZE establecido mayor que 1, puede enlazar columnas de resultados a matrices de variables, que se rellenarán en cada llamada a **SQLFetchScroll**.  
  
 La segunda opción se basa en [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). La aplicación no utiliza **SQLBindCol** para enlazar columnas de conjunto de resultados a variables de programa. Después de cada llamada a **SQLFetch**, la aplicación llama a **SQLGetData** una vez para cada columna del conjunto de resultados. **SQLGetData** indica al controlador que transfiera datos de una columna de conjunto de resultados específica a una variable de programa específica y especifica los tipos de datos de la columna y la variable. Esto permite al controlador convertir los datos si la columna de resultado y la variable de programa tienen tipos de datos distintos. **Las**columnas Text , **ntext**e **image** suelen ser demasiado grandes para caber en una variable de programa, pero todavía se pueden recuperar mediante **SQLGetData**. Si los datos **text**, **ntext**o **image** de la columna de resultados son mayores que la variable de programa, **SQLGetData** devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01004 (datos de cadena, truncados con el botón derecho). Las llamadas sucesivas a **SQLGetData** devuelven fragmentos sucesivos de los datos de **texto** o **imagen.** Cuando se alcanza el final de los datos, **SQLGetData** devuelve SQL_SUCCESS. Cada captura devuelve un conjunto de filas, si SQL_ATTR_ROW_ARRAY_SIZE es mayor que 1. Antes de usar **SQLGetData**, primero debe usar **SQLSetPos** para especificar una fila específica dentro del conjunto de filas como la fila actual.  
  
 La tercera opción es usar una combinación de **SQLBindCol** y **SQLGetData**. Una aplicación podría, por ejemplo, enlazar las primeras diez columnas de un conjunto de resultados y, a continuación, en cada captura, llamar a **SQLGetData** tres veces para recuperar los datos de tres columnas sin enlazar. Esto se usaría normalmente cuando un conjunto de resultados contiene una o más columnas de **texto** o **imagen.**  
  
 Dependiendo de las opciones de cursor establecidas para el conjunto de resultados, una aplicación también puede usar las opciones de desplazamiento de **SQLFetchScroll** para desplazarse por el conjunto de resultados.  
  
 El uso excesivo de **SQLBindCol** para enlazar una columna de conjunto de resultados a una variable de programa es costoso porque **SQLBindCol** hace que un controlador ODBC asigne memoria. Cuando se enlaza una columna de resultado a una variable, ese enlace permanece en vigor hasta que se llama a [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para liberar el identificador de instrucción o se llama a [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con *fOption* establecido en SQL_UNBIND. Los enlaces no se deshacen automáticamente cuando se completa la instrucción.  
  
 Esta lógica le permite solucionar eficazmente la ejecución de la misma instrucción SELECT varias veces con parámetros diferentes. Dado que el conjunto de resultados mantiene la misma estructura, puede enlazar el conjunto de resultados una vez, procesar todas las instrucciones SELECT y, a continuación, llamar a **SQLFreeStmt** con *fOption* establecido en SQL_UNBIND después de la última ejecución. No debe llamar a **SQLBindCol** para enlazar las columnas de un conjunto de resultados sin llamar primero a **SQLFreeStmt** con *fOption* establecido en SQL_UNBIND para liberar los enlaces anteriores.  
  
 Al usar **SQLBindCol**, puede realizar enlaces de fila o de columna. El enlace de modo de fila es algo más rápido que el enlace de modo de columna.  
  
 Puede usar **SQLGetData** para recuperar datos columna por columna en lugar de enlazar columnas de conjunto de resultados mediante **SQLBindCol**. Si un conjunto de resultados contiene solo unas pocas filas, usar **SQLGetData** en lugar de **SQLBindCol** es más rápido; de lo contrario, **SQLBindCol** ofrece el mejor rendimiento. Si no siempre coloca los datos en el mismo conjunto de variables, debe usar **SQLGetData** en lugar de volver a enlazar constantemente. Solo puede usar **SQLGetData** en las columnas que se encuentran en la lista de selección después de que todas las columnas se enlazan con **SQLBindCol**. La columna también debe aparecer después de las columnas en las que ya ha utilizado **SQLGetData**.  
  
 Las funciones ODBC que tratan de mover datos dentro o fuera de variables de programa, como **SQLGetData**, **SQLBindCol**y [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), admiten la conversión implícita de tipos de datos. Por ejemplo, si una aplicación enlaza una columna entera a una variable de programa de cadena de caracteres, el controlador convierte automáticamente los datos enteros en caracteres antes de incluirlos en la variable de programa.  
  
 Se debe minimizar la conversión de los datos en las aplicaciones. A menos que se requiera la conversión de datos para el procesamiento realizado por la aplicación, las aplicaciones deben enlazar las columnas y los parámetros a las variables de programa del mismo tipo de datos. Si los datos se deben convertir de un tipo a otro, sin embargo, es más eficaz hacer que el controlador haga la conversión que hacerla en la aplicación. El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client normalmente solo transfiere directamente los datos desde los búferes de la red a las variables de la aplicación. La solicitud al controlador de realizar la conversión de datos fuerza al controlador a almacenar en búfer los datos y usar los ciclos de CPU para convertir los datos.  
  
 Las variables de programa deben ser lo suficientemente grandes como para contener los datos transferidos desde una columna, excepto los datos **de texto,** **ntext**e **imagen.** Si una aplicación intenta recuperar datos del conjunto de resultados y colocarlos en una variable que es demasiado pequeña para contenerlos, el controlador genera una advertencia. Esto obliga al controlador a asignar memoria para el mensaje y los dos, el controlador y la aplicación, tienen que utilizar ciclos de CPU para procesar el mensaje y realizar el tratamiento de errores. La aplicación debe asignar una variable bastante grande para contener los datos que se van a recuperar o usar la función SUBSTRING de la lista de selección para reducir el tamaño de la columna del conjunto de resultados.  
  
 Se deben extremar las precauciones al utilizar SQL_C_DEFAULT para especificar el tipo de la variable C. SQL_C_DEFAULT especifica que el tipo de la variable C coincide con el tipo de datos SQL de la columna o parámetro. Si se especifica SQL_C_DEFAULT para una columna **ntext**, **nchar**o **nvarchar,** los datos Unicode se devuelven a la aplicación. Esto puede producir varios problemas si la aplicación no ha estado codificada para administrar los datos Unicode. Pueden producirse los mismos tipos de problemas con el tipo de datos **uniqueidentifier** (SQL_GUID).  
  
 **los**datos text , **ntext**e **image** suelen ser demasiado grandes para caber en una sola variable de programa y normalmente se procesan con **SQLGetData** en lugar de **SQLBindCol**. Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se utilizan cursores de servidor, el controlador ODBC de Native Client está optimizado para no transmitir los datos de las columnas de **texto**sin enlazar, **ntext**o **imagen** en el momento en que se captura la fila. Los datos **text**, **ntext**o **image** no se recuperan realmente del servidor hasta que la aplicación emite **SQLGetData** para la columna.  
  
 Esta optimización se puede aplicar a las aplicaciones para que no se muestre ningún **texto,** **ntext**o datos de **imagen** mientras un usuario se desplaza hacia arriba y hacia abajo un cursor. Después de que el usuario selecciona una fila, la aplicación puede llamar a **SQLGetData** para recuperar los datos de **texto,** **ntext**o **imagen.** Esto ahorra la transmisión de los datos de **texto,** **ntext**o **imagen** para cualquiera de las filas que el usuario no selecciona y puede guardar la transmisión de grandes cantidades de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Procesamiento de resultados &#40;&#41;ODBC](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
