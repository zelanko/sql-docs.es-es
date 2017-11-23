---
title: "Función SQLRateConnection | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLRateConnection function [ODBC]
ms.assetid: e8da2ffb-d6ef-4ca7-824f-57afd29585d8
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87657a0c0444c6de869cc30e5bcd98db5551be95
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlrateconnection-function"></a>SQLRateConnection (función)
**Conformidad**  
 Versión introdujo: ODBC 3,81 normativas: ODBC  
  
 **Resumen**  
 **SQLRateConnection** determina si un controlador puede reutilizar una conexión existente en la agrupación de conexiones.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hRequest*  
 [Entrada] Un identificador del token que representa la nueva solicitud de conexión de la aplicación.  
  
 *hCandidateConnection*  
 [Entrada] La conexión existente en la agrupación de conexiones. La conexión debe estar en un estado abierto.  
  
 *fRequiredTransactionEnlistment*  
 [Entrada] Si es TRUE, reutiliza la conexión existente *hCandidateConnection* para la nueva solicitud de conexión (*hRequest*) requiere una inscripción adicional.  
  
 *Id*  
 [Entrada] Si *fRequiredTransactionEnlistment* es TRUE, *ID* representa la transacción de DTC se inscribirá la solicitud. Si *fRequiredTransactionEnlistment* es FALSE, *ID* se pasará por alto.  
  
 *pRating*  
 [Salida] *hCandidateConnection*reutilización de clasificación para el *hRequest*. Esta valoración estará entre 0 y 100 (ambos incluidos).  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 El Administrador de controladores no procesará la información de diagnóstico que devuelve esta función.  
  
## <a name="remarks"></a>Comentarios  
 **SQLRateConnection** genera una puntuación de entre 0 y 100 (ambos incluidos) que indica el grado en que una conexión existente coincide con la solicitud.  
  
|Puntuación|Significado (cuando se devuelve SQL_SUCCESS)|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection* no debe utilizarse para la *hRequest*.|  
|Cualquier valor entre 1 y 98 (inclusive)|Cuanto mayor sea la puntuación, cuanto más se acerque que *hCandidateConnection* coincide con *hRequest*.|  
|99|Hay solo discrepancias en los atributos no significativos.  El Administrador de controladores debe detener el bucle de clasificación.|  
|100|Coincidencia exacta.  El Administrador de controladores debe detener el bucle de clasificación.|  
|Cualquier valor mayor que 100|*hCandidateConnection* está marcado como inactivas y no se reutilizará incluso en una solicitud de conexión futuras.|  
  
 El Administrador de controladores se marca una conexión como inactivas si el código de retorno es algo distinto de SQL_SUCCESS (incluidos SQL_SUCCESS_WITH_INFO) o la clasificación es superior a 100. Esa conexión inactiva no se reutilizará (incluso en las solicitudes de conexión futuras) y se finalmente se agotó el tiempo después de que pase CPTimeout. El Administrador de controladores seguirá encontrando otra conexión desde el grupo con frecuencia.  
  
 Si el Administrador de controladores se reutiliza una conexión cuya puntuación es estrictamente menor que 100 (incluyendo 99), el Administrador de controladores llamará a SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN) para restablecer la conexión en el estado solicitado por la aplicación. El controlador no debe restablecer la conexión en esta llamada a función.  
  
 Si *fRequiredTransactionEnlistment* es TRUE, reutilizar *hCandidateConnection* necesita una inscripción adicional (*ID* ! = NULL) o unenlistment ( *ID* == NULL). Esto indica que el costo de reutilización de una conexión y si el controlador debe dar de alta / dar de baja la conexión si se va a reutilizar la conexión. Si *fRequireTransactionEnlistment* es FALSE, controlador debe pasar por alto el valor de *ID*.  
  
 El Administrador de controladores garantiza que el elemento primario HENV controlar de *hRequest* y *hCandidateConnection* son los mismos. El Administrador de controladores garantiza que el identificador del grupo asociado *hRequest* y *hCandidateConnection* son los mismos.  
  
 Las aplicaciones no deben llamar directamente a esta función. Un controlador ODBC que admite la agrupación de conexiones dependientes del controlador debe implementar esta función.  
  
 Incluir sqlspi.h para el desarrollo del controlador ODBC.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación de conexiones dependientes del controlador](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
