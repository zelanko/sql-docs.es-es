---
title: LockType (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::LockType
helpviewer_keywords:
- LockType property [ADO]
ms.assetid: 9920c14e-033a-4de1-8149-0ce9737a3246
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7b50ab4a6fa31ec74371b86129f30abf11a1ba6c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932255"
---
# <a name="locktype-property-ado"></a>Propiedad LockType (ADO)
Indica el tipo de bloqueos colocados en los registros durante la edición.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) . El valor predeterminado es **adLockReadOnly**.  
  
## <a name="remarks"></a>Observaciones  
 Establezca la propiedad **LockType** antes de abrir un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) para especificar el tipo de bloqueo que debe utilizar el proveedor al abrirlo. Lea la propiedad para devolver el tipo de bloqueo en uso en un objeto de **conjunto de registros** abierto.  
  
 Es posible que los proveedores no admitan todos los tipos de bloqueo. Si un proveedor no admite la configuración de **LockType** solicitada, reemplazará a otro tipo de bloqueo. Para determinar la funcionalidad de bloqueo real disponible en un objeto de **conjunto de registros** , use el método [Supports](../../../ado/reference/ado-api/supports-method.md) con **adUpdate** y **adUpdateBatch**.  
  
 El valor **adLockPessimistic** no se admite si la propiedad [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) está establecida en **adUseClient**. Si se establece un valor no compatible, no se producirá ningún error. en su lugar, se utilizará el **LockType** compatible más cercano.  
  
 La propiedad **LockType** es de lectura y escritura cuando el **conjunto de registros** está cerrado y es de solo lectura cuando está abierto.  
  
> [!NOTE]
>  **Uso del servicio de datos remotos** Cuando se usa en un objeto de **conjunto de registros** del lado cliente, la propiedad **LockType** solo se puede establecer en **adLockBatchOptimistic**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades CursorType, LockType y EditMode (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [Ejemplo de las propiedades CursorType, LockType y EditMode (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [CancelBatch (método) (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
