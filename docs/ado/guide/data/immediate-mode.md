---
title: Modo inmediato | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6acd34e06c4660cff3e90c8ef2dd760996d77259
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="immediate-mode"></a>Modo inmediato
Modo inmediato está en vigor cuando el **LockType** propiedad está establecida en **adLockOptimistic** o **adLockPessimistic**. En el modo inmediato, los cambios en un registro se propagan al origen de datos en cuanto se declara completo el trabajo en una fila mediante una llamada a la **actualización** método.  
  
## <a name="calling-update"></a>Llamar a Update  
 Si se mueve desde el registro que está agregando o editando antes de llamar a la **actualización** método, ADO llamará automáticamente **actualización** para guardar los cambios. Debe llamar a la **CancelUpdate** método antes de desplazarse si desea cancelar los cambios realizados en el registro actual o descartar un registro recién agregado.  
  
 El registro actual se mantiene actual después de llamar a la **actualización** método.  
  
## <a name="cancelupdate"></a>CancelUpdate  
 Use la **CancelUpdate** método para cancelar los cambios realizados en la fila actual o descartar una fila recién agregada. No se puede cancelar los cambios en la fila actual o una fila nueva después de llamar a la **actualización** método, a menos que los cambios son parte de una transacción que puede revertir a la **RollbackTrans** método o parte de una actualización por lotes. En el caso de una actualización por lotes, puede cancelar la **actualizar** con el **CancelUpdate** o **CancelBatch** método.  
  
 Si va a agregar una nueva fila cuando se llama a la **CancelUpdate** método, la fila actual se convierte en la fila que era el actual antes de la **AddNew** llamar.  
  
 Si no ha cambiado la fila actual o agregar una nueva fila, una llamada a la **CancelUpdate** método genera un error.
