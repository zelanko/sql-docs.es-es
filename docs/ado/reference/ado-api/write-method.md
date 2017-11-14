---
title: "Método Write | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- _Stream::raw_Write
- _Stream::Write
helpviewer_keywords:
- Write method [ADO]
ms.assetid: 02982e6a-ac5f-4af2-b82e-ce12534b84b2
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6adf96fa3fd1135727a55a8c7e26351942f886c4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="write-method"></a>Método Write
Escribe datos binarios en un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Búfer*  
 A **Variant** que contiene una matriz de bytes que se escribirán.  
  
## <a name="remarks"></a>Comentarios  
 Los bytes especificados se escriben en el **flujo** objeto sin ningún espacio intermedio entre cada byte.  
  
 Actual [posición](../../../ado/reference/ado-api/position-property-ado.md) está establecido en el byte situado después de los datos escritos. El **escribir** método no trunca el resto de los datos en una secuencia. Si desea truncar estos bytes, llame a [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 Si escribe más allá de la actual [sobrecargas eléctricas](../../../ado/reference/ado-api/eos-property.md) posición, el [tamaño](../../../ado/reference/ado-api/size-property-ado-stream.md) de la **flujo** se incrementará para contener los bytes nuevos, y **sobrecargas eléctricas** moverá hasta el último byte nuevo en el **flujo**.  
  
> [!NOTE]
>  El **escribir** método se utiliza con secuencias binarias ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeBinary**). Para las secuencias de texto (**tipo** es **adTypeText**), utilice [WriteText](../../../ado/reference/ado-api/writetext-method.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)

