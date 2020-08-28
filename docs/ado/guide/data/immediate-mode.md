---
title: Modo inmediato | Microsoft Docs
description: Describe el modo inmediato, que está en vigor cuando la propiedad LockType está establecida en adLockOptimistic o adLockPessimistic.
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
author: rothja
ms.author: jroth
ms.openlocfilehash: e57d39fedb6509663ec21f28341d6bbca57dbd5c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980506"
---
# <a name="immediate-mode"></a>Modo inmediato
El modo inmediato está en vigor cuando la propiedad **LockType** está establecida en **adLockOptimistic** o **adLockPessimistic**. En el modo inmediato, los cambios en un registro se propagan al origen de datos en cuanto se declara el trabajo en una fila completa llamando al método **Update** .  
  
## <a name="calling-update"></a>Llamando a Update  
 Si se mueve del registro que está agregando o editando antes de llamar al método **Update** , ADO llamará automáticamente a **Update** para guardar los cambios. Debe llamar al método **CancelUpdate** antes de la navegación si desea cancelar los cambios realizados en el registro actual o descartar un registro recién agregado.  
  
 El registro actual sigue siendo actual después de llamar al método **Update** .  
  
## <a name="cancelupdate"></a>CancelUpdate  
 Utilice el método **CancelUpdate** para cancelar los cambios realizados en la fila actual o para descartar una fila recién agregada. No se pueden cancelar los cambios realizados en la fila actual o en una nueva una vez que se llama al método **Update** , a menos que los cambios formen parte de una transacción que se pueda revertir con el método **RollbackTrans** o parte de una actualización por lotes. En el caso de una actualización por lotes, puede cancelar la **actualización** con el método **CancelUpdate** o **CancelBatch** .  
  
 Si va a agregar una nueva fila al llamar al método **CancelUpdate** , la fila actual se convierte en la fila que era la actual antes de la llamada a **AddNew** .  
  
 Si no ha cambiado la fila actual ni ha agregado una nueva fila, al llamar al método **CancelUpdate** se genera un error.
