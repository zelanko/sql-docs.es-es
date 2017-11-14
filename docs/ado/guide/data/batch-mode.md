---
title: Modo de lote | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 92e249a7c2d5b0c01e291f4829d5c4f8c580fb2c
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="batch-mode"></a>Modo por lotes
Modo por lotes está en vigor cuando el **LockType** propiedad está establecida en **adLockBatchOptimistic** y actualización por lotes es compatible con el proveedor. Determinadas opciones de tipo de bloqueo no están disponibles según la ubicación del cursor. Por ejemplo, un tipo de bloqueo pesimista no está disponible cuando la **CursorLocation** está establecido en **adUseClient**. Por el contrario, un proveedor no admite un bloqueo optimista por lotes cuando la ubicación del cursor está en el servidor. Debe usar la actualización por lotes con un conjunto de claves o un cursor estático solo.  
  
 El **UpdateBatch** método se usa para enviar **Recordset** cambios se conservan en el búfer de copia en el servidor para actualizar el origen de datos. En la sección siguiente, se abrirá una **Recordset** en modo por lotes, realizar cambios en el búfer de copia y, a continuación, enviar los cambios al origen de datos mediante una llamada a **UpdateBatch**.  
  
 Esta sección contiene los siguientes temas:  
  
-   [Enviar actualizaciones: método UpdateBatch](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [Filtrar registros actualizados](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [Tratar actualizaciones con errores](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [Detectar y resolver conflictos](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [Desconectar y volver a conectar el conjunto de registros](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [Actualización unido a resultados: Tabla única](../../../ado/guide/data/updating-joined-results-unique-table.md)

