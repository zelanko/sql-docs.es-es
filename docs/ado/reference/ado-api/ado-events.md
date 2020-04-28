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
ms.openlocfilehash: 35169313ae487514403f62c8e6d1ba2c262cb8a7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921006"
---
# <a name="ado-events"></a>Eventos de ADO

|||  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Se llama después de la operación **BeginTrans** .|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Se llama después de la operación **CommitTrans** .|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Se llama después de que se inicie una conexión.|  
|[Conecto](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Se llama después de que finalice una conexión.|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|Se llama cuando se intenta moverse a una fila más allá del final del conjunto de **registros**.|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|Se llama después de que se haya terminado de ejecutar un comando.|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|Se llama después de que todos los registros de una operación asincrónica larga se hayan recuperado en el **conjunto de registros**.|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|Se llama periódicamente durante una operación asincrónica larga para informar del número de filas que se han recuperado actualmente en el **conjunto de registros**.|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Se llama después de cambiar el valor de uno o más objetos **Field** .|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|Se llama siempre que se produce una advertencia durante una operación **ConnectionEvent** .|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Se llama después de que cambie la posición actual del **conjunto de registros** .|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Se llama después de que uno o varios registros cambien.|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Se llama después de que el **conjunto de registros** haya cambiado.|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Se llama después de la operación **RollbackTrans** .|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Se llama antes de que una operación pendiente cambie el valor de uno o más objetos de **campo** en el **conjunto de registros**.|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Se llama antes de que se cambien uno o más registros (filas) del **conjunto de registros** .|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Se llama antes de que una operación pendiente cambie el **conjunto de registros**.|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|Se llama antes de que se inicie una conexión.|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|Se llama justo antes de que un comando pendiente se ejecute en esta conexión y permite al usuario examinar y modificar los parámetros de ejecución pendientes.|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Se **WillMove** llama al evento WillMove *antes* de que una operación pendiente cambie la posición actual en el **conjunto de registros**.|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API de ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Colecciones de ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas de ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apéndice B: errores de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Controlar eventos de ADO](../../../ado/guide/data/handling-ado-events.md)   
 [Métodos de ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objetos ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Objetos e interfaces de ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propiedades de ADO](../../../ado/reference/ado-api/ado-properties.md)
