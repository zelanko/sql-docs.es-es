---
title: Move (método) (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords:
- Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a64cfae0055f3052a75886556b7493fb096105a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="move-method-ado"></a>Move (método) (ADO)
Mueve la posición del registro actual en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>Parámetros  
 *NumRecords*  
 Iniciado **largo** expresión que especifica el número de registros que se mueve la posición del registro actual.  
  
 *Iniciar*  
 Opcional. A **cadena** valor o **Variant** que se evalúa como un marcador. También puede usar un [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) valor.  
  
## <a name="remarks"></a>Comentarios  
 El **mover** método se admite en todos los **Recordset** objetos.  
  
 Si el *NumRecords* argumento es mayor que cero, la posición actual del registro se mueve hacia delante (hacia el final de la **Recordset**). Si *NumRecords* es menor que cero, la posición actual del registro se mueve hacia atrás (hacia el principio de la **Recordset**).  
  
 Si el **mover** llamada haría al mover la posición del registro actual a un punto antes del primer registro, ADO establece el registro actual en la posición situada delante del primer registro en el conjunto de registros ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) es **True** ). Un intento de mover hacia atrás cuando el **BOF** propiedad ya está **True** genera un error.  
  
 Si el **mover** llamada haría al mover la posición del registro actual a un punto posterior al último registro, ADO establece el registro actual en la posición después del último registro en el conjunto de registros ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) es **True** ). Un intento de mover hacia delante cuando los **EOF** propiedad ya está **True** genera un error.  
  
 Llamar a la **mover** método desde una **Recordset** objeto genera un error.  
  
 Si se pasa el *iniciar* argumento, que es el movimiento en relación con el registro con este marcador, suponiendo que el **Recordset** objeto admite marcadores. Si no se especifica, el movimiento es en relación con el registro actual.  
  
 Si usas el [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propiedad localmente en caché los registros del proveedor, pasar un *NumRecords* argumento que se mueve la posición del registro actual fuera del grupo actual de registros almacenados en caché obliga a ADO para recuperar un nuevo grupo de registros, empezando por el registro de destino. El **CacheSize** propiedad determina el tamaño del grupo recién recuperado y el registro de destino es el primer registro recuperado.  
  
 Si el **Recordset** objeto es de solo avance, un usuario puede seguir pasando un *NumRecords* argumento menor que cero, siempre que el destino sea dentro del conjunto actual de registros almacenados en caché. Si el **mover** llamada haría al mover la posición actual del registro a un registro antes del primer registro almacenado en caché, se producirá un error. Por lo tanto, puede usar una caché de registro que admite el desplazamiento completa a través de un proveedor que permite el desplazamiento solo hacia delante. Dado que se cargan los registros almacenados en caché en memoria, no debe almacenar en caché más registros que son necesarios. Incluso si solo avance **Recordset** mueve el objeto es compatible con versiones anteriores de esta manera, una llamada a la [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) método en cualquier solo avance **conjunto de registros** sigue objeto generar un error.  
  
> [!NOTE]
>  Compatibilidad con los desplazamientos hacia atrás en un solo avance **Recordset** no es previsible, dependiendo del proveedor. Si el registro actual se ha colocado después del último registro en el **Recordset**, **mover** con las versiones anteriores no está penada por la posición actual correcta.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método Move (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Ejemplo del método Move (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Ejemplo del método Move (VC ++)](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
