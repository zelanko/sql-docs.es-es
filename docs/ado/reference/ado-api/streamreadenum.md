---
title: StreamReadEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6bd88a62a46bae523904b308d011ebe956e02497
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="streamreadenum"></a>StreamReadEnum
Especifica si se debe leer toda la secuencia o la línea siguiente de un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|Predeterminado: Lee todos los bytes de la secuencia, desde la posición actual en adelante el [sobrecargas eléctricas](../../../ado/reference/ado-api/eos-property.md) marcador. Este es el único valor válido **StreamReadEnum** valor con secuencias binarias ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeBinary**).|  
|**adReadLine**|-2|Lee la siguiente línea de la secuencia (designado por el [separador de línea](../../../ado/reference/ado-api/lineseparator-property-ado.md) propiedad).|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Método Read](../../../ado/reference/ado-api/read-method.md)|[Método ReadText](../../../ado/reference/ado-api/readtext-method.md)|
