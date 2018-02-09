---
title: Modo de lote | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 048fbd6f43bd78612c810049a07788e659a4139d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
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
