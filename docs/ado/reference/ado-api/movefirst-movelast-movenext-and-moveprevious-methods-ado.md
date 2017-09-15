---
title: "MoveFirst, MoveLast, MoveNext y MovePrevious métodos (ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::MoveLast
- Recordset15::MoveNext
- Recordset15::raw_MoveNext
- Recordset15::raw_MovePrevious
- Recordset15::MoveFirst
- Recordset15::raw_MoveLast
- Recordset15::MovePrevious
- Recordset15::raw_MoveFirst
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- MovePrevious method [ADO]
ms.assetid: a61a01a7-5b33-4150-9126-21dfa63654cb
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cda6c82147648f35adb80012d0810d514d08de86
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst, MoveLast, MoveNext y MovePrevious métodos (ADO)
Se mueve a la primera, última, siguiente o anterior registro en un determinado [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto y hace que el registro en el registro actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>Comentarios  
 Use la **MoveFirst** método para mover la posición del registro actual al primer registro en el **conjunto de registros**.  
  
 Use la **MoveLast** método para mover la posición del registro actual hasta el último registro en el **conjunto de registros**. El **Recordset** objeto debe admitir marcadores o movimiento de cursor hacia atrás; en caso contrario, la llamada al método generará un error.  
  
 Una llamada a **MoveFirst** o **MoveLast** cuando el **Recordset** está vacío (ambos **BOF** y **EOF** es True) genera un error.  
  
 Use la **MoveNext** método para mover el registro actual colocar un registro hacia delante (hacia el final de la **Recordset**). Si el último registro es el registro actual y se llama el **MoveNext** método, ADO establece el registro actual a la posición después del último registro en el **Recordset** ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) es **True**). Un intento de mover hacia delante cuando los **EOF** propiedad ya está **True** genera un error.  
  
 En ADO 2.5 y versiones posterior, cuando la **Recordset** se ha filtrado u ordena y se modifican los datos del registro actual, al llamar a la **MoveNext** método mueve los registros de cursor dos reenvían desde el registro actual . Esto es porque cuando se modifica el registro actual, el siguiente registro se convierte en el nuevo registro actual. Al llamar a **MoveNext** después de que el cambio mueve el cursor un registro hacia delante desde el nuevo registro actual. Esto es diferente del comportamiento en ADO 2.1 y versiones anteriores. En estas versiones anteriores, al cambiar los datos de un registro actual en ordenados o filtrados **Recordset** no cambia la posición del registro actual, y **MoveNext** mueve el cursor hasta el siguiente registro inmediatamente después del registro actual.  
  
 Use la **MovePrevious** método para mover el registro actual colocar un único registro con versiones anteriores (hacia el principio de la **Recordset**). El **Recordset** objeto debe admitir marcadores o movimiento de cursor hacia atrás; en caso contrario, la llamada al método generará un error. Si el primer registro es el registro actual y se llama el **MovePrevious** método, ADO establece el registro actual en la posición situada delante del primer registro de la **Recordset** ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)es **True**). Un intento de mover hacia atrás cuando el **BOF** propiedad ya está **True** genera un error. Si el **Recordset** objeto no admite marcadores o movimiento de cursor hacia atrás, la **MovePrevious** método generará un error.  
  
 Si el **Recordset** es solo hacia adelante y desea que admiten el desplazamiento hacia delante y hacia atrás, puede usar el [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propiedad para crear una memoria caché de registros que admita movimientos de cursor hacia atrás a través de la [mover](../../../ado/reference/ado-api/move-method-ado.md) método. Como registros almacenados en caché se cargan en memoria, no debe almacenar en caché más registros que sean necesarios. Puede llamar a la **MoveFirst** método de solo avance **Recordset** objeto; si se hace, puede impedir que el proveedor volver a ejecutar el comando que genera el **Recordset** objeto .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos ejemplo (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos ejemplo (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos ejemplo (VC ++)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Move (método) (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)

