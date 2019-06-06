---
title: Propiedad CursorLocation (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::CursorLocation
- Recordset15::CursorLocation
helpviewer_keywords:
- CursorLocation property [ADO]
ms.assetid: 39c8d86e-7ee9-4182-be5e-aad5ce952f84
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 344956b349e51a448a768988ff5062bfbc532562
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698428"
---
# <a name="cursorlocation-property-ado"></a>Propiedad CursorLocation (ADO)
Indica la ubicación del servicio de cursor.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **largo** valor que se puede establecer en uno de los [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) valores.  
  
## <a name="remarks"></a>Comentarios  
 Esta propiedad le permite elegir entre varias bibliotecas de cursores accesibles para el proveedor. Por lo general, puede elegir entre usar una biblioteca de cursores del lado cliente o uno que se encuentra en el servidor.  
  
 Valor de esta propiedad afecta a las conexiones establecidas solo después de haber establecido la propiedad. Cambiar el **CursorLocation** propiedad no tiene ningún efecto en las conexiones existentes.  
  
 Los cursores devueltos por la [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método heredarán este ajuste. **Conjunto de registros** objetos heredará automáticamente esta configuración de sus conexiones asociadas.  
  
 Esta propiedad es de lectura/escritura en un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) o un cerrado [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)y de solo lectura en una página abierta **Recordset**.  
  
> [!NOTE]
>  **Uso del servicio de datos remoto** cuando se usa en un cliente **Recordset** o **conexión** objeto, el **CursorLocation** propiedad solo puede establecerse en **adUseClient**.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Vea también  
 [Apéndice A: proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)
