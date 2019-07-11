---
title: Escribir ODBC 3.x aplicaciones | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 4a51183964fe36d799e0e62243c6a0012da99727
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793284"
---
# <a name="writing-odbc-3x-applications"></a>Escribir ODBC 3.x aplicaciones
Cuando un ODBC *2.x* aplicación se actualiza a ODBC *3.x*, se deberá escribir de forma que funcione con ambas ODBC *2.x* y *3.x* controladores . La aplicación debe incorporar código condicional para aprovechar al máximo el ODBC *3.x* características.  
  
 El atributo de entorno SQL_ATTR_ODBC_VERSION debe establecerse en SQL_OV_ODBC2. Así se asegurará de que el controlador se comporta como un ODBC *2.x* controlador con respecto a los cambios descritos en la sección [cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Si la aplicación puede emplear cualquiera de las características descritas en la sección [nuevas características](../../../odbc/reference/develop-app/new-features.md), se debe utilizar código condicional para determinar si el controlador es un ODBC *3.x* u ODBC *2.x* controlador. La aplicación usa **SQLGetDiagField** y **SQLGetDiagRec** obtener ODBC *3.x* SQLSTATEs mientras se realiza el error que se está procesando en estos fragmentos de código condicional. Deben tener en cuenta los siguientes puntos acerca de la nueva funcionalidad:  
  
-   Una aplicación que se ve afectada por el cambio de comportamiento de tamaño del conjunto de filas debe tener cuidadosa de no llamar a **SQLFetch** cuando el tamaño de la matriz es mayor que 1. Estas aplicaciones deben reemplazar las llamadas a **SQLExtendedFetch** con llamadas a **SQLSetStmtAttr** para establecer el atributo de instrucción SQL_ATTR_ARRAY_STATUS_PTR y a **SQLFetchScroll**, de modo que tienen código común que funciona con ODBC *3.x* y ODBC *2.x* controladores. Dado que **SQLSetStmtAttr** con SQL_ATTR_ROW_ARRAY_SIZE se asignará a **SQLSetStmtAttr** con SQL_ROWSET_SIZE para ODBC *2.x* controladores, las aplicaciones solo pueden establecer SQL _ATTR_ROW_ARRAY_SIZE para sus operaciones de captura con varias filas.  
  
-   La mayoría de las aplicaciones que se va a actualizar no resultan afectadas por cambios en los códigos SQLSTATE. Para aquellas aplicaciones que se ven afectadas, puede realizar una búsqueda mecánica y reemplazar en la mayoría de los casos con la tabla de conversión de errores en la sección "Realizar asignaciones SQLSTATE" para convertir ODBC *3.x* códigos de error de ODBC *2.x* códigos. Desde ODBC *3.x* Administrador de controladores realizará la asignación de ODBC *2.x* SqlState para ODBC *3.x* SQLSTATE, estos escritores de la aplicación necesitan comprobación solo para ODBC  *3.x* SQLState y no preocuparse acerca de cómo incluir ODBC *2.x* SQLSTATEs en código condicional.  
  
-   Si una aplicación muchísimo de fecha, hora y tipos de datos de marca de tiempo, la aplicación puede declarar a sí mismo como un ODBC *2.x* aplicación y utilice código su existente en lugar de usar código acondicionado.  
  
 La actualización también debe incluir los siguientes pasos:  
  
-   Llame a **SQLSetEnvAttr** antes de asignar una conexión para establecer el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC2.  
  
-   Reemplace todas las llamadas a **SQLAllocEnv**, **SQLAllocConnect**, o **SQLAllocStmt** con llamadas a **SQLAllocHandle** con los valores adecuados *HandleType* argumento de SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
-   Reemplace todas las llamadas a **SQLFreeEnv** o **SQLFreeConnect** con llamadas a **SQLFreeHandle** con los valores adecuados *HandleType* argumento de SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
-   Reemplace todas las llamadas a **SQLSetConnectOption** con llamadas a **SQLSetConnectAttr**. Si establece un atributo cuyo valor es una cadena, establezca el *StringLength* argumento adecuadamente. Cambio *atributo* argumento desde SQL_XXXX SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLGetConnectOption** con llamadas a **SQLGetConnectAttr**. Si recibe una cadena o un atributo binario, establezca *BufferLength* para el valor adecuado y pase un *StringLength* argumento. Cambio *atributo* argumento desde SQL_XXXX SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLSetStmtOption** con llamadas a **SQLSetStmtAttr**. Si establece un atributo cuyo valor es una cadena, establezca el *StringLength* argumento adecuadamente. Cambio *atributo* argumento desde SQL_XXXX SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLGetStmtOption** con llamadas a **SQLGetStmtAttr**. Si recibe una cadena o un atributo binario, establezca *BufferLength* para el valor adecuado y pase un *StringLength* argumento. Cambio *atributo* argumento desde SQL_XXXX SQL_ATTR_XXXX.  
  
-   Reemplace todas las llamadas a **SQLTransact** con llamadas a **SQLEndTran**. Si el identificador válido situado en la **SQLTransact** llamada es un identificador de entorno, un *HandleType* debe usar el argumento de SQL_HANDLE_ENV en el **SQLEndTran** llamar con adecuado *controlar* argumento. Si el identificador válido situado en la **SQLTransact** llamada es un identificador de conexión, un *HandleType* debe usar el argumento de SQL_HANDLE_DBC en el **SQLEndTran** llamar con adecuado *controlar* argumento.  
  
-   Reemplace todas las llamadas a **SQLColAttributes** con llamadas a **SQLColAttribute**. Si el *FieldIdentifier* argumento es SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE o SQL_COLUMN_LENGTH, no se debe cambiar nada que no sea el nombre de la función. Si no, cambie *FieldIdentifier* desde SQL_COLUMN_XXXX a SQL_DESC_XXXX. Si *FieldIdentifier* es SQL_DESC_CONCISE_TYPE y el tipo de datos es un tipo de datos de fecha y hora, cambie a ODBC correspondiente *3.x* tipo de datos.  
  
-   Si utiliza cursores de bloque, cursores desplazables o ambos, la aplicación hace lo siguiente:  
  
    -   Establece el tamaño de conjunto de filas, el tipo de cursor y la simultaneidad de cursor mediante **SQLSetStmtAttr**.  
  
    -   Las llamadas **SQLSetStmtAttr** a establezca SQL_ATTR_ROW_STATUS_PTR para que señale a una matriz de registros de estado.  
  
    -   Las llamadas **SQLSetStmtAttr** establecer SQL_ATTR_ROWS_FETCHED_PTR para que apunte a un SQLINTEGER.  
  
    -   Realiza los enlaces necesarios y ejecuta la instrucción SQL.  
  
    -   Las llamadas **SQLFetchScroll** en un bucle para capturar filas y moverse por el resultado establecido.  
  
    -   Si desea capturar por marcador, la aplicación llama a **SQLSetStmtAttr** establecer SQL_ATTR_FETCH_BOOKMARK_PTR a una variable que contendrá el marcador para la fila que desea capturar y llama a **SQLFetchScroll** con un *FetchOrientation* argumento de SQL_FETCH_BOOKMARK.  
  
-   Si el uso de matrices de parámetros, la aplicación hace lo siguiente:  
  
    -   Las llamadas **SQLSetStmtAttr** para establecer el atributo SQL_ATTR_PARAMSET_SIZE en el tamaño de la matriz de parámetros.  
  
    -   Las llamadas **SQLSetStmtAttr** establecer SQL_ATTR_ROWS_PROCESSED_PTR para que apunte a una variable UDWORD interna.  
  
    -   Realiza la preparación, enlazar y ejecutar operaciones según corresponda.  
  
    -   Si la ejecución se detiene por alguna razón (por ejemplo, SQL_NEED_DATA), puede encontrar la fila "actual" de los parámetros mediante la inspección de la ubicación señalada por SQL_ATTR_ROWS_PROCESSED_PTR.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Asignación de funciones de reemplazo para mantener la compatibilidad de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [Al llamar a SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [Al llamar a SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [Llamar a SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [Operaciones de la biblioteca de cursores](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [Asignar los tipos de información de Cursor Attributes1](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
