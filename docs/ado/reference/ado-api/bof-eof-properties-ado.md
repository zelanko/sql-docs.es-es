---
title: BOF, EOF (propiedades) (ADO) | Documentos de Microsoft
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
- Recordset15::BOF
- Recordset15::EOF
helpviewer_keywords:
- EOF property [ADO]
- BOF property [ADO]
ms.assetid: 36c31ab2-f3b6-4281-89b6-db7e04e38fd2
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 93689aa347014fd3976645682a396230a38476e6
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="bof-eof-properties-ado"></a>BOF, EOF (propiedades) (ADO)
-   **BOF** indica que la posición del registro actual está delante del primer registro en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
-   **EOF** indica que la posición del registro actual se sitúa después del último registro en un **Recordset** objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 El **BOF** y **EOF** devuelven propiedades **booleano** valores.  
  
## <a name="remarks"></a>Comentarios  
 Use la **BOF** y **EOF** propiedades para determinar si un **Recordset** objeto contiene registros o si ha ido más allá de los límites de un **conjunto de registros ** objeto cuando se mueve de un registro a otro.  
  
 El **BOF** propiedad devuelve **True** (-1) si la posición del registro actual está delante del primer registro y **False** (0) si la posición del registro actual está en o después del primero registro.  
  
 El **EOF** propiedad devuelve **True** si la posición del registro actual está después del último registro y **False** si la posición del registro actual está en o antes del último registro.  
  
 Si el **BOF** o **EOF** propiedad es **True**, no hay ningún registro actual.  
  
 Si abre un **Recordset** objeto que no contiene registros, la **BOF** y **EOF** propiedades se establecen en **True** (consulte la [ RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) propiedad para obtener más información sobre este estado de un **Recordset**). Cuando se abre un **Recordset** objeto que contiene al menos un registro, el primer registro es el registro actual y la **BOF** y **EOF** propiedades son **False **.  
  
 Si elimina el último registro que queda en el **Recordset** objeto, el **BOF** y **EOF** propiedades pueden permanecer **False** hasta que Intente volver a colocar el registro actual.  
  
 Esta tabla muestra qué **mover** se permiten métodos con diferentes combinaciones de la **BOF** y **EOF** propiedades.  
  
||MoveFirst,<br /><br /> MoveLast|MovePrevious,<br /><br /> Mover < 0|Mover 0|MoveNext,<br /><br /> Mover > 0|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF**=**True**, **EOF**=**False**|Permitido|Error|Error|Permitido|  
|**BOF**=**False**, **EOF**=**True**|Permitido|Permitido|Error|Error|  
|Ambos **True**|Error|Error|Error|Error|  
|Ambos **False**|Permitido|Permitido|Permitido|Permitido|  
  
 Lo que permite un **mover** método no garantiza que busque correctamente un registro; sólo significa que al llamar a especificado **mover** método no generará un error.  
  
 En la tabla siguiente se muestra lo que ocurre con la **BOF** y **EOF** valores de las propiedades cuando se llama a diversos **mover** métodos son pero no se puede encontrar un registro.  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**, **MoveLast**|Establecido en **es True**|Establecido en **es True**|  
|**Mover** 0|No hay ningún cambio|No hay ningún cambio|  
|**MovePrevious**, **mover** < 0|Establecido en **es True**|No hay ningún cambio|  
|**MoveNext**, **mover** > 0|No hay ningún cambio|Establecido en **es True**|  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [BOF, EOF y ejemplo de propiedades de marcador (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF, EOF y ejemplo de propiedades de marcador (VC ++)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   

