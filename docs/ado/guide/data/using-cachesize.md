---
title: Utilizar CacheSize | Documentos de Microsoft
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
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 74ec85c5907485edc5ad8dbcb6c24826fc21ccf3
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="using-cachesize"></a>Utilizar CacheSize
Use la **CacheSize** propiedad para controlar cuántos registros para recuperar en una vez en la memoria local desde el proveedor. Por ejemplo, si la **CacheSize** es 10, tras abrir primero la **Recordset** de objeto, el proveedor recupera los 10 primeros registros en la memoria local. Conforme se desplaza por la **Recordset** de objeto, el proveedor devuelve los datos desde el búfer de memoria local. En cuanto mueva más allá del último registro en la memoria caché, el proveedor recupera los 10 siguientes registros del origen de datos en la memoria caché.  
  
> [!NOTE]
>  **CacheSize** se basa en el **máximo de filas abiertas** propiedades específicas del proveedor (en el **propiedades** colección de la **Recordset** objeto). No se puede establecer **CacheSize** en un valor mayor que **máximo de filas abiertas.** Para modificar el número de filas que se puede abrir el proveedor, establezca **máximo de filas abiertas**.  
  
 El valor de **CacheSize** se puede ajustar durante la vida de la **Recordset** objeto, pero si se cambia este valor solo afecta al número de registros en la memoria caché después de recuperaciones subsiguientes desde el origen de datos. Cambiar el valor de propiedad por sí sola no cambiará el contenido actual de la memoria caché.  
  
 Si hay muy pocos registros para recuperar que **CacheSize** especifica, el proveedor devuelve los registros restantes y se produce ningún error.  
  
 A **CacheSize** valor de cero no está autorizada y devuelve un error.  
  
 Los registros recuperados de la memoria caché no reflejan los cambios simultáneos realizados por otros usuarios al origen de datos. Para forzar una actualización de todos los datos almacenados en memoria caché, use la [Resync](../../../ado/reference/ado-api/resync-method.md) método.  
  
 Si **CacheSize** se establece en un valor mayor que 1, los métodos de navegación ([mover](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext y MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) puede provocar la navegación a un eliminada registro, si se produce una eliminación después de haber recuperaron los registros. Después de la operación de captura inicial, las eliminaciones posteriores no se reflejarán en la memoria caché de datos hasta que se intente tener acceso a un valor de datos de una fila eliminada. Sin embargo, establecer **CacheSize** en 1, se elimina este problema porque no se pueden recuperar filas eliminadas.

