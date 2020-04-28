---
title: CancelBatch (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_CancelBatch
- Recordset15::CancelBatch
helpviewer_keywords:
- CancelBatch method [ADO]
ms.assetid: dbdc2574-e44e-4d95-b03d-4a5d9e9adf3c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f1c6a9f57d30b47641b9280e25a97336c28b0496
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920166"
---
# <a name="cancelbatch-method-ado"></a>Método CancelBatch (ADO)
Cancela una actualización por lotes pendiente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>Parámetros  
 *AffectRecords*  
 Opcional. Valor de [AffectEnum](../../../ado/reference/ado-api/affectenum.md) que indica el número de registros a los que afectará el método **CancelBatch** .  
  
## <a name="remarks"></a>Observaciones  
 Use el método **CancelBatch** para cancelar todas las actualizaciones pendientes en un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) en modo de actualización por lotes. Si el **conjunto de registros** está en modo de actualización inmediata, al llamar a **CancelBatch** sin **adAffectCurrent** se genera un error.  
  
 Si está editando el registro actual o está agregando un nuevo registro cuando se llama a **CancelBatch**, ADO llama primero al método [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) para cancelar los cambios almacenados en caché. Después, se cancelan todos los cambios pendientes en el **conjunto de registros** .  
  
 El registro actual puede ser indeterminable después de una llamada a **CancelBatch** , especialmente si estaba en el proceso de agregar un nuevo registro. Por esta razón, es prudente establecer la posición del registro actual en una ubicación conocida del conjunto de **registros** después de la llamada a **CancelBatch** . Por ejemplo, llame al método [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) .  
  
 Si se produce un error al intentar cancelar las actualizaciones pendientes debido a un conflicto con los datos subyacentes (por ejemplo, si otro usuario ha eliminado un registro), el proveedor devuelve advertencias a la colección de [errores](../../../ado/reference/ado-api/errors-collection-ado.md) , pero no detiene la ejecución del programa. Solo se produce un error en tiempo de ejecución si hay conflictos en todos los registros solicitados. Use la propiedad [Filter](../../../ado/reference/ado-api/filter-property.md) (**adFilterAffectedRecords**) y la propiedad [status](../../../ado/reference/ado-api/status-property-ado-recordset.md) para buscar registros con conflictos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de los métodos UpdateBatch y CancelBatch (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [Ejemplo de los métodos UpdateBatch y CancelBatch (VC + +)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [CANCEL (método) (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Método CANCEL (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelUpdate (método) (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Clear (método) (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType (propiedad, ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
