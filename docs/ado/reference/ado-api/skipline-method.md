---
description: Método SkipLine
title: Método SkipLine | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SkipLine
- _Stream::SkipLine
helpviewer_keywords:
- Skipline method [ADO]
ms.assetid: 0abc00fe-ee09-4c8e-b1f2-48ee9c5f3329
author: rothja
ms.author: jroth
ms.openlocfilehash: 463de3740ce29b859732c5ddb7ba69d58069f93f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442107"
---
# <a name="skipline-method"></a>Método SkipLine
Omite una línea completa cuando se lee una [secuencia](../../../ado/reference/ado-api/stream-object-ado.md)de texto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>Observaciones  
 Se omiten todos los caracteres hasta el separador de línea siguiente, incluido. De forma predeterminada, el valor de [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) es **adCRLF**. Si intenta omitir más allá de [EOS](../../../ado/reference/ado-api/eos-property.md), la posición actual permanecerá en **EOS**.  
  
 El método **SkipLine** se usa con secuencias de texto (el[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
