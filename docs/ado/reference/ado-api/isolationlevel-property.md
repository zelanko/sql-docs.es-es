---
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
ms.openlocfilehash: ea8d538dbd5c4c06cb770a983a2733bb2f27e6b2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758661"
---
# <a name="isolationlevel-property"></a>Propiedad IsolationLevel
Indica el nivel de aislamiento para un objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de [IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md) . El valor predeterminado es **adXactReadCommitted**.  
  
## <a name="remarks"></a>Comentarios  
 Utilice la propiedad **IsolationLevel** para establecer el nivel de aislamiento de un objeto de **conexión** . La configuración no surte efecto hasta la próxima vez que se llame al método [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) . Si el nivel de aislamiento solicitado no está disponible, el proveedor puede devolver el siguiente nivel mayor de aislamiento sin actualizar la propiedad **IsolationLevel** .  
  
 La propiedad **IsolationLevel** es de lectura y escritura.  
  
> [!NOTE]
>  **Uso del servicio de datos remotos** Cuando se usa en un objeto de **conexión** del lado cliente, la propiedad **IsolationLevel** solo se puede establecer en **adXactUnspecified**. Dado que los usuarios trabajan con objetos de **conjunto de registros** desconectados en una caché del lado cliente, puede haber problemas con los usuarios. Por ejemplo, cuando dos usuarios diferentes intentan actualizar el mismo registro, el servicio de datos remotos simplemente permite al usuario que actualiza el registro primero a "Win". Se producirá un error en la solicitud de actualización del segundo usuario.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades IsolationLevel y MODE (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [Ejemplo de las propiedades IsolationLevel y MODE (VC + +)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
