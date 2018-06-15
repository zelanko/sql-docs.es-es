---
title: StreamReadEnum | Documentos de Microsoft
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
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6dca9f57838f938e225790e164870b1bec834bd3
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282534"
---
# <a name="streamreadenum"></a>StreamReadEnum
Especifica si se debe leer toda la secuencia o la línea siguiente de un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|Predeterminado: Lee todos los bytes de la secuencia, desde la posición actual en adelante el [sobrecargas eléctricas](../../../ado/reference/ado-api/eos-property.md) marcador. Este es el único valor válido **StreamReadEnum** valor con secuencias binarias ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeBinary**).|  
|**adReadLine**|-2|Lee la siguiente línea de la secuencia (designado por el [separador de línea](../../../ado/reference/ado-api/lineseparator-property-ado.md) propiedad).|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Método Read](../../../ado/reference/ado-api/read-method.md)|[Método ReadText](../../../ado/reference/ado-api/readtext-method.md)|
