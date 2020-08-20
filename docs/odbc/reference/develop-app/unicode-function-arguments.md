---
description: Argumentos de función de Unicode
title: Argumentos de función Unicode | Microsoft Docs
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
ms.openlocfilehash: d2d59cad60855c670f7c7e2b189ad3c97a3027b9
ms.sourcegitcommit: 19ae05bc69edce1e3b3d621d7fdd45ea5f74969d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564043"
---
# <a name="unicode-function-arguments"></a>Argumentos de función de Unicode
El administrador de controladores ODBC 3,5 (o posterior) es compatible con las versiones ANSI y Unicode de todas las funciones que aceptan punteros a cadenas de caracteres o SQLPOINTER en sus argumentos. Las funciones Unicode se implementan como funciones (con un sufijo de *W*), no como macros. Las funciones ANSI (a las que se puede llamar con o sin un sufijo de) son idénticas a las funciones actuales de la *API de ODBC*.  
  
## <a name="remarks"></a>Observaciones  
 En el caso de las funciones Unicode que siempre devuelven o toman cadenas o argumentos de longitud, los argumentos se pasan como recuento de caracteres. En el caso de las funciones que devuelven información de longitud de los datos del servidor, el tamaño y la precisión de la pantalla se describen en número de caracteres. Cuando una longitud (el tamaño de transferencia de los datos) podría hacer referencia a datos de cadena o que no son de cadena, la longitud se describe en longitudes de octeto. Por ejemplo, **SQLGetInfoW** seguirá teniendo la longitud como recuento de bytes, pero **SQLExecDirectW** usará el recuento de caracteres.  
  
 Recuento de caracteres hace referencia al número de bytes (octetos) para las funciones ANSI y el número de WCHAR (palabras de 16 bits) para las funciones Unicode. En concreto, una secuencia de caracteres de doble byte (DBCS) o una secuencia de caracteres multibyte (MBCS) pueden estar compuestas de varios bytes. Una secuencia de caracteres Unicode UTF-16 puede estar formada por varios WCHARs.  
  
 A continuación se muestra una lista de las funciones de la API de ODBC que admiten las versiones Unicode (W) y ANSI (A):  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagRec**|  
|**SQLColAttribute**|**SQLGetInfo**|  
|**SQLColAttributes**|**SQLGetStmtAttr**|  
|**SQLColumnPrivileges**|**SQLGetTypeInfo**|  
|**SQLColumns**|**SQLNativeSql**|  
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
  
 A continuación se muestra una lista de las funciones de instalador de ODBC y de traductor de ODBC que admiten las versiones Unicode (W) y ANSI (A):  
  
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
>  Las funciones en desuso tienen compatibilidad con la asignación de Unicode a ANSI porque el administrador de controladores ODBC *3. x* admite la recompilación de aplicaciones ODBC *2. x* con la **#define**Unicode.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Aplicaciones de Unicode](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Controladores de Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [Asignación de función en el Administrador de controladores](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
