---
title: Métodos MoveFirst, MoveLast, MoveNext y MovePrevious (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4acdf777429e879ed22b99ea5a0f07775bc3798c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764506"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>Métodos MoveFirst, MoveLast, MoveNext y MovePrevious (ADO)
Se desplaza al registro primero, último, siguiente o anterior de un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) especificado y hace que registre el registro actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>Comentarios  
 Use el método **MoveFirst** para mover la posición del registro actual al primer registro del **conjunto de registros**.  
  
 Utilice el método **MoveLast** para mover la posición del registro actual al último registro del **conjunto de registros**. El objeto de **conjunto de registros** debe admitir marcadores o movimiento de cursor hacia atrás; de lo contrario, la llamada al método generará un error.  
  
 Una llamada a **MoveFirst** o **MoveLast** cuando **el conjunto de registros** está vacío (los valores **BOF** y **EOF** son true) genera un error.  
  
 Use el método **MoveNext** para mover la posición del registro actual un registro hacia delante (hacia la parte inferior del **conjunto de registros**). Si el último registro es el registro actual y se llama al método **MoveNext** , ADO establece el registro actual en la posición posterior al último registro del **conjunto de registros** ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) es **true**). Un intento de avanzar cuando la propiedad **EOF** ya es **true** genera un error.  
  
 En ADO 2,5 y versiones posteriores, cuando se filtra o se ordena el **conjunto de registros** y se modifican los datos del registro actual, al llamar al método **MoveNext** , se mueve el cursor dos registros hacia delante desde el registro actual. Esto se debe a que, cuando se cambia el registro actual, el Registro siguiente se convierte en el nuevo registro actual. Llamar a **MoveNext** después del cambio mueve el cursor un registro hacia delante desde el nuevo registro actual. Esto es diferente del comportamiento de ADO 2,1 y versiones anteriores. En estas versiones anteriores, el cambio de los datos de un registro actual del **conjunto de registros** ordenado o filtrado no cambia la posición del registro actual, y **MoveNext** mueve el cursor al siguiente registro inmediatamente después del registro actual.  
  
 Use el método **MovePrevious** para mover hacia atrás la posición del registro actual un registro (hacia la parte superior del **conjunto de registros**). El objeto de **conjunto de registros** debe admitir marcadores o movimiento de cursor hacia atrás; de lo contrario, la llamada al método generará un error. Si el primer registro es el registro actual y se llama al método **MovePrevious** , ADO establece el registro actual en la posición anterior al primer registro del **conjunto de registros** ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) es **true**). Si se intenta retroceder cuando la propiedad **BOF** ya es **true** , se genera un error. Si el objeto de **conjunto de registros** no admite marcadores o movimiento de cursor hacia atrás, el método **MovePrevious** generará un error.  
  
 Si el **conjunto de registros** es solo hacia delante y desea admitir el desplazamiento hacia delante y hacia atrás, puede usar la propiedad [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) para crear una caché de registros que admita el movimiento del cursor hacia atrás a través del método [Move](../../../ado/reference/ado-api/move-method-ado.md) . Dado que los registros almacenados en caché se cargan en la memoria, debe evitar almacenar en caché más registros de los necesarios. Puede llamar al método **MoveFirst** en un objeto de conjunto de **registros** de solo avance; Esto puede hacer que el proveedor vuelva a ejecutar el comando que generó el objeto de **conjunto de registros** .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de los métodos MoveFirst, MoveLast, MoveNext y MovePrevious (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [Ejemplo de los métodos MoveFirst, MoveLast, MoveNext y MovePrevious (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [Ejemplo de los métodos MoveFirst, MoveLast, MoveNext y MovePrevious (VC + +)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Move (método) (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [Métodos MoveFirst, MoveLast, MoveNext y MovePrevious (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
