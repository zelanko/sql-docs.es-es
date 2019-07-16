---
title: StreamReadEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7700fc1ddc3cc619db224ac46006370898af1d62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928663"
---
# <a name="streamreadenum"></a>StreamReadEnum
Especifica si se debe leer toda la secuencia o la línea siguiente de un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|Predeterminado: Lee todos los bytes de la secuencia, desde la posición actual y versiones posteriores a la [EOS](../../../ado/reference/ado-api/eos-property.md) marcador. Este es el único valor válido **StreamReadEnum** valor con secuencias binarias ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeBinary**).|  
|**adReadLine**|-2|Lee la línea siguiente de la secuencia (designado por el [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) propiedad).|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Estas constantes no tienen equivalentes de ADO y WFC.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Método Read](../../../ado/reference/ado-api/read-method.md)|[Método ReadText](../../../ado/reference/ado-api/readtext-method.md)|
