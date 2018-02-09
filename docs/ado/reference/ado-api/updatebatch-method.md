---
title: "Método UpdateBatch | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
- Recordset15::UpdateBatch
- Recordset15::raw_UpdateBatch
helpviewer_keywords:
- UpdateBatch method [ADO]
ms.assetid: 23f9314c-b027-4a51-aeae-50caa2977740
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5da32525c4ff0d04c19704efd2aa04050d3db93d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="updatebatch-method"></a>Método UpdateBatch
Escribe todas las actualizaciones por lotes pendientes en el disco.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>Parámetros  
 *AffectRecords*  
 Opcional. Un [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valor que indica cuántos registros la **UpdateBatch** afectará a método.  
  
 *PreserveStatus*  
 Opcional. A **booleano** valor que especifica si se permite o no los cambios realizados localmente, tal y como indica la [estado](../../../ado/reference/ado-api/status-property-ado-recordset.md) propiedad, se debería confirmar. Si este valor se establece en **True**, **estado** no cambie la propiedad de cada registro una vez completada la actualización.  
  
## <a name="remarks"></a>Comentarios  
 Use la **UpdateBatch** método cuando se modifica un **Recordset** objeto en modo de actualización por lotes para transmitir todos los cambios realizados en un **Recordset** objeto a la base de datos subyacente.  
  
 Si el **Recordset** objeto admite la actualización por lotes, puede almacenar en caché cualquier cambio múltiple en uno o más registros localmente hasta que llame a la **UpdateBatch** método. Si está modificando el registro actual o agregando un nuevo registro cuando se llama a la **UpdateBatch** método, ADO llamará automáticamente el [actualización](../../../ado/reference/ado-api/update-method.md) método para guardar los cambios pendientes en el registro actual antes de transmitir los cambios por lotes al proveedor. Debe usar la actualización por lotes con un conjunto de claves o un cursor estático solo.  
  
> [!NOTE]
>  Especificar **adAffectGroup** que el valor para este parámetro, se producirá un error cuando no hay ningún registro visible actual **Recordset** (por ejemplo, un filtro para el que no hay registros que coincidan con).  
  
 Si falla el intento de transmitir los cambios de algunos o todos los registros debido a un conflicto con los datos subyacentes (por ejemplo, otro usuario ya ha eliminado un registro), el proveedor devuelve advertencias a la [errores](../../../ado/reference/ado-api/errors-collection-ado.md) colección y un se produce el error en tiempo de ejecución. Use la [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad (**adFilterAffectedRecords**) y la [estado](../../../ado/reference/ado-api/status-property-ado-recordset.md) propiedad para localizar los registros con conflictos.  
  
 Para cancelar todas las pendientes las actualizaciones por lotes, utilice la [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) método.  
  
 Si el [tabla única](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) y [Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) se establecen las propiedades dinámicas y el **Recordset** es el resultado de ejecutar una operación JOIN en varias tablas, el ejecución de la **UpdateBatch** método va seguido de forma implícita la [Resync](../../../ado/reference/ado-api/resync-method.md) método, según la configuración de la [Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) propiedad.  
  
 El orden en el que se realizan las actualizaciones individuales de un lote en el origen de datos no es necesariamente el mismo que el orden en el que se realizaron en el equipo local **conjunto de registros**. Orden de actualización depende del proveedor. Tenerlo en cuenta al codificar las actualizaciones que se relacionan entre sí, como las restricciones de clave externa en una inserción o actualización.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo UpdateBatch y CancelBatch métodos (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [Ejemplo UpdateBatch y CancelBatch métodos (VC ++)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Clear (método) (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Propiedad LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Update (método)](../../../ado/reference/ado-api/update-method.md)
