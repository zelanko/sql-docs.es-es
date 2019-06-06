---
title: Propiedad LockType (ADO) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: a53c6e6e0164b404fdd5b106bae83137d56f319e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697636"
---
# <a name="locktype-property-ado"></a>Propiedad LockType (ADO)
Indica el tipo de los bloqueos colocados en registros durante la edición.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) valor. El valor predeterminado es **adLockReadOnly**.  
  
## <a name="remarks"></a>Comentarios  
 Establecer el **LockType** propiedad antes de abrir un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) para especificar qué tipo de bloqueo que el proveedor debe usar al abrirlo. Leer la propiedad para devolver el tipo de bloqueo en uso en una página abierta **Recordset** objeto.  
  
 Los proveedores pueden no admitir todos los tipos de bloqueo. Si un proveedor no admite solicitado **LockType** establecer, sustituirá por otro tipo de bloqueo. Para determinar la funcionalidad de bloqueo real disponible en un **Recordset** de objeto, utilice el [admite](../../../ado/reference/ado-api/supports-method.md) método con **adUpdate** y **adUpdateBatch**.  
  
 El **adLockPessimistic** configuración no se admite si el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad está establecida en **adUseClient**. Si se establece un valor no admitido, se producirá ningún error; admite la más cercana **LockType** se usará en su lugar.  
  
 El **LockType** propiedad es de lectura/escritura cuando el **Recordset** está cerrado y de solo lectura cuando se abre.  
  
> [!NOTE]
>  **Uso del servicio de datos remoto** cuando se usa en un cliente **Recordset** objeto, el **LockType** propiedad solo puede establecerse en **adLockBatchOptimistic**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [CursorType, LockType y ejemplo de las propiedades EditMode (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType y ejemplo de las propiedades EditMode (VC ++)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
