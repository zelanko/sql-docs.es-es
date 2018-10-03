---
title: Modo inmediato | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ff8782287f5a6cbeb3f22ca58eaa3bd061c6c89
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47657673"
---
# <a name="immediate-mode"></a>Modo inmediato
Modo inmediato está en vigor cuando el **LockType** propiedad está establecida en **adLockOptimistic** o **adLockPessimistic**. En el modo inmediato, los cambios realizados en un registro se propagan al origen de datos tan pronto como se declara completo el trabajo en una fila mediante una llamada a la **actualización** método.  
  
## <a name="calling-update"></a>Llamar a Update  
 Si mueve del registro va a agregar o editar antes de llamar a la **actualización** método, ADO llamará automáticamente **actualización** para guardar los cambios. Debe llamar a la **CancelUpdate** método antes de la navegación si desea cancelar los cambios realizados en el registro actual o descartar un registro recién agregado.  
  
 El registro actual permanece actual después de llamar a la **actualización** método.  
  
## <a name="cancelupdate"></a>CancelUpdate  
 Use la **CancelUpdate** método para cancelar los cambios realizados en la fila actual o descartar una fila recién agregada. No se puede cancelar los cambios realizados en la fila actual o una nueva fila después de llamar a la **actualización** método, a menos que los cambios son parte de una transacción que se puede revertir con el **RollbackTrans** método o parte de una actualización por lotes. En el caso de una actualización por lotes, puede cancelar el **actualizar** con el **CancelUpdate** o **CancelBatch** método.  
  
 Si va a agregar una nueva fila cuando se llama a la **CancelUpdate** método, la fila actual se convierte en la fila que era actual antes de la **AddNew** llamar.  
  
 Si no ha cambiado la fila actual o agrega una nueva fila, una llamada a la **CancelUpdate** método genera un error.
