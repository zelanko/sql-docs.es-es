---
title: Move (método) (ADO) | Microsoft Docs
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
ms.openlocfilehash: 4d76f239094185af7a3e940201b3f99132c0194a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918194"
---
# <a name="move-method-ado"></a>Move (método) (ADO)
Mueve la posición del registro actual en un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>Parámetros  
 *NumRecords*  
 Expresión de **tipo Long** con signo que especifica el número de registros que se mueve la posición del registro actual.  
  
 *Iniciar*  
 Opcional. Un valor de **cadena** o una **variante** que se evalúa como un marcador. También puede usar un valor de [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) .  
  
## <a name="remarks"></a>Observaciones  
 El método **Move** es compatible con todos los objetos de **conjunto de registros** .  
  
 Si el argumento *NumRecords* es mayor que cero, la posición del registro actual se desplaza hacia delante (hacia el final del **conjunto de registros**). Si *NumRecords* es menor que cero, la posición del registro actual se desplaza hacia atrás (hacia el principio del **conjunto de registros**).  
  
 Si la llamada a **Move** movera la posición del registro actual a un punto anterior al primer registro, ADO establece el registro actual en la posición anterior al primer registro del conjunto de registros ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) es **true**). Si se intenta retroceder cuando la propiedad **BOF** ya es **true** , se genera un error.  
  
 Si la llamada a **Move** movera la posición del registro actual a un punto después del último registro, ADO establece el registro actual en la posición posterior al último registro del conjunto de registros ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) es **true**). Un intento de avanzar cuando la propiedad **EOF** ya es **true** genera un error.  
  
 Al llamar al método **Move** desde un objeto **Recordset** vacío, se genera un error.  
  
 Si pasa el argumento de *Inicio* , el movimiento es relativo al registro con este marcador, suponiendo que el objeto de **conjunto de registros** admite marcadores. Si no se especifica, el movimiento es relativo al registro actual.  
  
 Si está utilizando la propiedad [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) para almacenar en caché localmente los registros del proveedor, al pasar un argumento *NumRecords* que mueve la posición del registro actual fuera del grupo actual de registros almacenados en caché, ADO recupera un nuevo grupo de registros, empezando por el registro de destino. La propiedad **CacheSize** determina el tamaño del grupo recién recuperado y el registro de destino es el primer registro recuperado.  
  
 Si el objeto de **conjunto de registros** es de solo avance, un usuario puede pasar un argumento *NumRecords* menor que cero, siempre que el destino esté dentro del conjunto actual de registros almacenados en caché. Si la llamada a **Move** movería la posición del registro actual a un registro antes del primer registro almacenado en caché, se producirá un error. Por lo tanto, puede usar una memoria caché de registros que admita el desplazamiento completo a través de un proveedor que admita solo el desplazamiento hacia delante. Dado que los registros almacenados en caché se cargan en la memoria, debe evitar almacenar en caché más registros de los necesarios. Aunque un objeto de conjunto de **registros** de solo avance admita movimientos hacia atrás de esta manera, al llamar al método [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) en cualquier objeto de **conjunto de registros** de solo avance se generará un error.  
  
> [!NOTE]
>  La compatibilidad para moverse hacia atrás en un **conjunto de registros** de solo avance no es predecible, dependiendo del proveedor. Si el registro actual se ha colocado después del último registro del **conjunto de registros**, es posible que el **desplazamiento** hacia atrás no dé como resultado la posición actual correcta.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo del método move (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Ejemplo del método move (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Ejemplo del método move (VC + +)](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [Métodos MoveFirst, MoveLast, MoveNext y MovePrevious (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Métodos MoveFirst, MoveLast, MoveNext y MovePrevious (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
