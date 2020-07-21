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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a74a92cc05ecd41e99ff87642c7fe3ee527e0c98
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301325"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>Función SQLCleanupConnectionPoolID
**Conformidad**  
 Versión introducida: ODBC 3,81 Standards Compliance: ODBC  
  
 **Resumen**  
 **SQLCleanupConnectionPoolID** informa a un controlador de que se ha agotado el tiempo de espera de un ID. de grupo. Un identificador de grupo puede agotar el tiempo de espera cada vez que se agota el tiempo de espera de todas las conexiones de un grupo asociado a ese ID. de grupo. Consulte [agrupación en Microsoft Data Access Components](https://msdn.microsoft.com/library/ms810829.aspx) para obtener más información sobre el tiempo de espera de la conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 Entradas Identificador de entorno del grupo.  
  
 *PoolID*  
 Entradas El grupo asociado al identificador de grupo que agotó el tiempo de espera.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 El administrador de controladores no procesará la información de diagnóstico devuelta desde **SQLCleanupConnectionPoolID**.  
  
 Una aplicación no puede recibir el mensaje de error devuelto por el controlador.  
  
## <a name="remarks"></a>Observaciones  
 Se puede llamar a **SQLCleanupConnectionPoolID** en cualquier momento, pero el administrador de controladores garantiza que ningún otro subproceso llama a **SQLGetPoolID** simultáneamente y ningún otro subproceso está llamando a **SQLRateConnection** y **SQLPoolConnect** de forma simultánea con un token de información de conexión asignado a ese ID. de grupo. Por lo tanto, el controlador debe asegurarse de que esta función es segura para subprocesos.  
  
 Un controlador puede limpiar los recursos asociados con el identificador del grupo.  
  
 Las aplicaciones no deben llamar directamente a esta función. Un controlador ODBC que admita la agrupación de conexiones compatible con controladores debe implementar esta función.  
  
 Incluya sqlspi. h para el desarrollo del controlador ODBC.  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación de conexiones compatible con controladores](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
