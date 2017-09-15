---
title: Resumen del controlador de eventos de ADO | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- events [ADO], about event handlers
- event handlers [ADO]
ms.assetid: b34f4472-5e04-4a2c-ab64-38d6eca31a69
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0cd8bf7593fb1e8c770edde83e697f5b5be1d1d3
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="ado-connection-and-recordset-events"></a>Conexión ADO y los eventos de conjunto de registros
Dos objetos ADO pueden provocar eventos: el [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto y el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. El **ConnectionEvent** familia pertenece a las operaciones en el **conexión** objeto y el **RecordsetEvent** familia pertenece a las operaciones en el ** Conjunto de registros** objeto.

-   **Eventos de conexión**: eventos se emiten cuando comienza, se confirma o se revierte atrás; si una transacción en una conexión un [comando](../../../ado/reference/ado-api/command-object-ado.md) ejecuta; cuando se produce una advertencia durante una **el evento de conexión**operación; o cuando un **conexión** se inicie o finalice.

-   **Eventos de conjunto de registros**: eventos se emiten alrededor de las operaciones de búsqueda asincrónica, así como al navegar a través de las filas de un **Recordset** de objetos, cambiar un campo de una fila de un **Recordset**, cambia una fila en un **Recordset**, abra un **Recordset** con un cursor de servidor, cierre una **Recordset**, o realizar cualquier cambio en el ** Conjunto de registros**.

 Las tablas siguientes resumen los eventos y sus descripciones.

|ConnectionEvent|Description|
|---------------------|-----------------|
|[RollbackTransComplete BeginTransComplete, CommitTransComplete,](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**Administración de transacciones** : notificación de que ha iniciado la transacción actual en la conexión, confirmar o revertir.|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md), [ConnectComplete, desconectar](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**Administración de conexiones** : notificación de que se iniciará la conexión actual, se ha iniciado o ha finalizado.|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md), [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**Administración de la ejecución del comando** : notificación de que la ejecución del comando actual en la conexión se iniciará o ha finalizado.|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**Informativo** : notificación de que no hay información adicional sobre la operación actual.|

|RecordsetEvent|Description|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md), [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**Estado de recuperación** : notificación del progreso de una operación de recuperación de datos o que se ha completado la operación de recuperación. Estos eventos solo están disponibles si el **Recordset** se abrió mediante un cursor de cliente.|
|[WillChangeField, FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**Administración de cambios de campo** : notificación de que el valor del campo actual cambiará o ha cambiado.|
|[WillMove, MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**Administración de navegación** : notificación de que la fila actual se coloque en un **Recordset** cambiará, ha cambiado o ha llegado al final de la **conjunto de registros**.|
|[WillChangeRecord, RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**Administración de los cambios de fila** : notificación de que algo en la fila actual de la **Recordset** cambiará o ha cambiado.|
|[WillChangeRecordset, RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**Administración de cambios del conjunto de registros** : notificación de que algo en la actual **Recordset** cambiará o ha cambiado.|

## <a name="see-also"></a>Vea también
 [Creación de instancias de eventos de ADO según el lenguaje](../../../ado/guide/data/ado-event-instantiation-by-language.md) [eventos de ADO](../../../ado/reference/ado-api/ado-events.md) [parámetros de evento](../../../ado/guide/data/event-parameters.md) [cómo funcionan conjuntamente los controladores de eventos](../../../ado/guide/data/how-event-handlers-work-together.md) [tipos de eventos](../../../ado/guide/data/types-of-events.md)

