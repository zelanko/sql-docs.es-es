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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc360bc91e977228a6f9139089a7bfa87d912e1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918438"
---
# <a name="isolationlevel-property"></a>Propiedad IsolationLevel
Indica el nivel de aislamiento para un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md) valor. El valor predeterminado es **adXactReadCommitted**.  
  
## <a name="remarks"></a>Comentarios  
 Use la **IsolationLevel** para establecer el nivel de aislamiento de la propiedad de un **conexión** objeto. La configuración no surte efecto hasta la próxima vez que se llama a la [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) método. Si el nivel de aislamiento solicitado no está disponible, el proveedor puede devolver el siguiente nivel superior de aislamiento sin actualizar el **IsolationLevel** propiedad.  
  
 El **IsolationLevel** propiedad es de lectura/escritura.  
  
> [!NOTE]
>  **Uso del servicio de datos remoto** cuando se usa en un cliente **conexión** objeto, el **IsolationLevel** propiedad se puede establecer solo en **adXactUnspecified**. Dado que los usuarios están trabajando sin conexión **Recordset** objetos en una memoria caché del lado cliente, puede haber problemas de multiusuario. Por ejemplo, cuando dos usuarios distintos intentan actualizar el mismo registro, servicio de datos remotos simplemente permite al usuario que actualice primero el registro "win". Solicitud de actualización del segundo usuario producirá un error.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo IsolationLevel y Mode propiedades (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [Ejemplo IsolationLevel y Mode propiedades (VC ++)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
