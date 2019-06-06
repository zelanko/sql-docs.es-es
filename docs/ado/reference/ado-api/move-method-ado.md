---
title: Mover (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords:
- Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c7b99a0848101ca0fad4844c51e44f1ccc628cd6
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707603"
---
# <a name="move-method-ado"></a>Move (método) (ADO)
Mueve la posición del registro actual en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>Parámetros  
 *NumRecords*  
 Con signo **largo** expresión que especifica el número de registros que se mueve la posición actual del registro.  
  
 *Iniciar*  
 Opcional. Un **cadena** valor o **Variant** que se evalúa como un marcador. También puede usar un [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) valor.  
  
## <a name="remarks"></a>Comentarios  
 El **mover** método es compatible con todas **Recordset** objetos.  
  
 Si el *NumRecords* argumento es mayor que cero, la posición actual del registro se mueve hacia delante (hacia el final de la **Recordset**). Si *NumRecords* es menor que cero, la posición actual del registro se mueve hacia atrás (hacia el principio de la **Recordset**).  
  
 Si el **mover** llamada haría al mover la posición actual del registro a un punto antes del primer registro, ADO establece el registro actual en la posición delante del primer registro en el conjunto de registros ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) es **True** ). Un intento de mover hacia atrás cuando el **BOF** propiedad ya está **True** genera un error.  
  
 Si el **mover** llamada a mueve la posición actual del registro a un punto después del último registro, ADO establece el registro actual en la posición después del último registro del conjunto de registros ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) es **True** ). Un intento de mover hacia delante cuando la **EOF** propiedad ya está **True** genera un error.  
  
 Una llamada a la **mover** método desde un valor vacío **Recordset** objeto genera un error.  
  
 Si se pasa el *iniciar* argumento, que es el movimiento en relación con el registro con este marcador, suponiendo que el **Recordset** objeto admite marcadores. Si no se especifica, el movimiento es en relación con el registro actual.  
  
 Si usas el [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propiedad localmente en caché los registros del proveedor, pasando un *NumRecords* argumento que se mueve la posición actual del registro fuera del grupo actual de registros almacenados en caché obliga a ADO para recuperar un nuevo grupo de registros, empezando por el registro de destino. El **CacheSize** propiedad determina el tamaño del grupo recién recuperado y el registro de destino es el primer registro recuperado.  
  
 Si el **Recordset** objeto es de solo avance, un usuario todavía puede pasar un *NumRecords* argumento menor que cero, proporciona el destino está dentro del actual conjunto de registros almacenados en caché. Si el **mover** llamada haría al mover la posición actual del registro a un registro antes del primer registro almacenado en caché, se producirá un error. Por lo tanto, puede usar una caché de registro que admite el desplazamiento completa a través de un proveedor que admite el desplazamiento sólo hacia delante. Dado que se cargan registros almacenados en caché en memoria, debe evitar almacenar en caché más registros que son necesarios. Incluso si sólo avance **Recordset** mueve el objeto es compatible con versiones anteriores de esta manera, una llamada a la [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) método en cualquier solo avance **Recordset** igualmente objeto generar un error.  
  
> [!NOTE]
>  Compatibilidad para mover hacia atrás en un solo avance **Recordset** no es predecible, dependiendo del proveedor. Si el registro actual se ha colocado después del último registro en el **Recordset**, **mover** con versiones anteriores no es posible que en la posición actual correcta.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método Move (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Ejemplo del método Move (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Ejemplo del método Move (VC ++)](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
