---
title: Más formas de mover en un conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- Recordset object [ADO], moving
- MovePrevious method [ADO]
ms.assetid: 9f8cf1b2-3def-453f-a0ff-4646c5f15262
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e648bd9dcb3c6a073419cde42587f1be706fff4d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52513902"
---
# <a name="more-ways-to-move-in-a-recordset"></a>Otras formas de mover en un conjunto de registros
Los cuatro métodos siguientes sirven para moverse o desplazar, en el **Recordset**: [MoveFirst, MoveLast, MoveNext y MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md). (Algunos de estos métodos no están disponibles en los cursores de solo avance).  
  
 **MoveFirst** cambia la posición actual del registro en el primer registro de la **Recordset**. **MoveLast** cambia el registro actual a la última posición el registro de la **Recordset**. Para usar **MoveFirst** o **MoveLast**, **Recordset** objeto debe admitir marcadores o movimiento de cursor hacia atrás; en caso contrario, la llamada al método generará un error.  
  
 **MoveNext** mueve el registro actual colocar un lugar hacia delante. Si se encuentra en el último registro cuando se llama a **MoveNext**, **EOF** se establecerá en **True**. **MovePrevious** mueve el registro actual posición de un solo lugar con versiones anteriores. Si se encuentra en el primer registro cuando se llama a **MovePrevious**, **BOF** se establecerá en **True**. Es conveniente comprobar el **EOF** y **BOF** propiedades al usar estos métodos y para mover el cursor de vuelta a una posición válida del registro actual si se sale de cualquier extremo de la **Recordset**, tal y como se muestra aquí:  
  
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
  
 En casos donde el **Recordset** ha sido filtrar u ordenar y se cambian los datos del registro actual, también puede cambiar la posición. En estos casos el **MoveNext** método funciona con normalidad, pero tenga en cuenta que la posición avanzará un registro con respecto a la nueva posición, no en la posición anterior. Por ejemplo, cambiando los datos en el registro actual, de modo que el registro se mueve al final de la ordenada **Recordset**, significaría que la llamada a **MoveNext** da como resultado en ADO, establezca el registro actual en el posición después del último registro en el **Recordset** (**EOF** = **True**).  
  
 El comportamiento de los distintos métodos de movimiento de la **Recordset** depende del objeto, en cierta medida, en los datos dentro de la **Recordset**. Los nuevos registros agregados a la **Recordset** se agregan inicialmente en un orden determinado, que se define mediante el origen de datos y puede ser dependientes de forma implícita o explícitamente los datos en el nuevo registro. Por ejemplo, si un criterio de ordenación o una combinación se realiza dentro de la consulta que rellena la **Recordset**, se insertará el nuevo registro en el lugar adecuado dentro de la **Recordset**. Si la ordenación no se especifica explícitamente al crear el **Recordset**, cambios en la implementación de origen de datos pueden provocar que el orden de las filas devueltas cambiar accidentalmente. En suma, la ordenación, filtrado y edición de las funciones de la **Recordset** puede afectar al orden y, posiblemente, las filas del conjunto de registros que estarán visibles.  
  
 Por lo tanto, **MoveNext**, **MovePrevious**, **MoveFirst**, **MoveLast**, y **mover** todos minúsculas a otras operaciones realizan en el mismo **Recordset**. ADO siempre intenta mantener la posición actual hasta que se mueve explícitamente, pero a veces, los cambios intermedios hacen que sea difícil comprender los efectos de un movimiento subsiguiente. Por ejemplo, si se llama a **MoveFirst** a la posición en la primera fila de un ordenado **Recordset** y cambiar el criterio de ordenación de ascendente a descendente, todavía está en la misma fila - pero ahora es la última fila en el **Recordset**. **MoveFirst** le llevará a una fila diferente (la nueva primera fila).  
  
 Como otro ejemplo, si se coloca en una fila determinada en el medio de un **Recordset** y se llama a **eliminar** y, a continuación, llame a **MoveNext**, está ahora en el registro inmediatamente después del registro eliminado. Pero la llamada a **MovePrevious** hace que el registro anterior al eliminar el registro actual, dado que el registro eliminado ya no se cuenta en la pertenencia de active el **Recordset**.  
  
 Es especialmente difícil de definir la semántica de movimiento coherente en todos los proveedores para los métodos que se mueven en relación con el registro actual - **MovePrevious**, **MoveNext**, y **mover** : frente a cambiar datos en el registro actual. Por ejemplo, si está trabajando con un ordenado, filtrado **Recordset**y cambiar los datos en el registro actual para que preceda a todos los demás registros, pero también, los datos modificados ya no coincide con el filtro, no está claro dónde un **MoveNext** operación tardará. La conclusión más segura es ese movimiento relativo dentro de un **Recordset** es más arriesgado que el movimiento absoluto (como el uso de **MoveFirst** o **MoveLast**) cuando los datos son cambiar mientras se editan los registros, agrega o elimina. Filtrado y ordenación deben basarse en una clave principal o un identificador, porque este tipo de valor no debe cambiar.
