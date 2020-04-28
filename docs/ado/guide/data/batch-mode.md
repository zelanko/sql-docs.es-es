---
title: Modo por lotes | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 188a95f985ac1d578bca8c7e10ac4c4054c935c0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925953"
---
# <a name="batch-mode"></a>Modo por lotes
El modo por lotes está en vigor cuando la propiedad **LockType** está establecida en **adLockBatchOptimistic** y el proveedor admite la actualización por lotes. Ciertas opciones de tipo de bloqueo no están disponibles en función de la ubicación del cursor. Por ejemplo, un tipo de bloqueo pesimista no está disponible cuando **CursorLocation** está establecido en **adUseClient**. Por el contrario, un proveedor no admite un bloqueo optimista por lotes cuando la ubicación del cursor está en el servidor. Debe usar la actualización por lotes solo con un cursor Keyset o static.  
  
 El método **UpdateBatch** se utiliza para enviar los cambios del **conjunto de registros** que se mantienen en el búfer de copia al servidor para actualizar el origen de datos. En la sección siguiente, se abrirá un **conjunto de registros** en modo por lotes, se realizarán cambios en el búfer de copia y, luego, se enviarán los cambios al origen de datos mediante una llamada a **UpdateBatch**.  
  
 Esta sección contiene los siguientes temas:  
  
-   [Envío de actualizaciones: Método UpdateBatch](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [Filtrar registros actualizados](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [Tratar actualizaciones con errores](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [Detectar y resolver conflictos](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [Desconectar y volver a conectar el conjunto de registros](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [Actualización de resultados unidos: Tabla única](../../../ado/guide/data/updating-joined-results-unique-table.md)
