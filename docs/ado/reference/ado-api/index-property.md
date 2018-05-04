---
title: Index (propiedad) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset21::Index
helpviewer_keywords:
- Index property
ms.assetid: 1c79e271-21ec-41a8-8163-c5e89f0001a7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01e7883719900e85fdb7227f50c90ed265f73c30
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="index-property"></a>Propiedad Index
Indica el nombre del índice actualmente en vigor para un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** valor, que es el nombre del índice.  
  
## <a name="remarks"></a>Comentarios  
 El índice denominado por la **índice** propiedad debe haber sido declarada previamente en la tabla base subyacente la **Recordset** objeto. Es decir, el índice debe haber sido declarado mediante programación como un ADOX [índice](../../../ado/reference/adox-api/index-object-adox.md) objeto, o cuando se creó la tabla base.  
  
 Si no se puede establecer el índice, se producirá un error de tiempo de ejecución. El **índice** no se puede establecer la propiedad en las siguientes condiciones:  
  
-   Dentro de un [WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) o **RecordsetChangeComplete** controlador de eventos.  
  
-   Si el **Recordset** todavía se está ejecutando una operación (que se puede determinar mediante el [estado](../../../ado/reference/ado-api/state-property-ado.md) propiedad).  
  
-   Si se ha establecido un filtro en el **Recordset** con el [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad.  
  
 El **índice** propiedad puede establecerse siempre correctamente si la **Recordset** está cerrada, pero la **Recordset** no abrirá correctamente o el índice no se podrá usar, si el proveedor subyacente no admite índices.  
  
 Si se puede establecer el índice, puede cambiar la posición de fila actual. Esto hará que una actualización de la [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) propiedad y se activará la **WillChangeRecordset**, **RecordsetChangeComplete**, [WillMove ](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), y [MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md) eventos.  
  
 Si se puede establecer el índice y la [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) propiedad es **adLockPessimistic** o **adLockOptimistic**, a continuación, implícita [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) se realiza la operación. Esto libera los grupos afectados y actuales. Se liberan todos los filtros existentes, y se cambia la posición de fila actual a la primera fila de la que se vuelve a pedir **conjunto de registros**.  
  
 El **índice** propiedad se utiliza junto con la [Seek](../../../ado/reference/ado-api/seek-method.md) método. Si el proveedor subyacente no admite la **índice** propiedad y, por tanto, la **Seek** método, considere el uso de la [buscar](../../../ado/reference/ado-api/find-method-ado.md) método en su lugar. Determinar si la **Recordset** objeto admite índices con el [admite](../../../ado/reference/ado-api/supports-method.md)**(adIndex)** método.  
  
 Integrado **índice** propiedad no está relacionada con dinámico [optimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propiedad, aunque ambas tienen que ver con los índices.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método Seek y ejemplo de la propiedad de índice (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Objeto Index (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [El método de búsqueda](../../../ado/reference/ado-api/seek-method.md)
