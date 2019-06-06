---
title: Propiedad Status (Field ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field::Status
- Field::get_Status
- Field::GetStatus
helpviewer_keywords:
- Status property [ADO Field]
ms.assetid: 8cd1f7f4-0a3a-4f07-b8ba-6582e70140ad
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a647051e7953d6f2977074feda94cf7e9f3d9d82
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711014"
---
# <a name="status-property-ado-field"></a>Propiedad Status (Field ADO)
Indica el estado de un [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) valor. El valor predeterminado es **adFieldOK**.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="record-field-status"></a>Estado de campos de registro  
 Los cambios en el valor de un **campo** objeto de la colección de campos de un [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto se almacenan en caché hasta que el objeto [actualización](../../../ado/reference/ado-api/update-method.md) se llama al método. En ese momento, si el cambio en el valor del campo se ha producido un error, OLE DB genera el error **DB_E_ERRORSOCCURRED** (2147749409). La propiedad Status de cualquiera de los **campo** objetos en el **campos** recopilación que produjo el error contendrá un valor de la [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) que describe la causa de el problema.  
  
 Para mejorar el rendimiento, las adiciones y eliminaciones para la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colecciones de la **registro** objeto se almacenan en caché hasta que el **actualización** se llama el método y, a continuación, los cambios se realizan en una actualización optimista por lotes. Si el **actualización** no se llama al método, no se actualiza el servidor. Si las actualizaciones se producen errores, a continuación, se devuelve un error de proveedor OLE DB (DB_E_ERRORSOCCURRED) y el **estado** propiedad indica los valores combinados del código de estado de error y operación. Por ejemplo, **adFieldPendingInsert OR adFieldPermissionDenied**. El **estado** propiedad para cada **campo** puede usarse para determinar por qué la **campo** se agregó, modificó o eliminó no.  
  
 Muchos tipos de problemas encontrados al agregar, modificar o eliminar un **campo** se notifican a través de la **estado** propiedad. Por ejemplo, si el usuario elimina un **campo**, está marcada para eliminación desde el **campos** colección. Si la subsiguiente **actualización** devuelve un error porque el usuario intentó eliminar un **campo** para el que no tienen permiso, el **campo** tendrá un  **Estado** de **adFieldPermissionDenied OR adFieldPendingDelete**. Una llamada a la [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) valores originales de las restauraciones de método y establece el **estado** a **adFieldOK**.  
  
 De forma similar, el **actualización** método puede devolver un error debido a un nuevo **campo** se haya agregado y tiene un valor incorrecto. En ese caso, el nuevo **campo** estará en el **campos** colección y tienen un estado de **adFieldPendingInsert** y quizás **adFieldCantCreate** (dependiendo de su proveedor). Puede proporcionar un valor adecuado para el nuevo **campo** y llamar a **actualización** nuevo.  
  
## <a name="recordset-field-status"></a>Estado del campo de conjunto de registros  
 Los cambios en el valor de un **campo** objeto de la colección de campos de uno de ellos un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) se almacenan en caché hasta que el objeto [actualización](../../../ado/reference/ado-api/update-method.md) se llama al método. En ese momento, si el cambio en el valor del campo se ha producido un error, OLE DB genera el error **DB_E_ERRORSOCCURRED** (2147749409). La propiedad Status de cualquiera de los **campo** objetos en el **campos** recopilación que produjo el error contendrá un valor de la [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) que describe la causa de el problema.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad de estado (campo) (VB)](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [Ejemplo de la propiedad de estado (VC ++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
