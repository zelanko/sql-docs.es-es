---
title: Función SQLCleanupConnectionPoolID | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCleanupConnectionPoolID function [ODBC]
ms.assetid: 1fc61908-e003-4587-b91a-32f40569fb99
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce48e7aa89451131b7ed483fa5132af22565c170
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51673554"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>Función SQLCleanupConnectionPoolID
**Conformidad**  
 Versión introdujo: ODBC 3,81 normativo: ODBC  
  
 **Resumen**  
 **SQLCleanupConnectionPoolID** informa a un controlador que se agotó un Id. de grupo. Un grupo de identificador puede tiempo de espera siempre que todas las conexiones en un grupo asociado con ese Id. de grupo eran agotó el tiempo de espera. Consulte [agrupación en el Microsoft Data Access Components](https://msdn.microsoft.com/library/ms810829.aspx) para obtener más información sobre el tiempo de espera de conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 [Entrada] El identificador del entorno del grupo.  
  
 *PoolID*  
 [Entrada] El grupo asociado al identificador de grupo que se ha agotado.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 El Administrador de controladores no procesará la información de diagnóstico devuelto desde **SQLCleanupConnectionPoolID**.  
  
 Una aplicación no puede recibir el mensaje de error devuelto por el controlador.  
  
## <a name="remarks"></a>Comentarios  
 **SQLCleanupConnectionPoolID** puede llamarse en cualquier momento, pero el Administrador de controladores garantiza que ningún otro subproceso llama al mismo tiempo **SQLGetPoolID** y ningún otro subproceso llama al mismo tiempo  **SQLRateConnection** y **SQLPoolConnect** con un token de la información de conexión asignado con ese identificador de grupo. Por lo tanto, el controlador debe asegurarse de que esta función es segura para subprocesos.  
  
 Un controlador puede limpiar los recursos asociados con el identificador de grupo.  
  
 Las aplicaciones no deben llamar directamente a esta función. Un controlador ODBC que admite la agrupación de conexiones dependientes del controlador debe implementar esta función.  
  
 Incluir sqlspi.h para el desarrollo de controladores ODBC.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación de conexiones dependientes del controlador](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
