---
title: Método SetEOS | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SetEOS
- _Stream::SetEOS
helpviewer_keywords:
- SetEOS method [ADO]
ms.assetid: 707c18ca-6a56-4970-bbd6-ae1fb86a0b8a
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3506ae0c62172461633df100c32bec73ea4af9f5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="seteos-method"></a>SetEOS (método)
Establece la posición que es el final de la secuencia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>Comentarios  
 **SetEOS** actualiza el valor de la [sobrecargas eléctricas](../../../ado/reference/ado-api/eos-property.md) propiedad realizando actual [posición](../../../ado/reference/ado-api/position-property-ado.md) el final de la secuencia. Se truncan los bytes o caracteres que siguen a la posición actual.  
  
 Dado que [escribir](../../../ado/reference/ado-api/write-method.md), [WriteText](../../../ado/reference/ado-api/writetext-method.md), y [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) no se truncan los valores adicionales existente **flujo** objetos, se pueden truncar estos bytes o caracteres estableciendo la nueva posición final de secuencia con **SetEOS**.  
  
> [!CAUTION]
>  Si establece **sobrecargas eléctricas** a una posición anterior al final real de la secuencia, se perderán todos los datos después de la nueva **sobrecargas eléctricas** posición.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
