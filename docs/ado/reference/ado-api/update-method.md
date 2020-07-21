---
title: Método Update | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Update
helpviewer_keywords:
- Update method [ADO]
ms.assetid: 6b2a9c31-1a7e-40db-8a53-30720d0f6cc1
author: rothja
ms.author: jroth
ms.openlocfilehash: 6c0d75e8f9fb6d11315e327edd6f7d064c13e063
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759501"
---
# <a name="update-method"></a>Update (método)
Guarda los cambios realizados en la fila actual de un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) o la colección de [campos](../../../ado/reference/ado-api/fields-collection-ado.md) de un objeto de [registro](../../../ado/reference/ado-api/record-object-ado.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Fields*  
 Opcional. **Variante** que representa un nombre único o una matriz de **variantes** que representa los nombres o posiciones ordinales del campo o los campos que desea modificar.  
  
 *Valores*  
 Opcional. **Variante** que representa un valor único o una matriz de **variantes** que representa los valores para el campo o los campos del nuevo registro.  
  
## <a name="remarks"></a>Observaciones  
  
## <a name="recordset"></a>DataRecordsets  
 Utilice el método **Update** para guardar los cambios realizados en el registro actual de un objeto de **conjunto de registros** desde la llamada al método [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) o desde la modificación de los valores de campo de un registro existente. El objeto de **conjunto de registros** debe admitir actualizaciones.  
  
 Para establecer los valores de los campos, realice una de las acciones siguientes:  
  
-   Asigne valores a la propiedad [Value](../../../ado/reference/ado-api/value-property-ado.md) de un objeto [Field](../../../ado/reference/ado-api/field-object.md) y llame al método **Update** .  
  
-   Pase un nombre de campo y un valor como argumentos con la llamada de **actualización** .  
  
-   Pase una matriz de nombres de campo y una matriz de valores con la llamada de **actualización** .  
  
 Cuando se usan matrices de campos y valores, debe haber un número igual de elementos en ambas matrices. Además, el orden de los nombres de campo debe coincidir con el orden de los valores de campo. Si el número y el orden de los campos y valores no coinciden, se produce un error.  
  
 Si el objeto de **conjunto de registros** admite la actualización por lotes, puede almacenar en caché varios cambios en uno o más registros localmente hasta que se llame al método [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) . Si está editando el registro actual o agregando un nuevo registro cuando se llama al método **UpdateBatch** , ADO llamará automáticamente al método **Update** para guardar los cambios pendientes en el registro actual antes de transmitir los cambios por lotes al proveedor.  
  
 Si se mueve del registro que está agregando o editando antes de llamar al método **Update** , ADO llamará automáticamente a **Update** para guardar los cambios. Debe llamar al método [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) si desea cancelar los cambios realizados en el registro actual o descartar un registro recién agregado.  
  
 El registro actual sigue siendo actual después de llamar al método **Update** .  
  
## <a name="record"></a>Registro  
 El método **Update** finaliza las adiciones, eliminaciones y actualizaciones de los campos de la colección [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de un objeto **Record** .  
  
 Por ejemplo, los campos eliminados con el método **Delete** se marcan para su eliminación inmediatamente, pero permanecen en la colección. Se debe llamar al método **Update** para eliminar realmente estos campos de la colección del proveedor.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Fields (colección) (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de los métodos Update y CancelUpdate (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Ejemplo de los métodos Update y CancelUpdate (VC + +)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew (método) (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [CancelUpdate (método) (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Propiedad EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
