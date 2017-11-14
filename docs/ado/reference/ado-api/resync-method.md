---
title: "Método Resync | Documentos de Microsoft"
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
- Recordset20::raw_Resync
- Fields::Resync
- Recordset20::Resync
- Fields::raw_Resync
helpviewer_keywords:
- Resync method [ADO]
ms.assetid: 73b355d4-a4c0-434b-bfc4-039b1c76b32e
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 392dd82f2b6412c537a86cc68331cffc852069b8
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="resync-method"></a>Método Resync
Actualiza los datos en este [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, o [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección de un [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto de la base de datos subyacente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>Parámetros  
 *AffectRecords*  
 Opcional. Un [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valor que determina cuántos registros la **Resync** afectará a método. El valor predeterminado es **adAffectAll**. Este valor no está disponible con la **Resync** método de la **campos** colección de un **registro** objeto.  
  
 *ResyncValues*  
 Opcional. A [ResyncEnum](../../../ado/reference/ado-api/resyncenum.md) valor que especifica si se sobrescriben los valores subyacentes. El valor predeterminado es **adResyncAllValues**.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="recordset"></a>Conjunto de registros  
 Use la **Resync** método para volver a sincronizar los registros actual **Recordset** con la base de datos subyacente. Esto es útil si está utilizando un cursor estático o de solo avance, pero desea ver los cambios en la base de datos subyacente.  
  
 Si establece la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad **adUseClient**, **Resync** solo está disponible para no son de solo lectura **Recordset** objetos.  
  
 A diferencia de la [Requery](../../../ado/reference/ado-api/requery-method.md) método, el **Resync** método no vuelva a ejecutar la **Recordset** comando subyacente del objeto. Nuevos registros en la base de datos subyacente no serán visibles.  
  
 Si se produce un error en el intento de volver a sincronizar debido a un conflicto con los datos subyacentes (por ejemplo, otro usuario ha eliminado un registro), el proveedor devuelve advertencias a la [errores](../../../ado/reference/ado-api/errors-collection-ado.md) se produce un error en tiempo de ejecución y colección. Use la [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad (**adFilterConflictingRecords**) y la [estado](../../../ado/reference/ado-api/status-property-ado-recordset.md) propiedad para localizar los registros con conflictos.  
  
 Si el [tabla única](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) y [Resync Command](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) se establecen las propiedades dinámicas y el **Recordset** es el resultado de ejecutar una operación JOIN en varias tablas y, a continuación, el  **Resincronizar** método ejecutará el comando especificado en el **Resync Command** propiedad solo en la tabla mencionada en el **tabla única** propiedad.  
  
## <a name="fields"></a>Campos  
 Use la **Resync** método para volver a sincronizar los valores de la **campos** colección de un **registro** objeto con el origen de datos subyacente. El [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad no se ve afectada por este método.  
  
 Si *ResyncValues* está establecido en **adResyncAllValues** (el valor predeterminado), el [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md), [valor](../../../ado/reference/ado-api/value-property-ado.md), y [ OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) propiedades de [campo](../../../ado/reference/ado-api/field-object.md) se sincronizan los objetos de la colección. Si *ResyncValues* está establecido en **adResyncUnderlyingValues**, solo el **UnderlyingValue** propiedad está sincronizada.  
  
 El valor de la **estado** propiedad para cada **campo** objeto en el momento de la llamada también afecta al comportamiento de **Resync**. Para **campo** objetos que tienen **estado** valores de **adFieldPendingUnknown** o **adFieldPendingInsert**, **Resync**  no tiene ningún efecto. Para **estado** valores de **adFieldPendingChange** o **adFieldPendingDelete**, **Resync** sincroniza los valores de datos para los campos que todavía existe en el origen de datos.  
  
 **Resincronizar** no modificará **estado** valores de **campo** objetos a menos que se produce un error cuando **Resync** se llama. Por ejemplo, si el campo ya no existe, el proveedor devolverá una adecuada **estado** valor para el **campo** objeto, como **adFieldDoesNotExist**. Devuelve **estado** valores pueden combinarse lógicamente dentro del valor de la **estado** propiedad.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Fields (colección) (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método (VB) Resync](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [Método ejemplo Resync (VC ++)](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Clear (método) (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Propiedad UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)

