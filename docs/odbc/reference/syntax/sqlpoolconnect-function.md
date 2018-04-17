---
title: Función SQLPoolConnect | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 130c39d4aab986b5053192d2fe2c548e89ccef2e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect (función)
**Conformidad**  
 Versión introdujo: ODBC 3.8 normativas: ODBC  
  
 **Resumen**  
 **SQLPoolConnect** se utiliza para crear una nueva conexión si no se puede reutilizar conexión en el grupo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SQLRETURN  SQLPoolConnect(  
                SQLHDBC              hDbc,  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              wszOutConnectString,  
                SQLSMALLINT          cchConnectStringBuffer,  
                SQLSMALLINT *        cchConnectStringLen );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hDbc*  
 [Entrada] El identificador de conexión.  
  
 *hDbcInfoToken*  
 [Entrada] El identificador del token para la nueva solicitud de conexión de la aplicación.  
  
 *wszOutConnectString*  
 [Salida] Puntero a un búfer para la cadena de conexión completa. Tras una conexión correcta con el origen de datos de destino, este búfer contiene la cadena de conexión completa. Las aplicaciones deben asignar al menos de 1.024 caracteres para este búfer.  
  
 Si *wszOutConnectString* es NULL, *cchConnectStringLen* devolverá el número total de caracteres (excepto el carácter de terminación null para los datos de carácter) disponible para devolver en el búfer señalado por *wszOutConnectString*.  
  
 *cchConnectStringBuffer*  
 [Entrada] Longitud de la **wszOutConnectString* búfer en caracteres.  
  
 *cchConnectStringLen*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de caracteres (excepto el carácter de terminación null) disponible para devolver en \* *wszOutConnectString*. Si el número de caracteres disponibles para devolver es mayor o igual que *cchConnectStringBuffer*, el completado de la cadena de conexión en \* *wszOutConnectString* se trunca a *cchConnectStringBuffer* menos la longitud de un carácter de terminación null.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Similar a [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) para cualquier error de validación de entrada salvo que va a usar el Administrador de controladores un **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN y un **controlar** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentarios  
 El Administrador de controladores garantiza que el elemento primario HENV controlar de *hDbc* y *hDbcInfoToken* son los mismos.  
  
 A diferencia de [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md), no hay ningún *DriverCompletion* argumento pasado a pedir a los usuarios para escribir la información de conexión. Un cuadro de diálogo de solicitud no está permitida en el escenario de agrupación.  
  
 Las aplicaciones no deben llamar directamente a esta función. Un controlador ODBC que admite la agrupación de conexiones dependientes del controlador debe implementar esta función.  
  
 Cada vez que un controlador devuelve SQL_ERROR o SQL_INVALID_HANDLE, el Administrador de controladores devuelve el error a la aplicación (en [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Cada vez que un controlador devuelve SQL_SUCCESS_WITH_INFO, el Administrador de controladores obtendrá la información de diagnóstico de *hDbcInfoToken*y devuelve SQL_SUCCESS_WITH_INFO para la aplicación en [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)y [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Cuando una aplicación usa [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md), *wszOutConnectString* será un búfer nulo (los tres últimos parámetros todos se establecerá en NULL, 0, NULL). En caso contrario, el controlador debe devolver la cadena de conexión de salida, que volverá a la aplicación [función SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) llamar.  
  
 Incluir sqlspi.h para el desarrollo del controlador ODBC.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación de conexiones dependientes del controlador](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
