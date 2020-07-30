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
author: rothja
ms.author: jroth
ms.openlocfilehash: 92c599665548c36b8349290b02d197393f707fbf
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243196"
---
# <a name="streamreadenum"></a>StreamReadEnum
Especifica si se debe leer toda la secuencia o la línea siguiente de un objeto de [secuencia](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|Predeterminada. Lee todos los bytes del flujo, desde la posición actual hacia el marcador de [EOS](../../../ado/reference/ado-api/eos-property.md) . Este es el único valor de **StreamReadEnum** válido con secuencias binarias (el[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeBinary**).|  
|**adReadLine**|-2|Lee la línea siguiente de la secuencia (designada por la propiedad [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) ).|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Estas constantes no tienen equivalentes de ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  

:::row:::
    :::column:::
        [Read (método)](../../../ado/reference/ado-api/read-method.md)  
    :::column-end:::
    :::column:::
        [Método ReadText](../../../ado/reference/ado-api/readtext-method.md)  
    :::column-end:::
:::row-end:::
