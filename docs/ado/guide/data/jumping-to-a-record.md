---
title: Saltar a un registro | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19a4275d339132db8efd4b09a313b482fc8cb666
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="jumping-to-a-record"></a>Saltar a un registro
El [mover](../../../ado/reference/ado-api/move-method-ado.md) método le permite mover hacia delante o hacia atrás en el **Recordset** un número especificado de registros utilizando la sintaxis siguiente:  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>Comentarios  
 El **mover** método se admite en todos los **Recordset** objetos.  
  
 Si el *NumRecords* argumento es mayor que cero, la posición actual del registro se mueve hacia delante (hacia el final de la **Recordset**). Si *NumRecords* es menor que cero, la posición actual del registro se mueve hacia atrás (hacia el principio de la **Recordset**).  
  
 Si el **mover** llamada haría al mover la posición del registro actual a un punto antes del primer registro, ADO establece el registro actual en la posición situada delante del primer registro de la **Recordset** (**BOF** es **True**). Un intento de mover hacia atrás cuando el **BOF** propiedad ya está **True** genera un error.  
  
 Si el **mover** llamada haría al mover la posición del registro actual a un punto posterior al último registro, ADO establece el registro actual en la posición después del último registro en el **Recordset** (**EOF** es **True**). Un intento de mover hacia delante cuando los **EOF** propiedad ya está **True** genera un error.  
  
 Llamar a la **mover** método desde una **Recordset** objeto genera un error.  
  
 Si se pasa un marcador en el *iniciar* argumento, que es el movimiento en relación con el registro con este marcador, suponiendo que el **Recordset** objeto admite marcadores. Un marcador se obtiene mediante la [marcador](../../../ado/reference/ado-api/bookmark-property-ado.md) propiedad. Si no se especifica, el movimiento es en relación con el registro actual.  
  
 Si usas el **CacheSize** propiedad localmente en caché los registros del proveedor, pasar un *NumRecords* argumento que se mueve la posición del registro actual fuera del grupo actual de registros almacenados en caché obliga a ADO para recuperar un nuevo grupo de registros, empezando por el registro de destino. El **CacheSize** propiedad determina el tamaño del grupo recién recuperado y el registro de destino es el primer registro recuperado.
