---
title: "Argumentos de la función Unicode | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: eafe8c7e-f6d2-44d7-99ee-cf2148a30f4f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ff461881ea10c904ceefd1c51a364984ca10971b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="unicode-function-arguments"></a>Argumentos de función de Unicode
El Administrador de controladores ODBC 3.5 (o superior) es compatible con las versiones ANSI y Unicode de todas las funciones que aceptan los punteros a cadenas de caracteres o SQLPOINTER en sus argumentos. Las funciones Unicode se implementan como funciones (con un sufijo de *W*), no como macros. Las funciones de ANSI (que se puede llamar con o sin un sufijo de *A*) son idénticas a las funciones de API de ODBC actuales.  
  
## <a name="remarks"></a>Comentarios  
 Las funciones Unicode que siempre devuelven o toman cadenas o argumentos de longitud se pasan como recuento de caracteres. Para las funciones que devuelven información sobre la longitud de datos del servidor, el tamaño de presentación y la precisión se describen en el número de caracteres. Cuando una longitud (tamaño de transferencia de los datos) puede hacer referencia a los datos de cadena o que no son cadenas, se describe la longitud en longitudes de octeto. Por ejemplo, **SQLGetInfoW** todavía tendrá la longitud como recuento de bytes, pero **SQLExecDirectW** utilizará el número de caracteres.  
  
 Recuento de caracteres se refiere al número de bytes (octetos) para las funciones de ANSI y el número de WCHAR (palabras de 16 bits) para las funciones UNICODE. En concreto, una secuencia de caracteres de doble byte (DBCS) o una secuencia de caracteres multibyte (MBCS) puede estar compuesta de varios bytes. Una secuencia de caracteres Unicode UTF-16 puede estar compuesta de un número de WCHAR varios.  
  
 La siguiente es una lista de las funciones de API de ODBC que admiten las versiones de Unicode (W) y ANSI (A):  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagField**|  
|**SQLColAttribute**|**SQLGetDiagRec**|  
|**SQLColAttributes**|**SQLGetInfo**|  
|**SQLColumnPrivileges**|**SQLGetStmtAttr**|  
|**SQLColumns**|**SQLNativeSQL**|  
|**SQLConnect**|**SQLPrepare**|  
|**SQLDataSources**|**SQLPrimaryKeys**|  
|**SQLDescribeCol**|**SQLProcedureColumns**|  
|**SQLDriverConnect**|**SQLProcedures**|  
|**SQLDrivers**|**SQLSetConnectAttr**|  
|**SQLError**|**SQLSetConnectOption**|  
|**SQLExecDirect**|**SQLSetCursorName**|  
|**SQLForeignKeys**|**SQLSetDescField**|  
|**SQLGetConnectAttr**|**SQLSetStmtAttr**|  
|**SQLGetConnectOption**|**SQLSpecialColumns**|  
|**SQLGetCursorName**|**SQLStatistics**|  
|**SQLGetDescField**|**SQLTablePrivileges**|  
|**SQLGetDescRec**|**SQLTables**|  
  
 La siguiente es una lista de las funciones del instalador ODBC y el traductor de ODBC que admiten versiones Unicode (W) y ANSI (A):  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstallDriverManager**|  
|**SQLCreateDataSource**|**SQLInstallerError**|  
|**SQLDataSourceToDriver**|**SQLInstallODBC**|  
|**SQLDriverToDataSource**|**SQLReadFileDSN**|  
|**SQLGetAvailableDrivers**|**SQLRemoveDSNFromINI**|  
|**SQLGetInstalledDrivers**|**SQLValidDSN**|  
|**SQLGetTranslator**|**SQLWriteDSNToINI**|  
|**SQLInstallDriver**||  
  
> [!NOTE]  
>  Funciones en desuso tienen compatibilidad de asignación de Unicode a ANSI porque ODBC 3*.x* el Administrador de controladores es compatible con volver a compilar ODBC 2. *x* aplicaciones con UNICODE **#define**.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Aplicaciones de Unicode](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Controladores de Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [Asignación de función en el Administrador de controladores](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)

