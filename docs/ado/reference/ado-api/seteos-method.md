---
description: SetEOS (método)
title: Seteos (método) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3ebf47bdae6a879a3afe699be36081eb136b700e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989136"
---
# <a name="seteos-method"></a>SetEOS (método)
Establece la posición que es el final de la secuencia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>Observaciones  
 **Seteoos** actualiza el valor de la propiedad [EOS](./eos-property.md) , haciendo que la [posición](./position-property-ado.md) actual sea el final de la secuencia. Se truncan los bytes o caracteres situados después de la posición actual.  
  
 Dado que [Write](./write-method.md), [WRITETEXT](./writetext-method.md)y [CopyTo](./copyto-method-ado.md) no truncan ningún valor adicional en los objetos de **secuencia** existentes, puede truncar estos caracteres o bytes estableciendo la nueva posición de final de secuencia con **seteos**.  
  
> [!CAUTION]
>  Si establece **EOS** en una posición antes del final real de la secuencia, perderá todos los datos después de la nueva posición de **EOS** .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](./stream-object-ado.md)