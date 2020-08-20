---
description: Eventos Connection y Recordset de ADO
title: Resumen del controlador de eventos ADO | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 92d1dcd202c4e115cda4198f90e3410c2cb44319
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453847"
---
# <a name="ado-connection-and-recordset-events"></a>Eventos Connection y Recordset de ADO
Dos objetos ADO pueden generar eventos: el objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) y el objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) . La familia **ConnectionEvent** pertenece a las operaciones en el objeto de **conexión** y la familia **RecordsetEvent** pertenece a las operaciones en el objeto de conjunto de **registros** .

-   **Eventos de conexión**: los eventos se emiten cuando se inicia una transacción en una conexión, se confirma o se revierte. Cuando se ejecuta un [comando](../../../ado/reference/ado-api/command-object-ado.md) ; Cuando se produce una advertencia durante una operación de **evento de conexión** ; o cuando se inicia o finaliza una **conexión** .

-   **Eventos de conjunto de registros**: los eventos se emiten en torno a las operaciones de captura asincrónicas y al navegar por las filas de un objeto de **conjunto de registros** , cambiar un campo de una fila de un **conjunto**de registros, cambiar una fila de un **conjunto de registros**, abrir un conjunto de **registros** con un cursor de servidor, cerrar un **conjunto de registros**o realizar cualquier cambio en el **conjunto**

 En las tablas siguientes se resumen los eventos y sus descripciones.

|ConnectionEvent|Descripción|
|---------------------|-----------------|
|[BeginTransComplete, CommitTransComplete, RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**Administración de transacciones** : notificación de que la transacción actual en la conexión se ha iniciado, confirmado o revertido.|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md), [ConnectComplete, Disconnect](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**Administración de conexiones** : notificación de que la conexión actual se inicia, se ha iniciado o ha finalizado.|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md), [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**Administración de ejecución de comandos** : notificación de que la ejecución del comando actual en la conexión se iniciará o ha finalizado.|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**Informativo** : notificación de que hay información adicional sobre la operación actual.|

|RecordsetEvent|Descripción|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md), [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**Estado de recuperación** : notificación del progreso de una operación de recuperación de datos o de que se ha completado la operación de recuperación. Estos eventos solo están disponibles si el **conjunto de registros** se ha abierto con un cursor del lado cliente.|
|[WillChangeField, FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**Administración de cambios de campo** : notificación de que el valor del campo actual cambiará o ha cambiado.|
|[WillMove, MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**Administración de navegación** : notificación de que la posición de la fila actual en un **conjunto de registros** cambia, ha cambiado o ha alcanzado el final del **conjunto de registros**.|
|[WillChangeRecord, RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**Administración de cambios de fila** : notificación de que un elemento de la fila actual del **conjunto de registros** cambiará o ha cambiado.|
|[WillChangeRecordset, RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**Administración de cambios de conjunto de registros** : notificación de que un elemento del **conjunto de registros** actual cambiará o ha cambiado.|

## <a name="see-also"></a>Consulte también
 [Creación de instancias de eventos de ADO con](../../../ado/guide/data/ado-event-instantiation-by-language.md) parámetros de eventos de [eventos de ADO](../../../ado/reference/ado-api/ado-events.md) de lenguaje cómo [los](../../../ado/guide/data/event-parameters.md) [controladores de eventos trabajan juntos](../../../ado/guide/data/how-event-handlers-work-together.md) [tipos de eventos](../../../ado/guide/data/types-of-events.md)
