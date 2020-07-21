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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1b38b11917bf5d8a3248a6c9c0a64518109d7c83
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760191"
---
# <a name="cursorlocation-property-ado"></a>Propiedad CursorLocation (ADO)
Indica la ubicación del servicio de cursor.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor **Long** que se puede establecer en uno de los valores de [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) .  
  
## <a name="remarks"></a>Observaciones  
 Esta propiedad permite elegir entre varias bibliotecas de cursores accesibles para el proveedor. Normalmente, puede elegir entre usar una biblioteca de cursores del lado cliente o una que se encuentre en el servidor.  
  
 El valor de esta propiedad afecta a las conexiones establecidas solo después de que se haya establecido la propiedad. El cambio de la propiedad **CursorLocation** no tiene ningún efecto en las conexiones existentes.  
  
 Los cursores devueltos por el método [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) heredan esta configuración. Los objetos de **conjunto de registros** heredarán automáticamente esta configuración de las conexiones asociadas.  
  
 Esta propiedad es de lectura/escritura en una [conexión](../../../ado/reference/ado-api/connection-object-ado.md) o en un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)cerrado y de solo lectura en un conjunto de **registros**abierto.  
  
> [!NOTE]
>  **Uso del servicio de datos remotos** Cuando se usa en un objeto de **conjunto de registros** o de **conexión** del lado cliente, la propiedad **CursorLocation** solo se puede establecer en **adUseClient**.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Apéndice A: Proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)
