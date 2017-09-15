---
title: "Función SQLGetPoolID | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c8db01749cf58e34c59294367b3e24105906b635
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetpoolid-function"></a>SQLGetPoolID (función)
**Conformidad**  
 Versión introdujo: ODBC 3,81 normativas: ODBC  
  
 **Resumen**  
 **SQLGetPoolID** recupera el identificador de grupo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hDbcInfoToken*  
 [Entrada] Identificador del token que contiene toda la información de conexión.  
  
 *pPoolID*  
 [Salida] El identificador del grupo, que se usa para identificar un conjunto de conexiones que se pueden usar indistintamente (posiblemente, lo que requiere un reinicio adicional).  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetPoolID** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, el Administrador de controladores se usará un **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN y un **controlar** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentarios  
 **SQLGetPoolID** se utiliza para obtener el identificador del grupo dado un conjunto de información de conexión (de **SQLSetConnectAttrForDbcInfo**, **SQLSetDriverConnectInfo**, y ** SQLSetConnectInfo**). Este grupo de identificador se usa para identificar un conjunto de conexiones que se pueden usar indistintamente (posiblemente, lo que requiere un reinicio adicional). El identificador del grupo se utilizará para identificar el grupo de conexiones para el grupo de conexiones.  
  
 Cada vez que un controlador devuelve SQL_ERROR o SQL_INVALID_HANDLE, el Administrador de controladores devuelve el error a la aplicación (en [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Cada vez que un controlador devuelve SQL_SUCCESS_WITH_INFO, el Administrador de controladores obtendrá la información de diagnóstico de *hDbcInfoToken*y devuelve SQL_SUCCESS_WITH_INFO para la aplicación en [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)y [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Las aplicaciones no deben llamar directamente a esta función. Un controlador ODBC que admite la agrupación de conexiones dependientes del controlador debe implementar esta función.  
  
 Incluir sqlspi.h para el desarrollo del controlador ODBC.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación de conexiones dependientes del controlador](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
