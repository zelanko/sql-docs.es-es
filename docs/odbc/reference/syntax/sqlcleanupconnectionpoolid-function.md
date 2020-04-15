---
title: Función SQLCleanupConnectionPoolID ?? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301325"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>Función SQLCleanupConnectionPoolID
**Conformidad**  
 Versión introducida: CUMPLIMIENTO de estándares ODBC 3.81: ODBC  
  
 **Resumen**  
 **SQLCleanupConnectionPoolID** informa a un controlador de que se ha agotado el tiempo de espera de un identificador de grupo. Un identificador de grupo puede agotar el tiempo de espera siempre que se adelante el tiempo de espera de todas las conexiones de un grupo asociado a ese identificador de grupo. Consulte [Agrupación en los componentes](https://msdn.microsoft.com/library/ms810829.aspx) de Microsoft Data Access para obtener más información sobre el tiempo de espera de conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 [Entrada] El identificador de entorno del grupo.  
  
 *PoolID*  
 [Entrada] El grupo asociado al identificador del grupo que se adelantó.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 El Administrador de controladores no procesará la información de diagnóstico devuelta desde **SQLCleanupConnectionPoolID**.  
  
 Una aplicación no puede recibir el mensaje de error devuelto por el controlador.  
  
## <a name="remarks"></a>Observaciones  
 **SQLCleanupConnectionPoolID** se puede llamar en cualquier momento, pero el Administrador de controladores garantiza que ningún otro subproceso está llamando simultáneamente **sqlGetPoolID** y ningún otro subproceso llama simultáneamente **SQLRateConnection** y **SQLPoolConnect** con un token de información de conexión asignado con ese identificador de grupo. Por lo tanto, el controlador debe asegurarse de que esta función es segura para subprocesos.  
  
 Un controlador puede limpiar los recursos asociados con el identificador del grupo.  
  
 Las aplicaciones no deben llamar a esta función directamente. Un controlador ODBC que admite la agrupación de conexiones con reconocimiento de controladores debe implementar esta función.  
  
 Incluya sqlspi.h para el desarrollo de controladores ODBC.  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollo de un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación de conexiones conscientes del conductor](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
