---
title: "Método SkipLine | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::raw_SkipLine
- _Stream::SkipLine
helpviewer_keywords:
- Skipline method [ADO]
ms.assetid: 0abc00fe-ee09-4c8e-b1f2-48ee9c5f3329
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f959ab3e83b91f8c8d8529e44c48a4cbe370882
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="skipline-method"></a>Método SkipLine
Omite una línea completa al leer un texto [flujo](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>Comentarios  
 Se omiten todos los caracteres hasta el siguiente separador de línea. De forma predeterminada, el [separador de línea](../../../ado/reference/ado-api/lineseparator-property-ado.md) es **adCRLF**. Si intenta omitir [sobrecargas eléctricas](../../../ado/reference/ado-api/eos-property.md), la posición actual se mantendrá en **sobrecargas eléctricas**.  
  
 El **SkipLine** método se utiliza con secuencias de texto ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
