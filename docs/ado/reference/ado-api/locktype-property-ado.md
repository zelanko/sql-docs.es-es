---
title: Propiedad LockType (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::LockType
helpviewer_keywords:
- LockType property [ADO]
ms.assetid: 9920c14e-033a-4de1-8149-0ce9737a3246
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 662b3be9eafac4687708be8a854da7f5d8701af9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="locktype-property-ado"></a>Propiedad LockType (ADO)
Indica el tipo de bloqueos colocados en registros durante la edición.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) valor. El valor predeterminado es **adLockReadOnly**.  
  
## <a name="remarks"></a>Comentarios  
 Establecer el **LockType** propiedad antes de abrir un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) para especificar el tipo de bloqueo que el proveedor debe usar al abrirlo. Lea la propiedad para devolver el tipo de bloqueo en uso en un formato de archivo **Recordset** objeto.  
  
 Proveedores pueden no admitir todos los tipos de bloqueo. Si un proveedor no admite solicitado **LockType** establecer, sustituirá por otro tipo de bloqueo. Para determinar la funcionalidad de bloqueo real disponible en un **Recordset** objeto, utilice la [admite](../../../ado/reference/ado-api/supports-method.md) método con **adUpdate** y **adUpdateBatch**.  
  
 El **adLockPessimistic** configuración no se admite si el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad está establecida en **adUseClient**. Si se establece un valor no admitido, no se producirá ningún error; admite la más parecida **LockType** se utilizará en su lugar.  
  
 El **LockType** propiedad es de lectura y escritura cuando el **Recordset** está cerrado y de solo lectura cuando se abre.  
  
> [!NOTE]
>  **Uso de servicios de datos remoto** cuando se utiliza en un lado del cliente **Recordset** objeto, el **LockType** propiedad solo puede establecerse en **adLockBatchOptimistic**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [CursorType, LockType y ejemplo de las propiedades EditMode (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType y ejemplo de las propiedades EditMode (VC ++)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
