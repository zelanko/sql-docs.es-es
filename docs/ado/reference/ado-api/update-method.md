---
title: "El método Update | Documentos de Microsoft"
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
- Recordset15::Update
helpviewer_keywords:
- Update method [ADO]
ms.assetid: 6b2a9c31-1a7e-40db-8a53-30720d0f6cc1
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 287fb5bf8b87a8371ee84d89ba4e5efee6b3587f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="update-method"></a>Update (método)
Guarda los cambios realizados en la fila actual de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, o el [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección de un [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Campos*  
 Opcional. A **Variant** que representa un nombre único, o un **Variant** matriz que representa los nombres o las posiciones ordinales del campo o campos que se va a modificar.  
  
 *Valores*  
 Opcional. A **Variant** que representa un valor único, o un **Variant** matriz que representa los valores para el campo o campos en el nuevo registro.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="recordset"></a>Conjunto de registros  
 Use la **actualización** método para guardar los cambios que realice en el registro actual de un **conjunto de registros** objeto desde el que realiza la llamada la [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) método o cambiando los valores de campo en un registro existente. El **Recordset** objeto debe admitir las actualizaciones.  
  
 Para establecer valores de campo, realice una de las siguientes acciones:  
  
-   Asignar valores a un [campo](../../../ado/reference/ado-api/field-object.md) del objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad y llame al método el **actualización** método.  
  
-   Pasar un nombre de campo y un valor como argumentos con la **actualización** llamar.  
  
-   Pasar una matriz de nombres de campo y una matriz de valores con el **actualización** llamar.  
  
 Cuando utiliza matrices de campos y valores, debe ser un número igual de elementos de ambas matrices. Además, el orden de los nombres de campo debe coincidir con el orden de los valores de campo. Si el número y el orden de los campos y valores no coinciden, se produce un error.  
  
 Si el **Recordset** objeto admite la actualización por lotes, puede almacenar en caché cualquier cambio múltiple en uno o más registros localmente hasta que llame a la [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método. Si está modificando el registro actual o agregando un nuevo registro cuando se llama a la **UpdateBatch** método, ADO llamará automáticamente el **actualización** método para guardar los cambios pendientes en el registro actual antes de transmitir los cambios por lotes al proveedor.  
  
 Si se mueve desde el registro que está agregando o editando antes de llamar a la **actualización** método, ADO llamará automáticamente **actualización** para guardar los cambios. Debe llamar a la [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método si desea cancelar los cambios realizados en el registro actual o descartar un registro recién agregado.  
  
 El registro actual se mantiene actual después de llamar a la **actualización** método.  
  
## <a name="record"></a>Grabar  
 El **actualización** método finaliza las adiciones, eliminaciones y actualizaciones a los campos de la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección de un **registro** objeto.  
  
 Por ejemplo, los campos eliminados con el **eliminar** método quedan inmediatamente marcados para su eliminación pero permanecen en la colección. El **actualización** método debe llamarse para eliminar realmente estos campos de la colección del proveedor.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Fields (colección) (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Vea también  
 [Actualización y ejemplo de los métodos CancelUpdate (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Actualización y ejemplo de los métodos CancelUpdate (VC ++)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew (método) (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Propiedad EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
