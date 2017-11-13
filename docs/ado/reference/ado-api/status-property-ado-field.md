---
title: Propiedad Status (Field ADO) | Documentos de Microsoft
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
- Field::Status
- Field::get_Status
- Field::GetStatus
helpviewer_keywords:
- Status property [ADO Field]
ms.assetid: 8cd1f7f4-0a3a-4f07-b8ba-6582e70140ad
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 65acf492f0364b26fa6a12240fbbd49c7d1dfed3
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="status-property-ado-field"></a>Propiedad Status (Field ADO)
Indica el estado de un [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) valor. El valor predeterminado es **adFieldOK**.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="record-field-status"></a>Estado de campos de registro  
 Cambios en el valor de un **campo** objeto de la colección de campos de un [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto se almacenan en caché hasta que el objeto [actualización](../../../ado/reference/ado-api/update-method.md) se llama al método. En ese momento, si el cambio en el valor del campo se ha producido un error, OLE DB genera el error **DB_E_ERRORSOCCURRED** (2147749409). La propiedad Status de cualquiera de los **campo** objetos en el **campos** colección que ha causado el error contendrá un valor de la [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) que describe la causa de el problema.  
  
 Para mejorar el rendimiento, las adiciones y eliminaciones para la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colecciones de la **registro** objeto se almacenan en caché hasta que el **actualización** método se llama y, a continuación, los cambios se realizan en una actualización optimista por lotes. Si el **actualización** método no se llama, el servidor no se actualiza. Si se producirá un error en todas las actualizaciones, a continuación, se devuelve un error de proveedor de OLE DB (DB_E_ERRORSOCCURRED) y la **estado** propiedad indica los valores combinados de la operación y estado código de error. Por ejemplo, **adFieldPendingInsert OR adFieldPermissionDenied**. El **estado** propiedad para cada **campo** puede usarse para determinar por qué la **campo** se agregó, modificó o eliminó no.  
  
 Muchos tipos de problemas encontrados al agregar, modificar o eliminar una **campo** se notifican mediante la **estado** propiedad. Por ejemplo, si el usuario elimina una **campo**, está marcado para su eliminación de la **campos** colección. Si la subsiguiente **actualización** devuelve un error porque el usuario intentó eliminar un **campo** para los que no tienen permiso, la **campo** tendrá un  **Estado** de **adFieldPermissionDenied OR adFieldPendingDelete**. Llamar a la [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) valores originales de restauraciones de método y establece el **estado** a **adFieldOK**.  
  
 De forma similar, el **actualización** método puede devolver un error debido a un nuevo **campo** se haya agregado y otorgado un valor inadecuado. En ese caso el nuevo **campo** estará en el **campos** colección y tienen un estado de **adFieldPendingInsert** y quizás **adFieldCantCreate** (dependiendo de su proveedor). Puede proporcionar un valor adecuado para el nuevo **campo** y llame a **actualización** nuevo.  
  
## <a name="recordset-field-status"></a>Estado de campos de conjunto de registros  
 Cambios en el valor de un **campo** objeto de la colección de campos de uno de ellos un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) se almacenan en caché hasta que el objeto [actualización](../../../ado/reference/ado-api/update-method.md) se llama al método. En ese momento, si el cambio en el valor del campo se ha producido un error, OLE DB genera el error **DB_E_ERRORSOCCURRED** (2147749409). La propiedad Status de cualquiera de los **campo** objetos en el **campos** colección que ha causado el error contendrá un valor de la [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) que describe la causa de el problema.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad de estado (campo) (VB)](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [Ejemplo de la propiedad de estado (VC ++)](../../../ado/reference/ado-api/status-property-example-vc.md)   

