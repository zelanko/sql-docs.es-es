---
title: Eventos de ADO | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- events [ADO]
- ADO, events
ms.assetid: 0ded5ad9-8f83-4224-95af-38512783b972
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 59492bb63fd11aa1c60b3c45daed5a7431475cd9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="ado-events"></a>Eventos de ADO
|||  
|-|-|  
|[Eventos BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Llamado después de la **BeginTrans** operación.|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Llamado después de la **CommitTrans** operación.|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Se llama después de iniciarse una conexión.|  
|[Desconectar](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Se llama después de que finalice una conexión.|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|Se llama cuando hay un intento para desplazarse a una fila más allá del final de la **conjunto de registros**.|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|Se llama después de que un comando ha terminado de ejecutarse.|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|Se llama después de recuperar todos los registros en una operación asincrónica prolongada en el **conjunto de registros**.|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|Llama periódicamente durante una operación asincrónica prolongada para informar de cuántas filas se han recuperado actualmente en el **conjunto de registros**.|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Llamado después del valor de uno o varios **campo** objetos ha cambiado.|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|Llama cada vez que se produce una advertencia durante una **ConnectionEvent** operación.|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Llamado después de la posición actual en el **Recordset** cambios.|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Se llama después de cambiar uno o más registros.|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Llamado después de la **Recordset** ha cambiado.|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Llamado después de la **RollbackTrans** operación.|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Se llama antes de que una operación pendiente cambie el valor de uno o varios **campo** objetos en el **conjunto de registros**.|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Llamado antes de uno o más registros (filas) el **Recordset** cambiar.|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Se llama antes de que una operación pendiente cambie el **conjunto de registros**.|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|Se llama antes de iniciarse una conexión.|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|Se llama justo antes de que un comando pendiente se ejecute en esta conexión y ofrece al usuario una oportunidad para examinar y modificar los parámetros de ejecución pendiente.|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|El **WillMove** se llama al evento *antes de* una operación pendiente cambie la posición actual en el **conjunto de registros**.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Colecciones de ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas de ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apéndice B: errores de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Control de eventos de ADO](../../../ado/guide/data/handling-ado-events.md)   
 [Métodos de ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objetos ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfaces y los objetos ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propiedades de ADO](../../../ado/reference/ado-api/ado-properties.md)

