---
title: Propiedad Status (conjunto de registros ADO) | Documentos de Microsoft
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
- Recordset15::GetStatus
- Recordset15::Status
helpviewer_keywords:
- Status property [ADO Recordset]
ms.assetid: 41d70d89-880f-4850-9d17-19d9790cc8eb
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 819b8e0d1c1716fd630aefc1622d7c08dcc4da73
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282084"
---
# <a name="status-property-ado-recordset"></a>Propiedad Status (conjunto de registros ADO)
Indica el estado del registro actual con respecto a las actualizaciones por lotes u otras operaciones masivas.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve una suma de uno o varios [RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md) valores.  
  
## <a name="remarks"></a>Notas  
 Use la **estado** propiedad para ver los cambios pendientes para los registros modificados durante la actualización por lotes. También puede usar el **estado** propiedad para ver el estado de los registros que se producirá un error durante las operaciones masivas, como cuando se llama a la [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) métodos en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto o establecer el [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad en un **Recordset** objeto a una matriz de marcadores. Con esta propiedad, puede determinar cómo un registro dado error y resolverlo en consecuencia.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad Status (Recordset) (VB)](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [Ejemplo de la propiedad de estado (VC ++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
