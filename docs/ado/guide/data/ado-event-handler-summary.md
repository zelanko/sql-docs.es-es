---
title: Resumen del controlador de eventos de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- event handlers [ADO]
ms.assetid: b34f4472-5e04-4a2c-ab64-38d6eca31a69
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4fef63ff610ad85e353c2ef1dc0f8e5987c74ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926197"
---
# <a name="ado-connection-and-recordset-events"></a>Conexión de ADO y eventos de conjunto de registros
Dos objetos ADO pueden provocar eventos: el [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto y el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. El **ConnectionEvent** familia pertenece a las operaciones en el **conexión** objeto y el **RecordsetEvent** familia pertenece a las operaciones en el  **Conjunto de registros** objeto.

-   **Eventos de conexión**: Los eventos se emiten cuando comienza una transacción en una conexión, se confirma o se revierte; Cuando un [comando](../../../ado/reference/ado-api/command-object-ado.md) ejecuta; cuando se produce una advertencia durante una **eventos de conexión** operación; o cuando un **conexión** se inicie o finalice.

-   **Eventos de conjunto de registros**: Los eventos se emiten en torno a las operaciones de captura asincrónico, así como al navegar por las filas de una **Recordset** de objetos, cambiar un campo de una fila de un **Recordset**, cambia una fila en un  **Conjunto de registros**, abra un **Recordset** con un cursor de servidor, cerrar un **Recordset**, o realizar cualquier cambio en el **Recordset**.

 Las tablas siguientes resumen los eventos y sus descripciones.

|ConnectionEvent|Descripción|
|---------------------|-----------------|
|[RollbackTransComplete BeginTransComplete, CommitTransComplete,](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**Administración de transacciones** -notificación de que ha iniciado la transacción actual en la conexión, confirmado o revertido.|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md), [ConnectComplete, desconectar](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**Administración de conexiones** -se ha iniciado la notificación que se iniciará la conexión actual, o ha finalizado.|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md), [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**Administración de la ejecución del comando** -notificación de que la ejecución del comando actual en la conexión se iniciará o ha finalizado.|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**Informativo** -notificación de que hay información adicional acerca de la operación actual.|

|RecordsetEvent|Descripción|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md), [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**Estado de recuperación** -notificación del progreso de una operación de recuperación de datos o que se ha completado la operación de recuperación. Estos eventos solo están disponibles si el **Recordset** se abrió mediante un cursor de cliente.|
|[WillChangeField, FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**Administración de cambios de campo** -notificación de que se cambia el valor del campo actual o se ha cambiado.|
|[Eventos WillMove, MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**Administración de navegación** -notificación de que la fila actual se coloque en un **Recordset** cambiará, ha cambiado o ha llegado al final de la **Recordset**.|
|[WillChangeRecord, RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**Administración de cambios de fila** -notificación de que algo en la fila actual de la **Recordset** se cambia o se ha cambiado.|
|[WillChangeRecordset, RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**Administración de cambios del conjunto de registros** -notificación de que algo en actual **Recordset** se cambia o se ha cambiado.|

## <a name="see-also"></a>Vea también
 [Creación de instancias de eventos de ADO por lenguaje](../../../ado/guide/data/ado-event-instantiation-by-language.md) [eventos de ADO](../../../ado/reference/ado-api/ado-events.md) [parámetros de evento](../../../ado/guide/data/event-parameters.md) [cómo funcionan conjuntamente los controladores de eventos](../../../ado/guide/data/how-event-handlers-work-together.md) [tipos de eventos](../../../ado/guide/data/types-of-events.md)
