---
title: "Propiedad sobrecargas eléctricas | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- EOS
- Stream::EOS
helpviewer_keywords:
- EOS property
ms.assetid: 57e08c5f-f3ed-4ecd-8c66-50b83b1031d1
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c29c72e9cd88ff5672b90aeab5da97c7742f5b30
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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

