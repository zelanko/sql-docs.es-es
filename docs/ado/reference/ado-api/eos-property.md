---
description: Propiedad EOS
title: Propiedad EOS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EOS
- Stream::EOS
helpviewer_keywords:
- EOS property
ms.assetid: 57e08c5f-f3ed-4ecd-8c66-50b83b1031d1
author: rothja
ms.author: jroth
ms.openlocfilehash: f7df00678197a4b9d16298e5f680263673fd10e8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973786"
---
# <a name="eos-property"></a>Propiedad EOS
Indica si la posición actual está al final de la [secuencia](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un valor **booleano** que indica si la posición actual está al final de la secuencia. **EOS** devuelve **true** si no hay más bytes en la secuencia; Devuelve **false** si hay más bytes después de la posición actual.  
  
 Para establecer el final de la posición de la secuencia, use el método [seteos](../../../ado/reference/ado-api/seteos-method.md) . Para determinar la posición actual, use la propiedad [Position](../../../ado/reference/ado-api/position-property-ado.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades EOS y LineSeparator y el método SkipLine (VB)](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
