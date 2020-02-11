---
title: Especificar el primer y el último desencadenador | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- first triggers [SQL Server]
- last triggers
- DML triggers, first or last triggers
- INSTEAD OF triggers
- AFTER triggers
ms.assetid: 9e6c7684-3dd3-46bb-b7be-523b33fae4d5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a851a19a7f00afd055bb2ee8f00eaf4621a1e98f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62524141"
---
# <a name="specify-first-and-last-triggers"></a>Especificar el primer y el último desencadenador
  Puede especificar que uno de los desencadenadores AFTER asociados a una tabla sea el primero o el último que se ejecute para cada una de las acciones desencadenadoras INSERT, DELETE y UPDATE. Los desencadenadores AFTER que se activan entre el primero y el último se ejecutan en un orden indefinido.  
  
 Para especificar el orden de un desencadenador AFTER, use el procedimiento almacenado **sp_settriggerorder** . **sp_settriggerorder** tiene las opciones siguientes.  
  
|Opción|Descripción|  
|------------|-----------------|  
|**Primero**|Especifica que el desencadenador DML es el primer desencadenador AFTER que se activa para una acción desencadenadora.|  
|**Último**|Especifica que el desencadenador DML es el último desencadenador AFTER que se activa para una acción desencadenadora.|  
|**None**|Especifica que no hay ningún orden determinado para la activación del desencadenador DML. Se utiliza principalmente para restablecer un desencadenador que era el primero o el último.|  
  
 En el siguiente ejemplo se muestra el uso de **sp_settriggerorder**:  
  
```  
sp_settriggerorder @triggername = 'MyTrigger', @order = 'first', @stmttype = 'UPDATE'  
```  
  
> [!IMPORTANT]  
>  Los desencadenadores primero y último deben ser dos desencadenadores DML diferentes.  
  
 Una tabla puede tener los desencadenadores INSERT, UPDATE y DELETE definidos al mismo tiempo. Cada tipo de instrucción puede tener sus propios desencadenadores primero y último, pero no pueden ser los mismos.  
  
 Si el primer o último desencadenador definido para una tabla no cubre una acción desencadenadora, como FOR UPDATE, FOR DELETE o FOR INSERT, no habrá desencadenadores primero ni último para las acciones que falten.  
  
 No se pueden especificar desencadenadores INSTEAD OF como primero ni último desencadenador. Los desencadenadores INSTEAD OF se activan antes de actualizar las tablas subyacentes. Si un desencadenador INSTEAD OF realiza actualizaciones en las tablas subyacentes, éstas se realizarán después de que se activen los desencadenadores AFTER definidos en la tabla. Por ejemplo, si un desencadenador INSTEAD OF INSERT de una vista inserta datos en una tabla base y ésta contiene un desencadenador INSTEAD OF INSERT y tres desencadenadores AFTER INSERT, se activará el desencadenador INSTEAD OF INSERT de la tabla base en lugar de la acción de inserción, y los desencadenadores AFTER de la tabla base se activarán después de cualquier acción de inserción de la tabla base. Para más información, consulte [DML Triggers](dml-triggers.md).  
  
 Si una instrucción ALTER TRIGGER cambia un desencadenador primero o último, se quitará el atributo **First** o **Last** y el valor de orden se establecerá como **None**. Para restablecer el orden, se debe usar **sp_settriggerorder**.  
  
 La función OBJECTPROPERTY informa acerca de si un desencadenador es primero o último mediante las propiedades **ExecIsFirstTrigger** y **ExecIsLastTrigger**.  
  
 La replicación genera automáticamente un primer desencadenador para cualquier tabla incluida en una suscripción de actualización inmediata o en cola. La replicación requiere que su desencadenador sea el primero. Generará un error si se intenta incluir una tabla con un primer desencadenador en una suscripción de actualización inmediata o en cola. Si intenta convertir un desencadenador en el primero después de haber incluido una tabla en una suscripción, **sp_settriggerorder** devolverá un error. Tanto si usa ALTER en el desencadenador de replicación como si usa **sp_settriggerorder** para convertir el desencadenador de replicación en un desencadenador último o sin orden definido, la suscripción no funcionará correctamente.  
  
## <a name="see-also"></a>Consulte también  
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectpropertyex-transact-sql)   
 [sp_settriggerorder &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql)  
  
  
