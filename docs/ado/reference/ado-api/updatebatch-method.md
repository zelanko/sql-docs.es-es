---
title: Método UpdateBatch | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::UpdateBatch
- Recordset15::raw_UpdateBatch
helpviewer_keywords:
- UpdateBatch method [ADO]
ms.assetid: 23f9314c-b027-4a51-aeae-50caa2977740
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e9d74fe938ce486a4cd15573af8166dbed12ba6f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67937841"
---
# <a name="updatebatch-method"></a>Método UpdateBatch
Escribe todas las actualizaciones de Batch pendientes en el disco.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>Parámetros  
 *AffectRecords*  
 Opcional. Valor de [AffectEnum](../../../ado/reference/ado-api/affectenum.md) que indica el número de registros a los que afectará el método **UpdateBatch** .  
  
 *PreserveStatus*  
 Opcional. Valor **booleano** que especifica si se deben confirmar o no los cambios locales, como indica la propiedad de [Estado](../../../ado/reference/ado-api/status-property-ado-recordset.md) . Si este valor se establece en **true**, la propiedad **status** de cada registro permanece sin cambios una vez completada la actualización.  
  
## <a name="remarks"></a>Observaciones  
 Use el método **UpdateBatch** al modificar un objeto de **conjunto de registros** en modo de actualización por lotes para transmitir todos los cambios realizados en un objeto de conjunto de **registros** a la base de datos subyacente.  
  
 Si el objeto de **conjunto de registros** admite la actualización por lotes, puede almacenar en caché varios cambios en uno o más registros localmente hasta que se llame al método **UpdateBatch** . Si está editando el registro actual o agregando un nuevo registro cuando se llama al método **UpdateBatch** , ADO llamará automáticamente al método [Update](../../../ado/reference/ado-api/update-method.md) para guardar los cambios pendientes en el registro actual antes de transmitir los cambios por lotes al proveedor. Debe usar la actualización por lotes solo con un cursor Keyset o static.  
  
> [!NOTE]
>  Si se especifica **adAffectGroup** como valor para este parámetro, se producirá un error cuando no haya registros visibles en el **conjunto de registros** actual (por ejemplo, un filtro para el que no coincidan los registros).  
  
 Si se produce un error al intentar transmitir los cambios para alguno o todos los registros debido a un conflicto con los datos subyacentes (por ejemplo, otro usuario ya ha eliminado un registro), el proveedor devuelve advertencias a la colección de [errores](../../../ado/reference/ado-api/errors-collection-ado.md) y se produce un error en tiempo de ejecución. Use la propiedad [Filter](../../../ado/reference/ado-api/filter-property.md) (**adFilterAffectedRecords**) y la propiedad [status](../../../ado/reference/ado-api/status-property-ado-recordset.md) para buscar registros con conflictos.  
  
 Para cancelar todas las actualizaciones de Batch pendientes, use el método [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) .  
  
 Si se establecen las propiedades dinámicas de [tabla única](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) y de [resincronización de actualizaciones](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) , y el **conjunto de registros** es el resultado de ejecutar una operación de combinación en varias tablas, la ejecución del método **UpdateBatch** va seguida implícitamente por el método [Resync](../../../ado/reference/ado-api/resync-method.md) , dependiendo de la configuración de la propiedad de [resincronización](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) de la actualización.  
  
 El orden en que se realizan las actualizaciones individuales de un lote en el origen de datos no es necesariamente el mismo que el orden en el que se realizaron en el **conjunto de registros**local. El orden de actualización depende del proveedor. Tenga esto en cuenta al codificar las actualizaciones relacionadas entre sí, como las restricciones Foreign Key en una instrucción INSERT o Update.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de los métodos UpdateBatch y CancelBatch (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [Ejemplo de los métodos UpdateBatch y CancelBatch (VC + +)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [CancelBatch (método) (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Clear (método) (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType (propiedad, ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Update (método)](../../../ado/reference/ado-api/update-method.md)
