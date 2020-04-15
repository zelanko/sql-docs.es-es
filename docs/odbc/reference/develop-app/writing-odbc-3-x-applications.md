---
title: Escritura de aplicaciones ODBC 3.x Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], about upgrading
- ODBC drivers [ODBC], backward compatibility
- upgrading applications [ODBC]
- compatibility [ODBC], upgrading applications
- application upgrades [ODBC]
- upgrading applications [ODBC], about upgrading
- backward compatibility [ODBC], upgrading applications
ms.assetid: 19c54fc5-9dd6-49b6-8c9f-a38961b40a65
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ba48d76babcaa5fcc49a541088f7c4cc349b569
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288993"
---
# <a name="writing-odbc-3x-applications"></a>Escribir ODBC 3.x aplicaciones
Cuando una aplicación ODBC *2.x* se actualiza a ODBC *3.x*, debe escribirse de forma que funcione con controladores ODBC *2.x* y *3.x.* La aplicación debe incorporar código condicional para aprovechar al máximo las características de ODBC *3.x.*  
  
 El atributo de entorno SQL_ATTR_ODBC_VERSION debe establecerse en SQL_OV_ODBC2. Esto garantizará que el controlador se comporta como un controlador ODBC *2.x* con respecto a los cambios descritos en la sección [Cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Si la aplicación va a utilizar cualquiera de las características descritas en la sección [Nuevas características](../../../odbc/reference/develop-app/new-features.md), se debe usar código condicional para determinar si el controlador es un controlador ODBC *3.x* u ODBC *2.x.* La aplicación usa **SQLGetDiagField** y **SQLGetDiagRec** para obtener SQLSTATEs ODBC *3.x* mientras se realiza el procesamiento de errores en estos fragmentos de código condicional. Se deben tener en cuenta los siguientes puntos sobre la nueva funcionalidad:  
  
-   Una aplicación afectada por el cambio en el comportamiento del tamaño del conjunto de filas debe tener cuidado de no llamar a **SQLFetch** cuando el tamaño de la matriz es mayor que 1. Estas aplicaciones deben reemplazar las llamadas a **SQLExtendedFetch** con llamadas a **SQLSetStmtAttr** para establecer el atributo de instrucción SQL_ATTR_ARRAY_STATUS_PTR y a **SQLFetchScroll**, para que tengan código común que funcione con controladores ODBC *3.x* y ODBC *2.x.* Dado que **SQLSetStmtAttr** con SQL_ATTR_ROW_ARRAY_SIZE se asignará a **SQLSetStmtAttr** con SQL_ROWSET_SIZE para controladores ODBC *2.x,* las aplicaciones solo pueden establecer SQL_ATTR_ROW_ARRAY_SIZE para sus operaciones de obtención de varias filas.  
  
-   La mayoría de las aplicaciones que se están actualizando no se ven realmente afectadas por los cambios en los códigos SQLSTATE. Para aquellas aplicaciones que se ven afectadas, pueden realizar una búsqueda mecánica y reemplazar en la mayoría de los casos mediante la tabla de conversión de errores de la sección "Asignación SQLSTATE" para convertir códigos de error ODBC *3.x* en códigos ODBC *2.x.* Puesto que el Administrador de controladores ODBC *3.x* realizará la asignación de SQLSTATEs ODBC *2.x* a SQLSTATEs ODBC *3.x,* estos escritores de aplicaciones solo necesitan comprobar los SQLSTATEs ODBC *3.x* y no preocuparse por incluir SQLSTATEs ODBC *2.x* en código condicional.  
  
-   Si una aplicación hace un gran uso de los tipos de datos de fecha, hora y marca de tiempo, la aplicación puede declararse como una aplicación ODBC *2.x* y usar su código existente en lugar de usar código de acondicionamiento.  
  
 La actualización también debe incluir los siguientes pasos:  
  
-   Llame a **SQLSetEnvAttr** antes de asignar una conexión para establecer el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC2.  
  
-   Reemplace todas las llamadas a **SQLAllocEnv**, **SQLAllocConnect**o **SQLAllocStmt** por llamadas a **SQLAllocHandle** por el argumento *HandleType* adecuado de SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
-   Reemplace todas las llamadas a **SQLFreeEnv** o **SQLFreeConnect** con llamadas a **SQLFreeHandle** por el argumento *HandleType* adecuado de SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
-   Reemplace todas las llamadas a **SQLSetConnectOption** por llamadas a **SQLSetConnectAttr**. Si establece un atributo cuyo valor es una cadena, establezca el *StringLength* argumento correctamente. Cambie el argumento *Attribute* de SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLGetConnectOption** por llamadas a **SQLGetConnectAttr**. Si obtiene una cadena o un atributo binario, establezca *BufferLength* en el valor adecuado y pase un *StringLength* argumento. Cambie el argumento *Attribute* de SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLSetStmtOption** por llamadas a **SQLSetStmtAttr**. Si establece un atributo cuyo valor es una cadena, establezca el *StringLength* argumento correctamente. Cambie el argumento *Attribute* de SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLGetStmtOption** por llamadas a **SQLGetStmtAttr**. Si obtiene una cadena o un atributo binario, establezca *BufferLength* en el valor adecuado y pase un *StringLength* argumento. Cambie el argumento *Attribute* de SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLTransact** por llamadas a **SQLEndTran**. Si el identificador válido más a la derecha en la llamada **SQLTransact** es un identificador de entorno, un *HandleType* argumento de SQL_HANDLE_ENV debe usarse en el **SQLEndTran** llamada con el *identificador* adecuado argumento. Si el identificador válido más a la derecha en la llamada **SQLTransact** es un identificador de conexión, un *HandleType* argumento de SQL_HANDLE_DBC debe usarse en el **SQLEndTran** llamada con el *identificador* adecuado argumento.  
  
-   Reemplace todas las llamadas a **SQLColAttributes** por llamadas a **SQLColAttribute**. Si el *Argumento FieldIdentifier* es SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE o SQL_COLUMN_LENGTH, no cambie nada que no sea el nombre de la función. Si no es así, cambie *FieldIdentifier* de SQL_COLUMN_XXXX a SQL_DESC_XXXX. Si *FieldIdentifier* es SQL_DESC_CONCISE_TYPE y el tipo de datos es un tipo de datos datetime, cambie al tipo de datos ODBC *3.x* correspondiente.  
  
-   Si utiliza cursores de bloque, cursores desplazables o ambos, la aplicación hace lo siguiente:  
  
    -   Establece el tamaño del conjunto de filas, el tipo de cursor y la simultaneidad del cursor mediante **SQLSetStmtAttr**.  
  
    -   Llama a **SQLSetStmtAttr** para establecer SQL_ATTR_ROW_STATUS_PTR para que apunte a una matriz de registros de estado.  
  
    -   Llama a **SQLSetStmtAttr** para establecer SQL_ATTR_ROWS_FETCHED_PTR para que apunte a un SQLINTEGER.  
  
    -   Realiza los enlaces necesarios y ejecuta la instrucción SQL.  
  
    -   Llama a **SQLFetchScroll** en un bucle para capturar filas y moverse en el conjunto de resultados.  
  
    -   Si desea capturar por marcador, la aplicación llama a **SQLSetStmtAttr** para establecer SQL_ATTR_FETCH_BOOKMARK_PTR en una variable que contendrá el marcador de la fila que desea capturar y llama a **SQLFetchScroll** con un *FetchOrientation* argumento de SQL_FETCH_BOOKMARK.  
  
-   Si utiliza matrices de parámetros, la aplicación hace lo siguiente:  
  
    -   Llama a **SQLSetStmtAttr** para establecer el atributo SQL_ATTR_PARAMSET_SIZE en el tamaño de la matriz de parámetros.  
  
    -   Llama a **SQLSetStmtAttr** para establecer SQL_ATTR_ROWS_PROCESSED_PTR para que apunte a una variable UDWORD interna.  
  
    -   Realiza operaciones de preparación, enlace y ejecución según corresponda.  
  
    -   Si la ejecución se detiene por alguna razón (como SQL_NEED_DATA), puede encontrar la fila "actual" de parámetros inspeccionando la ubicación a la que apunta SQL_ATTR_ROWS_PROCESSED_PTR.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Asignación de funciones de reemplazo para mantener la compatibilidad de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [Al llamar a SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [Al llamar a SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [Llamar a SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [Operaciones de la biblioteca de cursores](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [Asignar los tipos de información de Cursor Attributes1](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
