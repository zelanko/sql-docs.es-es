---
title: Argumentos de la función Unicode (Unicode Function Arguments) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: eafe8c7e-f6d2-44d7-99ee-cf2148a30f4f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a25dd6fe0a77aad5c5ec9ba15eaf12bd2ec3fc18
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284295"
---
# <a name="unicode-function-arguments"></a>Argumentos de función de Unicode
El Administrador de controladores ODBC 3.5 (o superior) admite versiones ANSI y Unicode de todas las funciones que aceptan punteros a cadenas de caracteres o SQLPOINTER en sus argumentos. Las funciones Unicode se implementan como funciones (con un sufijo *W*), no como macros. Las funciones ANSI (a las que se puede llamar con o sin un sufijo de *A*) son idénticas a las funciones actuales de la API ODBC.  
  
## <a name="remarks"></a>Observaciones  
 Las funciones Unicode que siempre devuelven o toman cadenas o argumentos de longitud se pasan como recuento de caracteres. Para las funciones que devuelven información de longitud para los datos del servidor, el tamaño de visualización y la precisión se describen en número de caracteres. Cuando una longitud (tamaño de transferencia de los datos) podría hacer referencia a datos de cadena o no de cadena, la longitud se describe en longitudes de octeto. Por ejemplo, **SQLGetInfoW** seguirá tomás la longitud como recuento de bytes, pero **SQLExecDirectW** usará count-of-characters.  
  
 Count-of-characters hace referencia al número de bytes (octets) para las funciones ANSI y al número de WCHAR (palabras de 16 bits) para las funciones UNICODE. En particular, una secuencia de caracteres de doble byte (DBCS) o una secuencia de caracteres multibyte (MBCS) se pueden componer de varios bytes. Una secuencia de caracteres Unicode UTF-16 se puede componer de varios WcHAR.  
  
 A continuación se muestra una lista de las funciones de la API ODBC que admiten las versiones Unicode (W) y ANSI (A):  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagRec**|  
|**SQLColAttribute**|**SQLGetInfo**|  
|**SQLColAttributes**|**SQLGetStmtAttr**|  
|**SQLColumnPrivileges**|**SQLGetTypeInfo**|  
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
|**SQLGetDiagField**||  
  
 A continuación se muestra una lista de las funciones Odbc Installer y ODBC Translator que admiten las versiones Unicode (W) y ANSI (A):  
  
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
>  Las funciones en desuso tienen compatibilidad con la asignación de Unicode a ANSI porque el Administrador de controladores ODBC *3.x* admite la recompilación de aplicaciones ODBC *2.x* con la **#define**UNICODE.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Aplicaciones de Unicode](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Controladores de Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [Asignación de función en el Administrador de controladores](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
