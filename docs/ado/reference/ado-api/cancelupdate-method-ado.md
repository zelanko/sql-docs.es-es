---
title: "Método CancelUpdate (ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset15::CancelUpdate
helpviewer_keywords: CancelUpdate method [ADO]
ms.assetid: eaa856cc-c786-462e-890c-c896261b1741
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6d283ceca9e6d5caa7a624f7ef250540c23df84c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="cancelupdate-method-ado"></a>Método CancelUpdate (ADO)
Cancela los cambios realizados en la fila actual o nueva de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, o el [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección de un [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto antes de llamar a la [actualización ](../../../ado/reference/ado-api/update-method.md) (método).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="recordset"></a>Conjunto de registros  
 Use la **CancelUpdate** método para cancelar los cambios realizados en la fila actual o descartar una fila recién agregada. No se puede cancelar los cambios en la fila actual o una fila nueva después de llamar a la **actualización** método, a menos que los cambios son parte de una transacción que puede revertir a la [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) método o parte de una actualización por lotes. En el caso de una actualización por lotes, puede cancelar la **actualizar** con el **CancelUpdate** o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) método.  
  
 Si va a agregar una nueva fila cuando se llama a la **CancelUpdate** método, la fila actual se convierte en la fila que era el actual antes de la [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) llamar.  
  
 Si se encuentra en modo de edición y desea abandonar el registro actual (por ejemplo, mediante la [mover](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md), o [cerrar](../../../ado/reference/ado-api/close-method-ado.md) métodos), puede usar  **CancelUpdate** para cancelarlos cambios pendientes. Debe hacer esto si la actualización no se puede enviar correctamente al origen de datos. Por ejemplo, un intento de eliminación que genera un error debido a infracciones de integridad referencial dejará el **Recordset** en modo de edición después de llamar a [eliminar](../../../ado/reference/ado-api/delete-method-ado-recordset.md).  
  
## <a name="record"></a>Grabar  
 El **CancelUpdate** método cancela todas las inserciones o eliminaciones de pendientes [campo](../../../ado/reference/ado-api/field-object.md) objetos y cancela las actualizaciones pendientes de los campos existentes y los restaura a sus valores originales. El [estado](../../../ado/reference/ado-api/status-property-ado-recordset.md) propiedad de todos los campos de la **campos** colección está establecida en **adFieldOK**.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Fields (colección) (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Vea también  
 [Actualización y ejemplo de los métodos CancelUpdate (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Actualización y ejemplo de los métodos CancelUpdate (VC ++)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew (método) (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Cancel (método) (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel (método) (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Propiedad EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Update (método)](../../../ado/reference/ado-api/update-method.md)
