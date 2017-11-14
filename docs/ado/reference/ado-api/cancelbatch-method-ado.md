---
title: "Método CancelBatch (ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::raw_CancelBatch
- Recordset15::CancelBatch
helpviewer_keywords:
- CancelBatch method [ADO]
ms.assetid: dbdc2574-e44e-4d95-b03d-4a5d9e9adf3c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2eced52fb03d47d8f79838d07a45c1d8dde31cf9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="cancelbatch-method-ado"></a>Método CancelBatch (ADO)
Cancela una actualización por lotes pendientes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>Parámetros  
 *AffectRecords*  
 Opcional. Un [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valor que indica cuántos registros la **CancelBatch** afectará a método.  
  
## <a name="remarks"></a>Comentarios  
 Use la **CancelBatch** método para cancelar cualquier actualización pendiente en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) en modo de actualización por lotes. Si el **Recordset** está en modo de actualización inmediata, una llamada a **CancelBatch** sin **adAffectCurrent** genera un error.  
  
 Si está modificando el registro actual o agregando un nuevo registro cuando se llama a **CancelBatch**, ADO primero llama el [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método para cancelarlos cambios almacenados en caché. Después de eso, todos los cambios pendientes en el **Recordset** se cancelan.  
  
 El registro actual puede ser después de un **CancelBatch** llamar, sobre todo si se estaba agregando un nuevo registro. Por esta razón, es recomendable establecer la posición del registro actual en una ubicación conocida en el **Recordset** después de la **CancelBatch** llamar. Por ejemplo, llamar a la [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) método.  
  
 Si se produce un error en el intento de cancelar las actualizaciones pendientes debido a un conflicto con los datos subyacentes (por ejemplo, si se ha eliminado un registro por otro usuario), el proveedor devuelve advertencias a la [errores](../../../ado/reference/ado-api/errors-collection-ado.md) colección, pero no detiene ejecución del programa. Se produce un error de tiempo de ejecución sólo si hay conflictos en todos los registros solicitados. Use la [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad (**adFilterAffectedRecords**) y la [estado](../../../ado/reference/ado-api/status-property-ado-recordset.md) propiedad para localizar los registros con conflictos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo UpdateBatch y CancelBatch métodos (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [Ejemplo UpdateBatch y CancelBatch métodos (VC ++)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Cancel (método) (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel (método) (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Clear (método) (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Propiedad LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)

