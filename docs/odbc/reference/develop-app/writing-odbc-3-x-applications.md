---
title: Escribir aplicaciones de ODBC 3.x | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application upgrades [ODBC], about upgrading
- ODBC drivers [ODBC], backward compatibility
- upgrading applications [ODBC]
- compatibility [ODBC], upgrading applications
- application upgrades [ODBC]
- upgrading applications [ODBC], about upgrading
- backward compatibility [ODBC], upgrading applications
ms.assetid: 19c54fc5-9dd6-49b6-8c9f-a38961b40a65
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da096dd38c87131259f9ea626fa874c0b83b7b95
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="writing-odbc-3x-applications"></a>Escribir ODBC 3.x aplicaciones
Cuando un ODBC 2. *x* aplicación se actualiza a ODBC 3. *x*, deben escribirse tal que funciona con ODBC 2. *x* y 3. *x* controladores. La aplicación debe incorporar código condicional para aprovechar al máximo de ODBC 3. *x* características.  
  
 El atributo de entorno SQL_ATTR_ODBC_VERSION debe establecerse en SQL_OV_ODBC2. Así se asegurará de que el controlador se comporta como una API ODBC 2*.x* controlador con respecto a los cambios descritos en la sección [cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Si la aplicación va a utilizar cualquiera de las características descritas en la sección [nuevas características](../../../odbc/reference/develop-app/new-features.md), código condicional debe usarse para determinar si el controlador es una aplicación ODBC 3. *x* o 2 de ODBC*.x* controlador. La aplicación usa **SQLGetDiagField** y **SQLGetDiagRec** obtener ODBC 3. *x* SQLSTATE mientras realiza el error que se está procesando en estos fragmentos de código condicional. Deben tener en cuenta los siguientes puntos acerca de las nuevas funcionalidades:  
  
-   Una aplicación que se ve afectada por el cambio de comportamiento de tamaño de conjunto de filas debe tener cuidadosa de no llamar a **SQLFetch** cuando el tamaño de la matriz es mayor que 1. Estas aplicaciones deben reemplazar las llamadas a **SQLExtendedFetch** con llamadas a **SQLSetStmtAttr** para establecer el atributo de instrucción de SQL_ATTR_ARRAY_STATUS_PTR y a **SQLFetchScroll**, de modo que tienen código común que funciona con ambas ODBC 3. *x* y ODBC 2. *x* controladores. Dado que **SQLSetStmtAttr** con SQL_ATTR_ROW_ARRAY_SIZE se asignarán a **SQLSetStmtAttr** con SQL_ROWSET_SIZE para ODBC 2. *x* controladores, aplicaciones basta con establecer SQL_ATTR_ROW_ARRAY_SIZE para sus operaciones de recopilación de varias filas.  
  
-   La mayoría de las aplicaciones que van a actualizar no resultan afectadas por los cambios de códigos SQLSTATE. Para las aplicaciones que se ven afectadas, pueden realizar una búsqueda mecánica y reemplazar en la mayoría de los casos usando la tabla de conversión de error en la sección "Realizar asignaciones SQLSTATE" para convertir ODBC 3. *x* códigos de error que ODBC 2*.x* códigos. Desde ODBC 3*.x* el Administrador de controladores realizará la asignación de ODBC 2. *x* SqlState para ODBC 3. *x* SQLSTATE, estos sistemas de escritura de la aplicación necesitan sólo comprobación de ODBC 3. *x* los códigos SQLState y no te preocupes acerca de cómo incluir ODBC 2. *x* SQLSTATEs en el código condicional.  
  
-   Si una aplicación realiza gran uso de fecha, hora y tipos de datos de marca de tiempo, la aplicación puede declarar que ha llegado a ser un 2 de ODBC. *x* aplicación y utilice código su existente en lugar de utilizar código acondicionado.  
  
 La actualización también debe incluir los siguientes pasos:  
  
-   Llame a **SQLSetEnvAttr** antes de asignar una conexión para establecer el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC2.  
  
-   Reemplace todas las llamadas a **SQLAllocEnv**, **SQLAllocConnect**, o **SQLAllocStmt** con llamadas a **SQLAllocHandle** con el adecuado *HandleType* argumento de SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
-   Reemplace todas las llamadas a **SQLFreeEnv** o **SQLFreeConnect** con llamadas a **SQLFreeHandle** con el adecuado *HandleType* argumento de SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
-   Reemplace todas las llamadas a **SQLSetConnectOption** con llamadas a **SQLSetConnectAttr**. Si establece un atributo cuyo valor es una cadena, establezca el *StringLength* argumento adecuadamente. Cambio *atributo* argumento de SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLGetConnectOption** con llamadas a **SQLGetConnectAttr**. Si recibe una cadena o un atributo binario, establezca *BufferLength* para el valor adecuado y pase un *StringLength* argumento. Cambio *atributo* argumento de SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLSetStmtOption** con llamadas a **SQLSetStmtAttr**. Si establece un atributo cuyo valor es una cadena, establezca el *StringLength* argumento adecuadamente. Cambio *atributo* argumento de SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLGetStmtOption** con llamadas a **SQLGetStmtAttr**. Si recibe una cadena o un atributo binario, establezca *BufferLength* para el valor adecuado y pase un *StringLength* argumento. Cambio *atributo* argumento de SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLTransact** con llamadas a **SQLEndTran**. Si el identificador válido situado en el **SQLTransact** llamada es un identificador de entorno, una *HandleType* debe usar el argumento de SQL_HANDLE_ENV en el **SQLEndTran** llama con adecuado *controlar* argumento. Si el identificador válido situado en la **SQLTransact** llamada es un identificador de conexión, un *HandleType* debe usar el argumento de SQL_HANDLE_DBC en el **SQLEndTran** llama con adecuado *controlar* argumento.  
  
-   Reemplace todas las llamadas a **SQLColAttributes** con llamadas a **SQLColAttribute**. Si el *FieldIdentifier* argumento es SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE o SQL_COLUMN_LENGTH, no se debe cambiar nada que no sea el nombre de la función. Si no es así, cambie *FieldIdentifier* de SQL_COLUMN_XXXX a SQL_DESC_XXXX. Si *FieldIdentifier* es SQL_DESC_CONCISE_TYPE y el tipo de datos es un tipo de datos de fecha y hora, cambie a la correspondiente ODBC 3*.x* tipo de datos.  
  
-   Si utiliza cursores de bloque, los cursores desplazables o ambos, la aplicación hace lo siguiente:  
  
    -   Establece el tamaño de conjunto de filas, el tipo de cursor y la simultaneidad de cursor mediante **SQLSetStmtAttr**.  
  
    -   Llamadas **SQLSetStmtAttr** establecer SQL_ATTR_ROW_STATUS_PTR para que señale a una matriz de registros de estado.  
  
    -   Llamadas **SQLSetStmtAttr** establecer SQL_ATTR_ROWS_FETCHED_PTR para que apunte a un SQLINTEGER.  
  
    -   Realiza los enlaces necesarios y ejecuta la instrucción SQL.  
  
    -   Llamadas **SQLFetchScroll** en un bucle para capturar filas y moverse por el resultado establecido.  
  
    -   Si desea capturar por marcador, la aplicación llama a **SQLSetStmtAttr** establecer SQL_ATTR_FETCH_BOOKMARK_PTR a una variable que contendrá el marcador de la fila que se va a capturar y llamadas **SQLFetchScroll** con un *FetchOrientation* argumento de SQL_FETCH_BOOKMARK.  
  
-   Si usa las matrices de parámetros, la aplicación hace lo siguiente:  
  
    -   Llamadas **SQLSetStmtAttr** para establecer el atributo SQL_ATTR_PARAMSET_SIZE en el tamaño de la matriz de parámetros.  
  
    -   Llamadas **SQLSetStmtAttr** establecer SQL_ATTR_ROWS_PROCESSED_PTR para que señale a una variable UDWORD interna.  
  
    -   Lleva a cabo preparar, enlazar y ejecutar operaciones según corresponda.  
  
    -   Si la ejecución se detiene por algún motivo (por ejemplo, SQL_NEED_DATA), que puede encontrar la fila "actual" de parámetros mediante la inspección de la ubicación señalada por SQL_ATTR_ROWS_PROCESSED_PTR.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Asignación de funciones de reemplazo para mantener la compatibilidad de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [Al llamar a SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [Al llamar a SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [Llamar a SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [Operaciones de la biblioteca de cursores](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [Asignar los tipos de información de Cursor Attributes1](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
