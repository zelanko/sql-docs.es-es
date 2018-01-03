---
title: "Propiedad sobrecargas eléctricas | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- EOS
- Stream::EOS
helpviewer_keywords: EOS property
ms.assetid: 57e08c5f-f3ed-4ecd-8c66-50b83b1031d1
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf26c00ecf445c9354d20fa5878942b56f2d2d19
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="eos-property"></a>Propiedad sobrecargas eléctricas
Indica si la actual posición está al final de la [flujo](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **booleano** valor que indica si la actual posición está al final de la secuencia. **Sobrecargas eléctricas** devuelve **True** si no hay ningún byte más en la secuencia; devuelve **False** si hay más bytes después de la posición actual.  
  
 Para establecer el final de la posición de la secuencia, utilice la [SetEOS](../../../ado/reference/ado-api/seteos-method.md) método. Para determinar la posición actual, utilice la [posición](../../../ado/reference/ado-api/position-property-ado.md) propiedad.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Sobrecargas eléctricas y en Propiedades de separador de línea de ejemplo del método SkipLine (VB)](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
