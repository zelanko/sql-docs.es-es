---
title: Método Resync | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_Resync
- Fields::Resync
- Recordset20::Resync
- Fields::raw_Resync
helpviewer_keywords:
- Resync method [ADO]
ms.assetid: 73b355d4-a4c0-434b-bfc4-039b1c76b32e
author: rothja
ms.author: jroth
ms.openlocfilehash: 6907bfa9b83370074db9d9e2e522ed49d2c96e7e
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243216"
---
# <a name="resync-method"></a>Método Resync
Actualiza los datos del objeto de conjunto de [registros](../../../ado/reference/ado-api/recordset-object-ado.md) actual, o la colección de [campos](../../../ado/reference/ado-api/fields-collection-ado.md) de un objeto de [registro](../../../ado/reference/ado-api/record-object-ado.md) , de la base de datos subyacente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>Parámetros  
 *AffectRecords*  
 Opcional. Valor de [AffectEnum](../../../ado/reference/ado-api/affectenum.md) que determina el número de registros a los que afectará el método **Resync** . El valor predeterminado es **adAffectAll**. Este valor no está disponible con el método **Resync** de la colección **Fields** de un objeto **Record** .  
  
 *ResyncValues*  
 Opcional. Valor [ResyncEnum](../../../ado/reference/ado-api/resyncenum.md) que especifica si se sobrescriben los valores subyacentes. El valor predeterminado es **adResyncAllValues**.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="recordset"></a>DataRecordsets  
 Use el método **Resync** para volver a sincronizar los registros del **conjunto de registros** actual con la base de datos subyacente. Esto resulta útil si usa un cursor estático o de solo avance, pero desea ver los cambios en la base de datos subyacente.  
  
 Si establece la propiedad [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) en **adUseClient**, **Resync** solo está disponible para los objetos de conjunto de **registros** que no son de solo lectura.  
  
 A diferencia del método [Requery](../../../ado/reference/ado-api/requery-method.md) , el método **Resync** no vuelve a ejecutar el comando subyacente del objeto de **conjunto de registros** . Los nuevos registros de la base de datos subyacente no estarán visibles.  
  
 Si se produce un error al intentar volver a sincronizar debido a un conflicto con los datos subyacentes (por ejemplo, otro usuario ha eliminado un registro), el proveedor devuelve advertencias a la colección de [errores](../../../ado/reference/ado-api/errors-collection-ado.md) y se produce un error en tiempo de ejecución. Use la propiedad [Filter](../../../ado/reference/ado-api/filter-property.md) (**adFilterConflictingRecords**) y la propiedad [status](../../../ado/reference/ado-api/status-property-ado-recordset.md) para buscar registros con conflictos.  
  
 Si se establecen las propiedades dinámicas [tabla única](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) y [comando de resincronización](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) , y el **conjunto de registros** es el resultado de ejecutar una operación de combinación en varias tablas, el método **Resync** ejecutará el comando proporcionado en la propiedad **comando Resync** solo en la tabla denominada en la propiedad de **tabla única** .  
  
## <a name="fields"></a>Fields  
 Use el método **Resync** para volver a sincronizar los valores de la colección **Fields** de un objeto **Record** con el origen de datos subyacente. Este método no afecta a la propiedad [Count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
 Si *ResyncValues* se establece en **adResyncAllValues** (el valor predeterminado), se sincronizan las propiedades [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md), [Value](../../../ado/reference/ado-api/value-property-ado.md)y [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) de los objetos de [campo](../../../ado/reference/ado-api/field-object.md) de la colección. Si *ResyncValues* se establece en **adResyncUnderlyingValues**, solo se sincroniza la propiedad **UnderlyingValue** .  
  
 El valor de la propiedad **status** de cada objeto **Field** en el momento de la llamada también afecta al comportamiento de **Resync**. En el caso de los objetos de **campo** que tienen valores de **Estado** de **adFieldPendingUnknown** o **adFieldPendingInsert**, **Resync** no tiene ningún efecto. En el caso de los valores de **Estado** de **adFieldPendingChange** o **adFieldPendingDelete**, **Resync** sincroniza los valores de datos de los campos que todavía existen en el origen de datos.  
  
 **Resync** no modificará los valores de **Estado** de los objetos de **campo** a menos que se produzca un error cuando se llame a **Resync** . Por ejemplo, si el campo ya no existe, el proveedor devolverá un valor de **Estado** adecuado para el objeto de **campo** , como **adFieldDoesNotExist**. Los valores de **Estado** devueltos se pueden combinar lógicamente dentro del valor de la propiedad **status** .  
  
## <a name="applies-to"></a>Se aplica a  

:::row:::
    :::column:::
        [Fields (colección) (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte también  
 [Ejemplo del método Resync (VB)](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [Ejemplo del método Resync (VC + +)](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Clear (método) (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Propiedad UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)
