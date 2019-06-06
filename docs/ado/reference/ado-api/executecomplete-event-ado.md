---
title: Evento ExecuteComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- ExecuteComplete event [ADO]
ms.assetid: 62470d42-e511-494c-bec4-ad4591734b7b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: df6437e80ab746a7d6aa219fb3299cb54712b5c3
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697908"
---
# <a name="executecomplete-event-ado"></a>Evento ExecuteComplete (ADO)
El **ExecuteComplete** se llama al evento después de un comando ha terminado de ejecutarse.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *RecordsAffected*  
 Un **largo** valor que indica el número de registros afectados por el comando.  
  
 *pError*  
 Un [Error](../../../ado/reference/ado-api/error-object.md) objeto. Describe el error producido si el valor de **adStatus** es **adStatusErrorsOccurred**; en caso contrario, no se establece.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado. Cuando se llama a este evento, este parámetro se establece en **adStatusOK** si la operación que provocó el evento se realizó correctamente, o para **adStatusErrorsOccurred** si la operación produjo un error.  
  
 Antes de que se devuelve este evento, establezca este parámetro en **adStatusUnwantedEvent** para evitar notificaciones posteriores.  
  
 *pCommand*  
 El [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que se ha ejecutado. Contiene un **comando** objeto incluso cuando se llama a **Connection.Execute** o **Recordset.Open** sin crear explícitamente un **comando** , en cuyo caso el **comando** ADO crea internamente el objeto.  
  
 *pRecordset*  
 Un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto que es el resultado del comando ejecutado. Esto **Recordset** puede estar vacío. Nunca debe destruir este objeto de conjunto de registros desde dentro de este controlador de eventos. Si lo hace, se producirá una infracción de acceso cuando ADO intenta tener acceso a un objeto que ya no existe.  
  
 *pConnection*  
 Un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto. La conexión en la que se ejecutó la operación.  
  
## <a name="remarks"></a>Comentarios  
 Un **ExecuteComplete** evento puede producirse debido a la **conexión.** [Ejecutar](../../../ado/reference/ado-api/execute-method-ado-connection.md), **comando.** [Ejecutar](../../../ado/reference/ado-api/execute-method-ado-command.md), **Recordset.** [Abierto](../../../ado/reference/ado-api/open-method-ado-recordset.md), **Recordset.** [Requery](../../../ado/reference/ado-api/requery-method.md), o **Recordset.** [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md) métodos.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)
