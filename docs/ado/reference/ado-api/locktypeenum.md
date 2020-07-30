---
title: LockTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- LockTypeEnum
helpviewer_keywords:
- LockTypeEnum enumeration [ADO]
ms.assetid: d2894eaf-4450-4ace-aa51-c8b875fd3010
author: rothja
ms.author: jroth
ms.openlocfilehash: e609a51d6b9f42cb6101ff485633302193757fbd
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242655"
---
# <a name="locktypeenum"></a>LockTypeEnum
Especifica el tipo de bloqueo colocado en los registros durante la edición.  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|Indica actualizaciones de Batch optimistas. Necesario para el modo de actualización por lotes.|  
|**adLockOptimistic**|3|Indica bloqueo optimista, registro por registro. El proveedor utiliza el bloqueo optimista y bloquea los registros solo cuando se llama al método [Update](../../../ado/reference/ado-api/update-method.md) .|  
|**adLockPessimistic**|2|Indica un bloqueo pesimista, registro por registro. El proveedor hace lo necesario para garantizar la correcta edición de los registros, normalmente mediante el bloqueo de registros en el origen de datos inmediatamente después de la edición.|  
|**adLockReadOnly**|1|Indica los registros de solo lectura. No se pueden modificar los datos.|  
|**adLockUnspecified**|-1|No especifica un tipo de bloqueo. En el caso de los clones, el clon se crea con el mismo tipo de bloqueo que el original.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.LockType.BATCHOPTIMISTIC|  
|AdoEnums. LockType. OPTIMISTic|  
|AdoEnums. LockType. PESIMISTA|  
|AdoEnums. LockType. READONLY|  
|AdoEnums. LockType. no especificado|  
  
## <a name="applies-to"></a>Se aplica a  

:::row:::
    :::column:::
        [Clone (método) (ADO)](../../../ado/reference/ado-api/clone-method-ado.md)  
        [Propiedad LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)  
    :::column-end:::
    :::column:::
        [Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)  
        [Evento WillExecute (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)  
    :::column-end:::
:::row-end:::
