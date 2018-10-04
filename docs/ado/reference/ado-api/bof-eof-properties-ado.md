---
title: BOF, EOF (propiedades) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::BOF
- Recordset15::EOF
helpviewer_keywords:
- EOF property [ADO]
- BOF property [ADO]
ms.assetid: 36c31ab2-f3b6-4281-89b6-db7e04e38fd2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72954cb199976f05eacd7c79ba0e89cab0a45bbc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47748123"
---
# <a name="bof-eof-properties-ado"></a>BOF, EOF (propiedades) (ADO)
-   **BOF** indica que la posición actual del registro es antes del primer registro en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
-   **EOF** indica que es la posición actual del registro después del último registro en un **Recordset** objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 El **BOF** y **EOF** devuelven propiedades **booleano** valores.  
  
## <a name="remarks"></a>Comentarios  
 Use la **BOF** y **EOF** propiedades para determinar si un **Recordset** objeto contiene registros o si se ha desplazado más allá de los límites de un **conjunto de registros**  objeto cuando se mueve de un registro a otro.  
  
 El **BOF** propiedad devuelve **True** (-1) si la posición actual del registro es antes del primer registro y **False** (0) si la posición actual del registro está en o después del primer registro.  
  
 El **EOF** propiedad devuelve **True** si es la posición actual del registro después del último registro y **False** si la posición actual del registro está en o antes del último registro.  
  
 Si el **BOF** o **EOF** propiedad es **True**, no hay ningún registro actual.  
  
 Si abre un **Recordset** objeto que no contiene registros, la **BOF** y **EOF** propiedades se establecen en **True** (consulte la [ RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) propiedad para obtener más información sobre este estado de un **Recordset**). Al abrir un **Recordset** objeto que contiene al menos un registro, el primer registro es el registro actual y el **BOF** y **EOF** propiedades son **False** .  
  
 Si elimina el último registro que queda en el **Recordset** objeto, el **BOF** y **EOF** propiedades pueden permanecer **False** hasta que intenta colocar el registro actual.  
  
 Esta tabla muestra qué **mover** se permiten métodos con diferentes combinaciones de la **BOF** y **EOF** propiedades.  
  
||Métodos MoveFirst,<br /><br /> MoveLast|MovePrevious,<br /><br /> Mover < 0|Mover 0|MoveNext,<br /><br /> Mover > 0|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF**=**True**, **EOF**=**False**|Permitido|Error|Error|Permitido|  
|**BOF**=**False**, **EOF**=**True**|Permitido|Permitido|Error|Error|  
|Ambos **True**|Error|Error|Error|Error|  
|Ambos **False**|Permitido|Permitido|Permitido|Permitido|  
  
 Lo que permite un **mover** método no garantiza que busque correctamente un registro; sólo significa que al llamar al especificado **mover** método no generará un error.  
  
 En la tabla siguiente se muestra lo que ocurre en el **BOF** y **EOF** valores de propiedad cuando se llama a varios **mover** métodos son pero no se puede encontrar un registro.  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**, **MoveLast**|Establecido en **True**|Establecido en **True**|  
|**Mover** 0|Sin cambios|Sin cambios|  
|**MovePrevious**, **mover** < 0|Establecido en **True**|Sin cambios|  
|**MoveNext**, **mover** > 0|Sin cambios|Establecido en **True**|  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [BOF, EOF y Bookmark propiedades ejemplo (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF, EOF y Bookmark ejemplo de propiedades (VC ++)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
