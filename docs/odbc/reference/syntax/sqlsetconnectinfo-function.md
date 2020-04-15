---
title: Función SQLSetConnectInfo ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectInfo function [ODBC]
ms.assetid: 0782a1c3-c5d1-499b-a8ba-134162db9990
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b575e0d09f87ad21e1190b8081b6604349a98263
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301856"
---
# <a name="sqlsetconnectinfo-function"></a>Función SQLSetConnectInfo
**Conformidad**  
 Versión introducida: CUMPLIMIENTO de estándares ODBC 3.81: ODBC  
  
 **Resumen**  
 **SQLSetConnectInfo** se usa para establecer el origen de datos, el identificador de usuario y la contraseña en el token de información de conexión para la llamada [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) de una aplicación.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
  
SQLRETURN  SQLSetConnectInfo(  
                SQLHDBC_INFO_TOKEN   TokenHandle,  
                WCHAR *              ServerName,  
                SQLSMALLINT          NameLength1,  
                WCHAR *              UserName,  
                SQLSMALLINT          NameLength2,  
                WCHAR *              Authentication,  
                SQLSMALLINT          NameLength3 );  
```  
  
## <a name="arguments"></a>Argumentos  
 *TokenHandle*  
 [Entrada] Mango de token.  
  
 *nombreDeServidor*  
 [Entrada] Nombre del origen de datos. Los datos pueden estar ubicados en el mismo equipo que el programa, o en otro equipo en algún lugar de una red. Para obtener información sobre cómo una aplicación elige un origen de datos, vea Elegir un origen de [datos o un controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 *NameLength1*  
 [Entrada] Longitud de **ServerName* en caracteres.  
  
 *nombre de usuario*  
 [Entrada] Identificador de usuario.  
  
 *NameLength2*  
 [Entrada] Longitud de **UserName* en caracteres.  
  
 *Autenticación*  
 [Entrada] Cadena de autenticación (normalmente la contraseña).  
  
 *NameLength3*  
 [Entrada] Longitud de **Autenticación* en caracteres.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Igual que [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) para los errores de validación de entrada, excepto que el Administrador de controladores usará un **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN y un **identificador** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Observaciones  
 Cada vez que un controlador devuelve SQL_ERROR o SQL_INVALID_HANDLE, el Administrador de controladores devuelve el error a la aplicación (en [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Cada vez que un controlador devuelve SQL_SUCCESS_WITH_INFO, el Administrador de controladores obtendrá la información de diagnóstico de *hDbcInfoToken*y devolverá SQL_SUCCESS_WITH_INFO a la aplicación en [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) y [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Las aplicaciones no deben llamar a esta función directamente. Un controlador ODBC que admite la agrupación de conexiones con reconocimiento de controladores debe implementar esta función.  
  
 Incluya sqlspi.h para el desarrollo de controladores ODBC.  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollo de un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación de conexiones conscientes del conductor](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
