---
title: Propiedad StayInSync | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::StayInSync
- Recordset20::put_StayInSync
- Recordset20::PutStayInSync
- Recordset20::get_StayInSync
- Recordset20::GetStayInSync
helpviewer_keywords:
- StayInSync property
ms.assetid: 502d69b5-dc9a-455d-b115-a03bd39a552b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ccd1cf14eddb9fb0b7b440defb0eb700b2fb354
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282504"
---
# <a name="stayinsync-property"></a>Propiedad StayInSync
Indica, en jerárquica [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, si la referencia a los registros secundarios subyacentes (es decir, el *capítulo*) cambios cuando los cambios de posición de la fila primaria.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **booleano** valor. El valor predeterminado es **True**. Si **True**, el capítulo se actualizará si el elemento primario **Recordset** posición; de la fila de cambios en el objeto si **False**, continuará el capítulo hacer referencia a los datos en el capítulo anterior Aunque el elemento primario **Recordset** objeto ha cambiado la posición de la fila.  
  
## <a name="remarks"></a>Notas  
 Esta propiedad se aplica a los conjuntos de registros jerárquicos, como los admitidos por la [servicio de forma de datos de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)y debe establecerse en el registro primario **Recordset** antes del elemento secundario  **Conjunto de registros** se recupera. Esta propiedad simplifica el desplazamiento por conjuntos de registros jerárquicos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad StayInSync (VB)](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [Datos de Microsoft para dar forma al servicio para OLE DB (proveedor de servicios ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
