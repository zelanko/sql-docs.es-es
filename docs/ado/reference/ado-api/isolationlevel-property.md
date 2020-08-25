---
description: Propiedad IsolationLevel
title: Propiedad IsolationLevel | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::IsolationLevel
helpviewer_keywords:
- IsolationLevel property
ms.assetid: ea84e4b2-fbf2-4eef-b9ce-796b22e21800
author: rothja
ms.author: jroth
ms.openlocfilehash: f46199512521e6fe6fda6dc40fe894ba113c0229
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774724"
---
# <a name="isolationlevel-property"></a>Propiedad IsolationLevel
Indica el nivel de aislamiento para un objeto de [conexión](./connection-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de [IsolationLevelEnum](./isolationlevelenum.md) . El valor predeterminado es **adXactReadCommitted**.  
  
## <a name="remarks"></a>Observaciones  
 Utilice la propiedad **IsolationLevel** para establecer el nivel de aislamiento de un objeto de **conexión** . La configuración no surte efecto hasta la próxima vez que se llame al método [BeginTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) . Si el nivel de aislamiento solicitado no está disponible, el proveedor puede devolver el siguiente nivel mayor de aislamiento sin actualizar la propiedad **IsolationLevel** .  
  
 La propiedad **IsolationLevel** es de lectura y escritura.  
  
> [!NOTE]
>  **Uso del servicio de datos remotos** Cuando se usa en un objeto de **conexión** del lado cliente, la propiedad **IsolationLevel** solo se puede establecer en **adXactUnspecified**. Dado que los usuarios trabajan con objetos de **conjunto de registros** desconectados en una caché del lado cliente, puede haber problemas con los usuarios. Por ejemplo, cuando dos usuarios diferentes intentan actualizar el mismo registro, el servicio de datos remotos simplemente permite al usuario que actualiza el registro primero a "Win". Se producirá un error en la solicitud de actualización del segundo usuario.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades IsolationLevel y MODE (VB)](./isolationlevel-and-mode-properties-example-vb.md)   
 [Ejemplo de las propiedades IsolationLevel y MODE (VC + +)](./isolationlevel-and-mode-properties-example-vc.md)