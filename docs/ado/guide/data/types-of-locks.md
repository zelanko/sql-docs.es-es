---
title: Tipos de bloqueos | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AdLockBatchOptimistic [ADO]
- AdLockReadOnly [ADO]
- AdLockUnspecified [ADO]
- locks [ADO], types
- AdLockOptimistic [ADO]
- AdLockPessimistic [ADO]
ms.assetid: 12a978c0-b8a0-4ef0-87f0-a43c13659272
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5a84610a43966d4861b1227131e0c7aee3b828b3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="types-of-locks"></a>Tipos de bloqueos
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 Indica actualizaciones optimistas por lotes. Se requiere para el modo de actualización por lotes.  
  
 Muchas aplicaciones capturar un número de filas a la vez y, a continuación, que deba realizar actualizaciones coordinadas que incluyen todo el conjunto de filas para insertar, actualizar o eliminar. Con cursores por lotes, sólo uno es necesario redondear ida y vuelta al servidor, mejorando el rendimiento de las actualizaciones y reduce el tráfico de red. Utilizar una biblioteca de cursores de lote, puede crear un cursor estático y, a continuación, desconectarse del origen de datos. En este momento puede realizar cambios en las filas y posteriormente volver a conectarse y enviar los cambios al origen de datos en un lote.  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 Indica que el proveedor utiliza bloqueo optimista: bloquear registros sólo cuando se llama a la **actualización** método. Esto significa que no hay posibilidad de que otro usuario puede cambiar los datos entre el momento en que se modificó el registro y cuando se llama a **actualización**, que genera conflictos. Use este tipo de bloqueo en situaciones donde se están quedando sin las posibilidades de una colisión o donde las colisiones se puedan resolver fácilmente.  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 Indica un bloqueo pesimista, registro por registro. El proveedor no lo que es necesario para garantizar la modificación correcta de los registros, por lo general, los registros de bloqueos en el origen de datos inmediatamente antes de modificarla. Por supuesto, esto significa que los registros están disponibles para otros usuarios una vez que empiece a editar, hasta que se libere el bloqueo mediante una llamada a **Update.** Use este tipo de bloqueo en un sistema que no puede permitirse tener cambios simultáneos a los datos, como en un sistema de reserva.  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 Indica los registros de solo lectura. No se puede modificar los datos. Un bloqueo de solo lectura es el tipo de bloqueo "más rápido" porque no requiere el servidor para mantener un bloqueo en los registros.  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 No especifica un tipo de bloqueo.
