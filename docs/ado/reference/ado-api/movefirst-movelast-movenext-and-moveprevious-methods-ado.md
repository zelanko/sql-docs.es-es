---
title: MoveFirst, MoveLast, MoveNext y MovePrevious métodos (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 905fc532057a827f30735efe067464f488f51dc0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242912"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst, MoveLast, MoveNext y MovePrevious métodos (ADO)
Se mueve a la primera, última, siguiente o anterior de registro en un determinado [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto y hace que el registro en el registro actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>Comentarios  
 Use la **MoveFirst** método para mover la posición actual del registro en el primer registro de la **Recordset**.  
  
 Use la **MoveLast** método para mover la posición actual del registro al último registro en el **Recordset**. El **Recordset** objeto debe admitir marcadores o movimiento de cursor hacia atrás; en caso contrario, la llamada al método generará un error.  
  
 Una llamada a **MoveFirst** o **MoveLast** cuando el **Recordset** está vacío (ambos **BOF** y **EOF** es True) genera un error.  
  
 Use la **MoveNext** método para mover el registro actual colocar un único registro hacia delante (hacia la parte inferior de la **Recordset**). Si el último registro es el registro actual y se llama el **MoveNext** método, ADO establece el registro actual a la posición después del último registro en el **Recordset** ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) es **True**). Un intento de mover hacia delante cuando la **EOF** propiedad ya está **True** genera un error.  
  
 En ADO 2.5 y versiones posterior, cuando el **Recordset** se ha filtrado u ordenados y se cambian los datos del registro actual, una llamada a la **MoveNext** método mueve el cursor dos delante desde el registro actual . Esto es porque cuando se cambia el registro actual, el registro siguiente, se convierte en el nuevo registro actual. Una llamada a **MoveNext** después de que el cambio mueve el cursor un registro hacia delante desde el nuevo registro actual. Esto es diferente del comportamiento en ADO 2.1 y versiones anteriores. En estas versiones anteriores, cambiando los datos de registro actual en ordenados o filtrados **Recordset** no cambia la posición del registro actual, y **MoveNext** mueve el cursor al siguiente registro inmediatamente después del registro actual.  
  
 Use la **MovePrevious** con versiones anteriores de un registro de posición de método para mover el registro actual (hacia la parte superior de la **Recordset**). El **Recordset** objeto debe admitir marcadores o movimiento de cursor hacia atrás; en caso contrario, la llamada al método generará un error. Si el primer registro es el registro actual y se llama el **MovePrevious** método, ADO establece el registro actual en la posición delante del primer registro en el **Recordset** ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)es **True**). Un intento de mover hacia atrás cuando el **BOF** propiedad ya está **True** genera un error. Si el **Recordset** objeto no admite marcadores o movimiento de cursor hacia atrás, la **MovePrevious** método generará un error.  
  
 Si el **Recordset** es de solo avance y desea admitir el desplazamiento hacia delante y hacia atrás, puede usar el [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propiedad para crear una caché de registro que admitirá el movimiento de cursor hacia atrás a través de la [mover](../../../ado/reference/ado-api/move-method-ado.md) método. Dado que se cargan registros almacenados en caché en memoria, debe evitar almacenar en caché más registros que es necesario. Puede llamar a la **MoveFirst** método de solo avance **Recordset** objeto; si lo hace, se puede volver a ejecutar el comando que genera el proveedor de la **Recordset** objeto .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos ejemplo (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos ejemplo (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos ejemplo (VC ++)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Método Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
