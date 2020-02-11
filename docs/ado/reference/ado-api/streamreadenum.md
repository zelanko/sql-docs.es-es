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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928663"
---
# <a name="streamreadenum"></a>StreamReadEnum
Especifica si se debe leer toda la secuencia o la línea siguiente de un objeto de [secuencia](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|Default. Lee todos los bytes del flujo, desde la posición actual hacia el marcador de [EOS](../../../ado/reference/ado-api/eos-property.md) . Este es el único valor de **StreamReadEnum** válido con secuencias binarias (el[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeBinary**).|  
|**adReadLine**|-2|Lee la línea siguiente de la secuencia (designada por la propiedad [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) ).|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Estas constantes no tienen equivalentes de ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Método Read](../../../ado/reference/ado-api/read-method.md)|[Método ReadText](../../../ado/reference/ado-api/readtext-method.md)|
