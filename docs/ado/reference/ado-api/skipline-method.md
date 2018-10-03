---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0e96900fdac55e97e3481ba5198e0f51d659877
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713763"
---
# <a name="skipline-method"></a>Método SkipLine
Omite una línea completa al leer un texto [Stream](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>Comentarios  
 Se omiten todos los caracteres hasta e incluyendo el separador de la línea siguiente. De forma predeterminada, el [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) es **adCRLF**. Si intenta omitir [EOS](../../../ado/reference/ado-api/eos-property.md), la posición actual se mantendrá en **EOS**.  
  
 El **SkipLine** método se utiliza con secuencias de texto ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
