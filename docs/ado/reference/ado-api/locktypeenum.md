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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9dbc6e9e78fc08be2bba08d0fbeb897496a2058b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66694933"
---
# <a name="locktypeenum"></a>LockTypeEnum
Especifica el tipo de bloqueo colocado en registros durante la edición.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|Indica las actualizaciones por lotes optimista. Se requiere para el modo de actualización por lotes.|  
|**adLockOptimistic**|3|Indica un bloqueo optimista, registro por registro. El proveedor utiliza el bloqueo optimista bloquear registros solo cuando se llama a la [actualización](../../../ado/reference/ado-api/update-method.md) método.|  
|**adLockPessimistic**|2|Indica un bloqueo pesimista, registro por registro. El proveedor no lo que es necesario para garantizar la modificación correcta de los registros, normalmente mediante el bloqueo de registros en el origen de datos inmediatamente después de editar.|  
|**adLockReadOnly**|1|Indica los registros de solo lectura. No se puede modificar los datos.|  
|**adLockUnspecified**|-1|No especifica un tipo de bloqueo. Para clones, el clon se crea con el mismo tipo de bloqueo que el original.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.LockType.BATCHOPTIMISTIC|  
|AdoEnums.LockType.OPTIMISTIC|  
|AdoEnums.LockType.PESSIMISTIC|  
|AdoEnums.LockType.READONLY|  
|AdoEnums.LockType.UNSPECIFIED|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Clone (método) (ADO)](../../../ado/reference/ado-api/clone-method-ado.md)|[Propiedad LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)|  
|[Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Evento WillExecute (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|
