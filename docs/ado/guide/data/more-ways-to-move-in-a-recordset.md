---
title: Otras formas de mover en un conjunto de registros | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- Recordset object [ADO], moving
- MovePrevious method [ADO]
ms.assetid: 9f8cf1b2-3def-453f-a0ff-4646c5f15262
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 894ab6b4daba13d6d57dda178f45bf07fc8a8f8d
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272134"
---
# <a name="more-ways-to-move-in-a-recordset"></a>Otras formas de mover en un conjunto de registros
Los cuatro métodos siguientes sirven para moverse o desplazarse, en la **Recordset**: [MoveFirst, MoveLast, MoveNext y MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md). (Algunos de estos métodos no están disponibles en los cursores de solo avance).  
  
 **MoveFirst** cambia la posición del registro actual al primer registro en el **conjunto de registros**. **MoveLast** cambia el registro actual a la última posición el registro de la **conjunto de registros**. Usar **MoveFirst** o **MoveLast**, **Recordset** objeto debe admitir marcadores o movimiento de cursor hacia atrás; en caso contrario, la llamada al método generará un error.  
  
 **MoveNext** mueve el registro actual colocar una posición hacia delante. Si se encuentra en el último registro cuando se llama a **MoveNext**, **EOF** se establecerá en **True**. **MovePrevious** mueve el registro actual colocar un solo lugar con versiones anteriores. Si se encuentra en el primer registro cuando se llama a **MovePrevious**, **BOF** se establecerá en **True**. Es recomendable comprobar la **EOF** y **BOF** propiedades al usar estos métodos y devolver el cursor a una posición válida de registro activo si se sale de cualquier extremo de la **Recordset**, tal y como se muestra aquí:  
  
```  
. . .  
oRs.MoveNext  
If oRs.EOF Then oRs.MoveLast  
. . .   
```  
  
 O bien, en el caso de los **MovePrevious** método:  
  
```  
. . .   
oRs.MovePrevious  
If oRs.BOF Then oRs.MoveFirst  
. . .  
```  
  
 En casos donde la **Recordset** ha sido filtrar u ordenar y se cambian los datos del registro actual, también puede cambiar la posición. En estos casos el **MoveNext** método funciona con normalidad, pero tenga en cuenta que la posición es avanzará un registro con respecto a la nueva posición, no respecto a la antigua. Por ejemplo, cambiar los datos en el registro actual, por ejemplo, que el registro se desplaza hasta el final de ordenada en la **Recordset**, significaría que la llamada a **MoveNext** provocará que ADO establezca el registro actual en el posición después del último registro en el **Recordset** (**EOF** = **True**).  
  
 El comportamiento de los diversos métodos Move de la **Recordset** depende del objeto, hasta cierto punto, los datos dentro de la **conjunto de registros**. Los nuevos registros agregados a la **Recordset** se agregan inicialmente en un orden determinado, que se define por el origen de datos y puede ser dependientes de forma implícita o explícitamente en los datos en el nuevo registro. Por ejemplo, si un criterio de ordenación o una combinación se realiza dentro de la consulta que rellena la **Recordset**, el nuevo registro se insertará en el lugar adecuado dentro de la **conjunto de registros**. Si la ordenación no se especifica explícitamente al crear el **Recordset**, cambios en la implementación del origen de datos podrían provocar la ordenación de las filas devueltas al cambiar accidentalmente. En suma, la ordenación, filtrado y edición de las funciones de la **Recordset** puede afectar al orden y posiblemente qué filas del conjunto de registros serán visibles.  
  
 Por lo tanto, **MoveNext**, **MovePrevious**, **MoveFirst**, **MoveLast**, y **mover** son todos sensible a otras operaciones realizadas en el mismo **conjunto de registros**. ADO siempre intenta mantener la posición actual hasta que se mueve explícitamente, pero a veces, los cambios hacen que sea difícil comprender los efectos de un movimiento posterior. Por ejemplo, si se llama a **MoveFirst** a la posición en la primera fila de una ordenada **Recordset** y cambiar el criterio de ordenación de ascendente a descendente, todavía está en la misma fila, pero ahora es la última fila en el **conjunto de registros**. **MoveFirst** le llevará a una fila diferente (la nueva primera fila).  
  
 Otro ejemplo, si se colocan en una fila determinada en el medio de un **Recordset** y se llama a **eliminar** y, a continuación, llame a **MoveNext**, se encuentra ahora en el registro inmediatamente después del registro eliminado. Pero la llamada a **MovePrevious** hace que el registro anterior al eliminar el registro actual, dado que el registro eliminado ya no se enumeran en la pertenencia de active el **conjunto de registros**.  
  
 Es especialmente difícil definir la semántica de movimiento coherente entre todos los proveedores para los métodos que se mueven en relación con el registro actual: **MovePrevious**, **MoveNext**, y **mover** : frente a cambiar datos en el registro actual. Por ejemplo, si está trabajando con un ordenado, filtrar **Recordset**y cambiar los datos en el registro actual para que preceda a todos los demás registros, pero también, los datos modificados ya no coincide con el filtro, no está claro dónde una **MoveNext** operación debería tardar. La conclusión más segura es ese movimiento relativo dentro de un **Recordset** es más arriesgado que el movimiento absoluto (como el uso de **MoveFirst** o **MoveLast**) cuando los datos son cambiar mientras se editan registros, agrega o elimina. Para ordenar y filtrar deben basarse en una clave principal o un identificador, porque este tipo de valor no debería cambiar.
