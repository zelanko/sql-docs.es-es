---
description: Propiedad LockType (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b9211ec3b9c6213ffab8cfc07c8bcf89559240ae
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774584"
---
# <a name="locktype-property-ado"></a>Propiedad LockType (ADO)
Indica el tipo de bloqueos colocados en los registros durante la edición.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de [LockTypeEnum](./locktypeenum.md) . El valor predeterminado es **adLockReadOnly**.  
  
## <a name="remarks"></a>Observaciones  
 Establezca la propiedad **LockType** antes de abrir un [conjunto de registros](./recordset-object-ado.md) para especificar el tipo de bloqueo que debe utilizar el proveedor al abrirlo. Lea la propiedad para devolver el tipo de bloqueo en uso en un objeto de **conjunto de registros** abierto.  
  
 Es posible que los proveedores no admitan todos los tipos de bloqueo. Si un proveedor no admite la configuración de **LockType** solicitada, reemplazará a otro tipo de bloqueo. Para determinar la funcionalidad de bloqueo real disponible en un objeto de **conjunto de registros** , use el método [Supports](./supports-method.md) con **adUpdate** y **adUpdateBatch**.  
  
 El valor **adLockPessimistic** no se admite si la propiedad [CursorLocation](./cursorlocation-property-ado.md) está establecida en **adUseClient**. Si se establece un valor no compatible, no se producirá ningún error. en su lugar, se utilizará el **LockType** compatible más cercano.  
  
 La propiedad **LockType** es de lectura y escritura cuando el **conjunto de registros** está cerrado y es de solo lectura cuando está abierto.  
  
> [!NOTE]
>  **Uso del servicio de datos remotos** Cuando se usa en un objeto de **conjunto de registros** del lado cliente, la propiedad **LockType** solo se puede establecer en **adLockBatchOptimistic**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades CursorType, LockType y EditMode (VB)](./cursortype-locktype-and-editmode-properties-example-vb.md)   
 [Ejemplo de las propiedades CursorType, LockType y EditMode (VC + +)](./cursortype-locktype-and-editmode-properties-example-vc.md)   
 [CancelBatch (método) (ADO)](./cancelbatch-method-ado.md)   
 [Método UpdateBatch](./updatebatch-method.md)