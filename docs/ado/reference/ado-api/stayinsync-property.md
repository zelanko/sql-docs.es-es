---
description: Propiedad StayInSync
title: Propiedad StayInSync | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9677a776273e83ad31fecde3a7ea436138d3784e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988626"
---
# <a name="stayinsync-property"></a>Propiedad StayInSync
Indica, en un objeto de [conjunto de registros](./recordset-object-ado.md) jerárquico, si la referencia a los registros secundarios subyacentes (es decir, el *capítulo*) cambia cuando cambia la posición de la fila primaria.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor **booleano** . El valor predeterminado es **True**. Si **es true**, el capítulo se actualizará si el objeto de **conjunto de registros** primario cambia la posición de la fila; Si **es false**, el capítulo seguirá haciendo referencia a los datos del capítulo anterior, aunque el objeto de **conjunto de registros** primario haya cambiado la posición de la fila.  
  
## <a name="remarks"></a>Observaciones  
 Esta propiedad se aplica a los conjuntos de registros jerárquicos, como los que admite el [servicio de forma de datos de Microsoft para OLE DB](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md), y debe establecerse en el **conjunto de registros** primario antes de que se recupere el **conjunto de registros** secundario. Esta propiedad simplifica la navegación por los conjuntos de registros jerárquicos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de la propiedad StayInSync (VB)](./stayinsync-property-example-vb.md)   
 [Servicio de forma de datos de Microsoft para OLE DB (proveedor de servicios ADO)](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)