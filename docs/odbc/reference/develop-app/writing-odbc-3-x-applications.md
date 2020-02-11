---
title: Escribir aplicaciones ODBC 3. x | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9939d11e3a779cc25d7faeb4950783353947f140
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081455"
---
# <a name="writing-odbc-3x-applications"></a>Escribir ODBC 3.x aplicaciones
Cuando una aplicación ODBC *2. x* se actualiza a ODBC *3. x*, debe escribirse de modo que funcione con los controladores ODBC *2. x* y *3. x* . La aplicación debe incorporar código condicional para sacar el máximo partido de las características de ODBC *3. x* .  
  
 El atributo SQL_ATTR_ODBC_VERSION Environment debe establecerse en SQL_OV_ODBC2. Esto garantizará que el controlador se comporte como un controlador ODBC *2. x* con respecto a los cambios descritos en la sección [cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Si la aplicación va a utilizar cualquiera de las características descritas en la sección [nuevas características](../../../odbc/reference/develop-app/new-features.md), se debe usar código condicional para determinar si el controlador es un controlador ODBC *3. x* o ODBC *2. x* . La aplicación usa **SQLGetDiagField** y **SQLGETDIAGREC** para obtener ODBC *3. x* SQLSTATEs mientras se realiza el procesamiento de errores en estos fragmentos de código condicional. Se deben tener en cuenta los puntos siguientes sobre la nueva funcionalidad:  
  
-   Una aplicación afectada por el cambio en el comportamiento del tamaño del conjunto de filas debe tener cuidado de no llamar a **SQLFetch** cuando el tamaño de la matriz es mayor que 1. Estas aplicaciones deben reemplazar las llamadas a **SQLExtendedFetch** con llamadas **a SQLSetStmtAttr** para establecer el atributo de instrucción SQL_ATTR_ARRAY_STATUS_PTR y en **SQLFetchScroll**, de modo que tengan código común que funcione con los controladores ODBC *3. x* y ODBC *2. x* . Dado que **SQLSetStmtAttr** con SQL_ATTR_ROW_ARRAY_SIZE se asignará a **SQLSetStmtAttr** con SQL_ROWSET_SIZE para los controladores ODBC *2. x* , las aplicaciones solo pueden establecer SQL_ATTR_ROW_ARRAY_SIZE para las operaciones de captura de varias filas.  
  
-   En realidad, la mayoría de las aplicaciones que se están actualizando no se ven afectadas por los cambios en códigos SQLSTATE. En el caso de las aplicaciones afectadas, pueden realizar una búsqueda mecánica y reemplazar en la mayoría de los casos mediante la tabla de conversión de errores de la sección "asignación de SQLSTATE" para convertir códigos de error de ODBC *3. x* a códigos ODBC *2. x* . Dado que el administrador de controladores ODBC *3. x* realizará la asignación desde ODBC *2. x* SQLSTATEs a ODBC *3. x* SQLSTATEs, estos escritores de aplicaciones solo necesitan comprobar el SQLSTATEs de ODBC *3. x* y no preocuparse por incluir ODBC *2. x* SQLSTATEs en código condicional.  
  
-   Si una aplicación hace un gran uso de los tipos de datos de fecha, hora y marca de tiempo, la aplicación puede declararse como una aplicación ODBC *2. x* y usar el código existente en lugar de usar el código de acondicionamiento.  
  
 La actualización también debe incluir los siguientes pasos:  
  
-   Llame a **SQLSetEnvAttr** antes de asignar una conexión para establecer el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC2.  
  
-   Reemplace todas las llamadas a **SQLAllocEnv**, **SQLAllocConnect**o **SQLAllocStmt** por llamadas a **SQLAllocHandle** con el argumento *HandleType* adecuado de SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
-   Reemplace todas las llamadas a **SQLFreeEnv** o **SQLFreeConnect** por llamadas a **SQLFreeHandle** con el argumento *HandleType* adecuado de SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
-   Reemplace todas las llamadas a **SQLSetConnectOption** por llamadas a **SQLSetConnectAttr**. Si se establece un atributo cuyo valor es una cadena, establezca el argumento *StringLength* correctamente. Cambie el argumento de *atributo* de SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLGetConnectOption** por llamadas a **SQLGetConnectAttr**. Si obtiene un atributo de cadena o binario, establezca *BufferLength* en el valor adecuado y pase un argumento *StringLength* . Cambie el argumento de *atributo* de SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLSetStmtOption** por llamadas a **SQLSetStmtAttr**. Si se establece un atributo cuyo valor es una cadena, establezca el argumento *StringLength* correctamente. Cambie el argumento de *atributo* de SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLGetStmtOption** por llamadas a **SQLGetStmtAttr**. Si obtiene un atributo de cadena o binario, establezca *BufferLength* en el valor adecuado y pase un argumento *StringLength* . Cambie el argumento de *atributo* de SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLTransact** por llamadas a **SQLEndTran**. Si el identificador válido más a la derecha en la llamada a **SQLTransact** es un identificador de entorno, se debe usar un argumento *HandleType* de SQL_HANDLE_ENV en la llamada **SQLEndTran** con el argumento de *identificador* adecuado. Si el identificador válido más a la derecha en la llamada a **SQLTransact** es un identificador de conexión, se debe usar un argumento *HandleType* de SQL_HANDLE_DBC en la llamada **SQLEndTran** con el argumento de *identificador* adecuado.  
  
-   Reemplace todas las llamadas a **SQLColAttributes** por llamadas a **SQLColAttribute**. Si el argumento *FieldIdentifier* es SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE o SQL_COLUMN_LENGTH, no cambie nada que no sea el nombre de la función. Si no es así, cambie *FieldIdentifier* de SQL_COLUMN_XXXX a SQL_DESC_XXXX. Si *FieldIdentifier* es SQL_DESC_CONCISE_TYPE y el tipo de datos es un tipo de datos DateTime, cambie al tipo de datos ODBC *3. x* correspondiente.  
  
-   Si utiliza cursores de bloque, cursores desplazables o ambos, la aplicación hace lo siguiente:  
  
    -   Establece el tamaño del conjunto de filas, el tipo de cursor y la simultaneidad del cursor mediante **SQLSetStmtAttr**.  
  
    -   Llama a **SQLSetStmtAttr** para establecer SQL_ATTR_ROW_STATUS_PTR para que apunten a una matriz de registros de estado.  
  
    -   Llama a **SQLSetStmtAttr** para establecer SQL_ATTR_ROWS_FETCHED_PTR para que apunten a un sqlinteger donde.  
  
    -   Realiza los enlaces necesarios y ejecuta la instrucción SQL.  
  
    -   Llama a **SQLFetchScroll** en un bucle para capturar filas y desplazarse por el conjunto de resultados.  
  
    -   Si desea capturar por marcador, la aplicación llama a **SQLSetStmtAttr** para establecer SQL_ATTR_FETCH_BOOKMARK_PTR en una variable que contendrá el marcador de la fila que desea capturar y llama a **SQLFetchScroll** con un argumento *FetchOrientation* de SQL_FETCH_BOOKMARK.  
  
-   Si usa matrices de parámetros, la aplicación hace lo siguiente:  
  
    -   Llama a **SQLSetStmtAttr** para establecer el atributo de SQL_ATTR_PARAMSET_SIZE en el tamaño de la matriz de parámetros.  
  
    -   Llama a **SQLSetStmtAttr** para establecer SQL_ATTR_ROWS_PROCESSED_PTR de forma que señale a una variable interna de UDWORD.  
  
    -   Realiza las operaciones de preparación, enlace y ejecución según corresponda.  
  
    -   Si la ejecución se detiene por alguna razón (como SQL_NEED_DATA), puede encontrar la fila "actual" de parámetros inspeccionando la ubicación a la que apunta SQL_ATTR_ROWS_PROCESSED_PTR.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Asignación de funciones de reemplazo para mantener la compatibilidad de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [Al llamar a SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [Al llamar a SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [Llamar a SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [Operaciones de la biblioteca de cursores](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [Asignar los tipos de información de Cursor Attributes1](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
