---
title: Función SQLGetPoolID | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9fc6737530fdf151573a570eb83f777785ddb679
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/11/2019
ms.locfileid: "65538079"
---
# <a name="sqlgetpoolid-function"></a>Función SQLGetPoolID
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 3,81 de ODBC: ODBC  
  
 **Resumen**  
 **SQLGetPoolID** recupera el identificador de grupo.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hDbcInfoToken*  
 [Entrada] Identificador del token que contiene toda la información de conexión.  
  
 *pPoolID*  
 [Salida] El identificador de grupo, que se usa para identificar un conjunto de conexiones que se pueden usar indistintamente (que posiblemente necesite un reinicio adicional).  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetPoolID** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, el Administrador de controladores se usará un **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN y un **controlar** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentarios  
 **SQLGetPoolID** se utiliza para obtener el identificador del grupo dado un conjunto de información de conexión (desde **SQLSetConnectAttrForDbcInfo**, **SQLSetDriverConnectInfo**, y  **SQLSetConnectInfo**). Este identificador se usa para identificar un conjunto de conexiones que se pueden usar indistintamente de grupo (que posiblemente necesite un reinicio adicional). El identificador del grupo se usará para identificar el grupo de conexiones para el grupo de conexiones.  
  
 Cada vez que un controlador devuelve SQL_ERROR o SQL_INVALID_HANDLE, el Administrador de controladores devuelve el error a la aplicación (en [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Cada vez que un controlador devuelve SQL_SUCCESS_WITH_INFO, el Administrador de controladores obtendrá la información de diagnóstico de *hDbcInfoToken*y devuelvan SQL_SUCCESS_WITH_INFO a la aplicación en [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)y [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Las aplicaciones no deben llamar directamente a esta función. Un controlador ODBC que admite la agrupación de conexiones dependientes del controlador debe implementar esta función.  
  
 Incluir sqlspi.h para el desarrollo de controladores ODBC.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación de conexiones dependientes del controlador](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
