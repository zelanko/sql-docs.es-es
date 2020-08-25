---
description: StreamReadEnum
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
ms.openlocfilehash: c0a0e8d93742574e9a2975b99d15c18500684e60
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777184"
---
# <a name="streamreadenum"></a>StreamReadEnum
Especifica si se debe leer toda la secuencia o la línea siguiente de un objeto de [secuencia](./stream-object-ado.md) .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|Predeterminada. Lee todos los bytes del flujo, desde la posición actual hacia el marcador de [EOS](./eos-property.md) . Este es el único valor de **StreamReadEnum** válido con secuencias binarias (el[tipo](./type-property-ado-stream.md) es **adTypeBinary**).|  
|**adReadLine**|-2|Lee la línea siguiente de la secuencia (designada por la propiedad [LineSeparator](./lineseparator-property-ado.md) ).|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Estas constantes no tienen equivalentes de ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  

:::row:::
    :::column:::
        [Método Read](./read-method.md)  
    :::column-end:::
    :::column:::
        [Método ReadText](./readtext-method.md)  
    :::column-end:::
:::row-end:::