---
title: Función SQLPoolConnect (SQLPoolConnect) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5045fe47683529f858b01e69f6af696e2821ca4c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306906"
---
# <a name="sqlpoolconnect-function"></a>Función SQLPoolConnect
**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 3.8: ODBC  
  
 **Resumen**  
 **SQLPoolConnect** se utiliza para crear una nueva conexión si no se puede reutilizar ninguna conexión en el grupo.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
  
SQLRETURN  SQLPoolConnect(  
                SQLHDBC              hDbc,  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              wszOutConnectString,  
                SQLSMALLINT          cchConnectStringBuffer,  
                SQLSMALLINT *        cchConnectStringLen );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hDbc*  
 [Entrada] El controlador de conexión.  
  
 *hDbcInfoToken*  
 [Entrada] El identificador de token para la nueva solicitud de conexión de aplicación.  
  
 *wszOutConnectString*  
 [Salida] Puntero a un búfer para la cadena de conexión completada. Tras la conexión correcta con el origen de datos de destino, este búfer contiene la cadena de conexión completada. Las aplicaciones deben asignar al menos 1.024 caracteres para este búfer.  
  
 Si *wszOutConnectString* es NULL, *cchConnectStringLen* seguirá devolviendo el número total de caracteres (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer al que apunta *wszOutConnectString*.  
  
 *cchConnectStringBuffer*  
 [Entrada] Longitud del búfer **wszOutConnectString,* en caracteres.  
  
 *cchConnectStringLen*  
 [Salida] Puntero a un búfer en el que se va a devolver el número \*total de caracteres (excluyendo el carácter de terminación null) disponibles para devolver en *wszOutConnectString*. Si el número de caracteres disponibles para devolver es mayor o igual \*que *cchConnectStringBuffer*, la cadena de conexión completada en *wszOutConnectString* se trunca en *cchConnectStringBuffer* menos la longitud de un carácter de terminación nula.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o,SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Similar a [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) para cualquier error de validación de entrada, excepto que el Administrador de controladores usará un **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN y un **identificador** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Observaciones  
 El Administrador de controladores garantiza que el identificador HENV primario de *hDbc* y *hDbcInfoToken* son los mismos.  
  
 A diferencia de [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md), no hay ningún *argumento DriverCompletion* para solicitar a los usuarios que escriban información de conexión. No se permite un cuadro de diálogo de solicitud en el escenario de agrupación.  
  
 Las aplicaciones no deben llamar a esta función directamente. Un controlador ODBC que admite la agrupación de conexiones con reconocimiento de controladores debe implementar esta función.  
  
 Cada vez que un controlador devuelve SQL_ERROR o SQL_INVALID_HANDLE, el Administrador de controladores devuelve el error a la aplicación (en [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Cada vez que un controlador devuelve SQL_SUCCESS_WITH_INFO, el Administrador de controladores obtendrá la información de diagnóstico de *hDbcInfoToken*y devolverá SQL_SUCCESS_WITH_INFO a la aplicación en [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) y [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Cuando una aplicación utiliza [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md), *wszOutConnectString* será un búfer NULL (los tres últimos parámetros se establecerán en NULL, 0, NULL). De lo contrario, el controlador debe devolver la cadena de conexión de salida, que se devolverá a la llamada [sqlDriverConnect de](../../../odbc/reference/syntax/sqldriverconnect-function.md) la aplicación.  
  
 Incluya sqlspi.h para el desarrollo de controladores ODBC.  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollo de un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación de conexiones conscientes del conductor](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
