---
title: Evento ExecuteComplete (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- ExecuteComplete event [ADO]
ms.assetid: 62470d42-e511-494c-bec4-ad4591734b7b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0af3666e4f5aecf897bdd6b93f756c2d251fa40
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278174"
---
# <a name="executecomplete-event-ado"></a>Evento ExecuteComplete (ADO)
El **ExecuteComplete** eventos se llama después de que un comando ha terminado de ejecutarse.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *RecordsAffected*  
 A **largo** valor que indica el número de registros afectados por el comando.  
  
 *pError*  
 Un [Error](../../../ado/reference/ado-api/error-object.md) objeto. Describe el error que se ha producido si el valor de **adStatus** es **adStatusErrorsOccurred**; en caso contrario, no se establece.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado. Cuando se llama a este evento, este parámetro se establece en **adStatusOK** si la operación que provocó el evento se realizó correctamente, o para **adStatusErrorsOccurred** si la operación produce un error.  
  
 Antes de que se devuelve este evento, establezca este parámetro en **adStatusUnwantedEvent** para impedir notificaciones posteriores.  
  
 *pCommand*  
 El [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que se ejecutó. Contiene un **comando** objeto incluso cuando se llama a **Connection.Execute** o **Recordset.Open** sin crear explícitamente un **comando** , en cuyo caso el **comando** ADO crea internamente el objeto.  
  
 *pRecordset*  
 A [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto que es el resultado del comando ejecutado. Esto **Recordset** puede estar vacío. Nunca se debe destruir este objeto de conjunto de registros desde este controlador de eventos. Si lo hace, se producirá una infracción de acceso cuando ADO intenta obtener acceso a un objeto que ya no existe.  
  
 *pConnection*  
 A [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto. La conexión en la que se ejecutó la operación.  
  
## <a name="remarks"></a>Notas  
 Un **ExecuteComplete** evento puede ocurrir debido a la **conexión.** [Ejecutar](../../../ado/reference/ado-api/execute-method-ado-connection.md), **comando.** [Ejecutar](../../../ado/reference/ado-api/execute-method-ado-command.md), **Recordset.** [Abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md), **Recordset.** [Requery](../../../ado/reference/ado-api/requery-method.md), o **Recordset.** [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md) métodos.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)
