---
title: "Método WriteText | Documentos de Microsoft"
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
- _Stream::raw_WriteText
- _Stream::WriteText
helpviewer_keywords:
- WriteText method [ADO]
ms.assetid: 7a669048-13f4-4574-a2b1-985e089729d5
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d7facdd886b6bf048afb9f17a6d9c7c0a69ced57
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
  
## <a name="remarks"></a>Comentarios  
 Cadenas especificadas se escriben en el **flujo** objeto sin los espacios ni caracteres entre cada cadena.  
  
 Actual [posición](../../../ado/reference/ado-api/position-property-ado.md) se establece en el carácter que sigue a los datos escritos. El **WriteText** método no trunca el resto de los datos en una secuencia. Si desea truncar estos caracteres, llame a [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 Si escribe más allá de la actual [sobrecargas eléctricas](../../../ado/reference/ado-api/eos-property.md) posición, el [tamaño](../../../ado/reference/ado-api/size-property-ado-stream.md) de la **flujo** se incrementará para contener los caracteres nuevos, y **sobrecargas eléctricas** se moverá hasta el último byte nuevo en el **flujo**.  
  
> [!NOTE]
>  El **WriteText** método se utiliza con secuencias de texto ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**). Para secuencias binarias (**tipo** es **adTypeBinary**), utilice [escribir](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método Write](../../../ado/reference/ado-api/write-method.md)

