---
title: Eventos de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
ms.assetid: 0ded5ad9-8f83-4224-95af-38512783b972
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 50bdb3117b01d68f03208d6db501d44f05a849ce
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044888"
---
# <a name="ado-events"></a>Eventos de ADO

|||  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Se llama después de la **BeginTrans** operación.|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Se llama después de la **CommitTrans** operación.|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Se llama después de iniciar una conexión.|  
|[Desconectar](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Se llama después de que finalice una conexión.|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|Se llama cuando hay un intento de mover una fila más allá del final de la **Recordset**.|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|Se llama después de un comando ha terminado de ejecutarse.|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|Se llama después de que se han recuperado todos los registros de una operación asincrónica prolongada en el **Recordset**.|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|Se llama periódicamente durante una operación asincrónica prolongada para informar de cuántas filas se han recuperado actualmente en el **Recordset**.|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Se llama después el valor de uno o varios **campo** objetos ha cambiado.|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|Se llama siempre que se produce una advertencia durante una **ConnectionEvent** operación.|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Se llama después de la posición actual en el **Recordset** cambios.|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Se llama después de cambiar uno o más registros.|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Se llama después de la **Recordset** ha cambiado.|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Se llama después de la **RollbackTrans** operación.|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Se llama antes de una operación pendiente cambie el valor de uno o varios **campo** objetos en el **Recordset**.|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Se llama antes de uno o más registros (filas) el **Recordset** cambiar.|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Se llama antes de una operación pendiente cambie el **Recordset**.|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|Se llama antes de iniciar una conexión.|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|Se llama justo antes de que un comando pendiente en esta conexión se ejecuta y ofrece al usuario una oportunidad para examinar y modificar los parámetros de ejecución pendiente.|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|El **WillMove** se llama al evento *antes* una operación pendiente cambia la posición actual en el **Recordset**.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de API de ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Colecciones de ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas de ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apéndice B: Errores de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Control de eventos de ADO](../../../ado/guide/data/handling-ado-events.md)   
 [Métodos de ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objetos ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfaces y los objetos ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propiedades de ADO](../../../ado/reference/ado-api/ado-properties.md)
