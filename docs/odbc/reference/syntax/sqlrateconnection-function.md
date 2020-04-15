---
title: Función SQLRateConnection (Función) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRateConnection function [ODBC]
ms.assetid: e8da2ffb-d6ef-4ca7-824f-57afd29585d8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d29033460a7f89fc4a8b1c371a4d32bdf94a2a05
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288885"
---
# <a name="sqlrateconnection-function"></a>Función SQLRateConnection
**Conformidad**  
 Versión introducida: CUMPLIMIENTO de estándares ODBC 3.81: ODBC  
  
 **Resumen**  
 **SQLRateConnection** determina si un controlador puede reutilizar una conexión existente en el grupo de conexiones.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hSolicitud*  
 [Entrada] Identificador de token que representa la nueva solicitud de conexión de aplicación.  
  
 *hCandidateConnection*  
 [Entrada] La conexión existente en el grupo de conexiones. La conexión debe estar en un estado abierto.  
  
 *fRequiredTransactionEnlistment*  
 [Entrada] Si es TRUE, reutilizar *hCandidateConnection* de la conexión existente para la nueva solicitud de conexión (*hRequest*) requiere una inscripción adicional.  
  
 *transId*  
 [Entrada] Si *fRequiredTransactionEnlistment* es TRUE, *transId* representa la transacción DTC que se dará de alta la solicitud. Si *fRequiredTransactionEnlistment* es FALSE, *transId* se omitirá.  
  
 *pRating*  
 [Salida] *hCandidateConnection*'s reuse rating for the *hRequest*. Esta calificación estará entre 0 y 100 (incluido).  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 El Administrador de controladores no procesará la información de diagnóstico devuelta desde esta función.  
  
## <a name="remarks"></a>Observaciones  
 **SQLRateConnection** genera una puntuación entre 0 y 100 (incluido) que indica qué tan bien coincide una conexión existente con la solicitud.  
  
|Score|Significado (cuando se devuelve SQL_SUCCESS)|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection* no se debe reutilizar para *hRequest*.|  
|Cualquier valor entre 1 y 98 (incluido)|Cuanto mayor sea la puntuación, más cerca coincidirá *hCandidateConnection* con *hRequest*.|  
|99|Sólo hay discrepancias en atributos insignificantes.  El Administrador de controladores debe detener el bucle de clasificación.|  
|100|Coincidencia perfecta.  El Administrador de controladores debe detener el bucle de clasificación.|  
|Cualquier otro valor mayor que 100|*hCandidateConnection* se marca como dead y no se reutilizará incluso en una solicitud de conexión futura.|  
  
 El Administrador de controladores marcará una conexión como muerta si el código de retorno es algo distinto de SQL_SUCCESS (incluido SQL_SUCCESS_WITH_INFO) o la calificación es mayor que 100. Esa conexión muerta no se reutilizará (incluso en futuras solicitudes de conexión) y, finalmente, se agotará el tiempo de espera después de que pasen CPTimeout. El Administrador de controladores seguirá encontrando otra conexión desde el grupo para calificar.  
  
 Si el Administrador de controladores reutilizó una conexión cuya puntuación es estrictamente menor que 100 (incluido 99), el Administrador de controladores llamará a SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN) para restablecer la conexión al estado solicitado por la aplicación. El controlador no debe restablecer la conexión en esta llamada de función.  
  
 Si *fRequiredTransactionEnlistment* es TRUE, la reutilización de *hCandidateConnection* necesita una inscripción adicional (*transId* !- NULL) o unenlistment (*transId* - NULL). Esto indica el costo de reutilizar una conexión y si el controlador debe dar de alta / anular la lista de la conexión si va a reutilizar la conexión. Si *fRequireTransactionEnlistment* es FALSE, el controlador debe omitir el valor de *transId*.  
  
 El Administrador de controladores garantiza que el identificador HENV primario de *hRequest* y *hCandidateConnection* son los mismos. El Administrador de controladores garantiza que el identificador de grupo asociado a *hRequest* y *hCandidateConnection* son los mismos.  
  
 Las aplicaciones no deben llamar a esta función directamente. Un controlador ODBC que admite la agrupación de conexiones con reconocimiento de controladores debe implementar esta función.  
  
 Incluya sqlspi.h para el desarrollo de controladores ODBC.  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollo de un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación de conexiones conscientes del conductor](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
