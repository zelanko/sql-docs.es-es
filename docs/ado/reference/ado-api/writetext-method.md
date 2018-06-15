---
title: Método WriteText | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_WriteText
- _Stream::WriteText
helpviewer_keywords:
- WriteText method [ADO]
ms.assetid: 7a669048-13f4-4574-a2b1-985e089729d5
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c38b1e8573e59d4446ff0a4dbfebf1cc627b3863
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35283194"
---
# <a name="writetext-method"></a>Método WriteText
Escribe una cadena de texto especificado en un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Datos*  
 A **cadena** valor que contiene el texto en caracteres que se va a escribir.  
  
 *Opciones*  
 Opcional. A [StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md) valor que especifica si se debe escribir un carácter separador de línea al final de la cadena especificada.  
  
## <a name="remarks"></a>Notas  
 Cadenas especificadas se escriben en el **flujo** objeto sin los espacios ni caracteres entre cada cadena.  
  
 Actual [posición](../../../ado/reference/ado-api/position-property-ado.md) se establece en el carácter que sigue a los datos escritos. El **WriteText** método no trunca el resto de los datos en una secuencia. Si desea truncar estos caracteres, llame a [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 Si escribe más allá de la actual [sobrecargas eléctricas](../../../ado/reference/ado-api/eos-property.md) posición, el [tamaño](../../../ado/reference/ado-api/size-property-ado-stream.md) de la **flujo** se incrementará para contener los caracteres nuevos, y **sobrecargas eléctricas** se moverá hasta el último byte nuevo en el **flujo**.  
  
> [!NOTE]
>  El **WriteText** método se utiliza con secuencias de texto ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**). Para secuencias binarias (**tipo** es **adTypeBinary**), utilice [escribir](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método Write](../../../ado/reference/ado-api/write-method.md)
