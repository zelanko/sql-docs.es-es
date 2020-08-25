---
description: Modo por lotes
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 353e5ae0fe15fb21f04f6efcc97195a5e237b58e
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806397"
---
# <a name="batch-mode"></a>Modo por lotes
El modo por lotes está en vigor cuando la propiedad **LockType** está establecida en **adLockBatchOptimistic** y el proveedor admite la actualización por lotes. Ciertas opciones de tipo de bloqueo no están disponibles en función de la ubicación del cursor. Por ejemplo, un tipo de bloqueo pesimista no está disponible cuando **CursorLocation** está establecido en **adUseClient**. Por el contrario, un proveedor no admite un bloqueo optimista por lotes cuando la ubicación del cursor está en el servidor. Debe usar la actualización por lotes solo con un cursor Keyset o static.  
  
 El método **UpdateBatch** se utiliza para enviar los cambios del **conjunto de registros** que se mantienen en el búfer de copia al servidor para actualizar el origen de datos. En la sección siguiente, se abrirá un **conjunto de registros** en modo por lotes, se realizarán cambios en el búfer de copia y, luego, se enviarán los cambios al origen de datos mediante una llamada a **UpdateBatch**.  
  
 Esta sección contiene los siguientes temas:  
  
-   [Envío de actualizaciones: Método UpdateBatch](./sending-the-updates-updatebatch-method.md)  
  
-   [Filtrar registros actualizados](./filtering-for-updated-records.md)  
  
-   [Tratar actualizaciones con errores](./dealing-with-failed-updates.md)  
  
-   [Detectar y resolver conflictos](./detecting-and-resolving-conflicts.md)  
  
-   [Desconectar y volver a conectar el conjunto de registros](./disconnecting-and-reconnecting-the-recordset.md)  
  
-   [Actualización de resultados unidos: Tabla única](./updating-joined-results-unique-table.md)