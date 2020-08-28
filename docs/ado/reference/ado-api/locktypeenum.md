---
description: LockTypeEnum
title: LockTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 26cbe4b13e855949b617804311bd283cf44f2ef3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990686"
---
# <a name="locktypeenum"></a>LockTypeEnum
Especifica el tipo de bloqueo colocado en los registros durante la edición.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|Indica actualizaciones de Batch optimistas. Necesario para el modo de actualización por lotes.|  
|**adLockOptimistic**|3|Indica bloqueo optimista, registro por registro. El proveedor utiliza el bloqueo optimista y bloquea los registros solo cuando se llama al método [Update](./update-method.md) .|  
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
        [Clone (método) (ADO)](./clone-method-ado.md)  
        [Propiedad LockType (ADO)](./locktype-property-ado.md)  
    :::column-end:::
    :::column:::
        [Open (método) (conjunto de registros ADO)](./open-method-ado-recordset.md)  
        [Evento WillExecute (ADO)](./willexecute-event-ado.md)  
    :::column-end:::
:::row-end:::