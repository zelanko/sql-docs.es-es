---
title: SetEOS (método) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SetEOS
- _Stream::SetEOS
helpviewer_keywords:
- SetEOS method [ADO]
ms.assetid: 707c18ca-6a56-4970-bbd6-ae1fb86a0b8a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0db8c7972d6b647cdd021d43dbb3cdee1ba0452
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63314736"
---
# <a name="seteos-method"></a>SetEOS (método)
Establece la posición que es el final de la secuencia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>Comentarios  
 **SetEOS** actualiza el valor de la [EOS](../../../ado/reference/ado-api/eos-property.md) propiedad realizando actual [posición](../../../ado/reference/ado-api/position-property-ado.md) al final de la secuencia. Se truncan los bytes o caracteres que siguen a la posición actual.  
  
 Dado que [escribir](../../../ado/reference/ado-api/write-method.md), [WriteText](../../../ado/reference/ado-api/writetext-method.md), y [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) no se truncan los valores adicionales existente **Stream** objetos, se pueden truncar estos bytes o caracteres estableciendo la nueva posición final de secuencia con **SetEOS**.  
  
> [!CAUTION]
>  Si establece **EOS** a una posición antes del final de la secuencia real, perderá todos los datos después de la nueva **EOS** posición.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
