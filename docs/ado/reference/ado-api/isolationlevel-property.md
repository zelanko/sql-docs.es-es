---
title: Propiedad IsolationLevel | Documentos de Microsoft
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
- Connection15::IsolationLevel
helpviewer_keywords:
- IsolationLevel property
ms.assetid: ea84e4b2-fbf2-4eef-b9ce-796b22e21800
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 326f145da9c2e80b7f4765a0c4bae1a657f4ee25
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="isolationlevel-property"></a>Propiedad IsolationLevel
Indica el nivel de aislamiento para una [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md) valor. El valor predeterminado es **adXactReadCommitted**.  
  
## <a name="remarks"></a>Comentarios  
 Use la **IsolationLevel** propiedad para establecer el aislamiento de nivel de un **conexión** objeto. El valor no surtirá efecto hasta la próxima vez que se llama a la [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) método. Si el nivel de aislamiento solicitado no está disponible, el proveedor puede devolver el siguiente nivel superior de aislamiento sin actualizar la **IsolationLevel** propiedad.  
  
 El **IsolationLevel** propiedad es de lectura/escritura.  
  
> [!NOTE]
>  **Uso de servicios de datos remoto** cuando se utiliza en un lado del cliente **conexión** objeto, el **IsolationLevel** propiedad se puede establecer solo en **adXactUnspecified**. Dado que los usuarios están trabajando con desconectada **Recordset** objetos en una caché de cliente, puede haber problemas de multiusuario. Por ejemplo, cuando dos usuarios distintos intentan actualizar el mismo registro, servicio de datos remoto simplemente permite al usuario que actualice primero el registro "win". La segunda solicitud del usuario actualización se producirá un error.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo IsolationLevel y Mode propiedades (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [Ejemplo IsolationLevel y Mode propiedades (VC ++)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
