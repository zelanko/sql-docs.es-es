---
title: Seteos (método) | Microsoft Docs
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
ms.openlocfilehash: 357778765f0c7ac59d924518340ca34226853fc0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67916922"
---
# <a name="seteos-method"></a>SetEOS (método)
Establece la posición que es el final de la secuencia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>Observaciones  
 **Seteoos** actualiza el valor de la propiedad [EOS](../../../ado/reference/ado-api/eos-property.md) , haciendo que la [posición](../../../ado/reference/ado-api/position-property-ado.md) actual sea el final de la secuencia. Se truncan los bytes o caracteres situados después de la posición actual.  
  
 Dado que [Write](../../../ado/reference/ado-api/write-method.md), [WRITETEXT](../../../ado/reference/ado-api/writetext-method.md)y [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) no truncan ningún valor adicional en los objetos de **secuencia** existentes, puede truncar estos caracteres o bytes estableciendo la nueva posición de final de secuencia con **seteos**.  
  
> [!CAUTION]
>  Si establece **EOS** en una posición antes del final real de la secuencia, perderá todos los datos después de la nueva posición de **EOS** .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
