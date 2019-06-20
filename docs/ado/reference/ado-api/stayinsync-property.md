---
title: La propiedad StayInSync | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 98a0cc1df12f905cd0d22d05b162983742d0f355
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710789"
---
# <a name="stayinsync-property"></a>Propiedad StayInSync
Indica, en jerárquica [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, si la referencia a los registros secundarios subyacentes (es decir, el *capítulo*) los cambios cuando los cambios de posición de la fila primaria.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **booleano** valor. El valor predeterminado es **True**. Si **True**, el capítulo se actualizará si el elemento primario **Recordset** posición; de la fila de cambios en el objeto si **False**, el capítulo seguirá haciendo referencia a los datos en el capítulo anterior Aunque el elemento primario **Recordset** objeto ha cambiado la posición de fila.  
  
## <a name="remarks"></a>Comentarios  
 Esta propiedad se aplica a conjuntos de registros jerárquicos, como los admitidos por el [servicio de forma de datos de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)y debe establecerse en el elemento primario **Recordset** antes del elemento secundario  **Conjunto de registros** se recupera. Esta propiedad simplifica el desplazamiento por conjuntos de registros jerárquicos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad StayInSync (VB)](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [Servicio de OLE DB (proveedor de servicios de ADO) de la forma de datos de Microsoft](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
