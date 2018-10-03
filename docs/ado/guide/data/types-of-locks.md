---
title: Tipos de bloqueos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AdLockBatchOptimistic [ADO]
- AdLockReadOnly [ADO]
- AdLockUnspecified [ADO]
- locks [ADO], types
- AdLockOptimistic [ADO]
- AdLockPessimistic [ADO]
ms.assetid: 12a978c0-b8a0-4ef0-87f0-a43c13659272
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 039f09a1d3731b316359acd03e72312b4485df89
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47726823"
---
# <a name="types-of-locks"></a>Tipos de bloqueos
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 Indica las actualizaciones por lotes optimista. Se requiere para el modo de actualización por lotes.  
  
 Muchas aplicaciones capturar un número de filas a la vez y, a continuación, se deben realizar actualizaciones coordinadas que incluyen todo el conjunto de filas que se insertan, actualizan o eliminan. Con los cursores de lote, solo uno es necesario redondo y vuelta al servidor, mejorando así el rendimiento de las actualizaciones y reduce el tráfico de red. Usar una biblioteca de cursores por lotes, puede crear un cursor estático y, a continuación, desconectarse del origen de datos. En este momento puede realizar cambios en las filas y posteriormente volver a conectarse y publicar los cambios en el origen de datos en un lote.  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 Indica que el proveedor utiliza el bloqueo optimista: bloquear registros solo cuando se llama a la **actualización** método. Esto significa que es probable que otro usuario puede cambiar los datos entre el momento en modificó el registro y al llamar a **actualización**, que genera conflictos. Utilice este tipo de bloqueo en situaciones en que las posibilidades de una colisión de baja o donde se puedan resolver fácilmente las colisiones.  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 Indica un bloqueo pesimista, registro por registro. El proveedor no lo que es necesario para garantizar la edición correcta de los registros, por lo general, bloqueando los registros en el origen de datos inmediatamente antes de editarlo. Por supuesto, esto significa que los registros están disponibles para otros usuarios una vez que empiece a editar, hasta que se libere el bloqueo mediante una llamada a **Update.** Use este tipo de bloqueo en un sistema donde no puede permitirse tener los cambios simultáneos a los datos, como en un sistema de reserva.  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 Indica los registros de solo lectura. No se puede modificar los datos. Un bloqueo de solo lectura es el tipo de bloqueo "más rápido" porque no requiere el servidor para mantener un bloqueo en los registros.  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 No especifica un tipo de bloqueo.
