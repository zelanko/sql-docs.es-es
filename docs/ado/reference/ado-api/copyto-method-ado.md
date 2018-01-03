---
title: "CopyTo (método) (ADO) | Documentos de Microsoft"
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
- _Stream::raw_CopyTo
- _Stream::CopyTo
helpviewer_keywords: CopyTo method [ADO]
ms.assetid: b4aa5714-916b-48b8-8b09-cc2708379602
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9c59a27806939557b170ae8fc7d3f842afd21f83
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="copyto-method-ado"></a>CopyTo (método) (ADO)
Copia el número especificado de caracteres o bytes (en función de [tipo](../../../ado/reference/ado-api/type-property-ado-stream.md)) en el [flujo](../../../ado/reference/ado-api/stream-object-ado.md) a otro **flujo** objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DestStream*  
 Un valor de variable de objeto que contiene una referencia a un formato de archivo **flujo** objeto. Actual **flujo** se copia en el destino **flujo** especificado por *DestStream*. El destino **flujo** ya debe estar abierto. Si no es así, se produce un error en tiempo de ejecución.  
  
> [!NOTE]
>  El *DestStream* parámetro no puede ser un servidor proxy de **flujo** objeto porque esto requiere acceso a una interfaz privada en el **flujo** objetos que no se pueden enviar de forma remota a la cliente.  
  
 *NumChars*  
 Opcional. Un **entero** valor que especifica el número de bytes o caracteres que se copian desde la posición actual en el origen de **flujo** al destino **flujo**. El valor predeterminado es -1, que especifica que todos los caracteres o bytes que se copian desde la posición actual hasta [sobrecargas eléctricas](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Comentarios  
 Este método copia el número especificado de caracteres o bytes, a partir de la actual posición especificada por el [posición](../../../ado/reference/ado-api/position-property-ado.md) propiedad. Si el número especificado es mayor que el número de bytes hasta disponibles **sobrecargas eléctricas**, a continuación, solo caracteres o bytes desde la posición actual hasta **sobrecargas eléctricas** se copian. Si el valor de *NumChars* es – 1 o se omite, se copian todos los caracteres o bytes a partir de la posición actual.  
  
 Si existen caracteres o bytes en la secuencia de destino, todo el contenido más allá del punto donde finaliza la copia permanecen y no se trunca. **Posición** será el byte inmediatamente después del último byte copiado. Si desea truncar estos bytes, llame a [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 **CopyTo** debe utilizarse para copiar datos a un destino **flujo** del mismo tipo como el origen de **flujo** (sus **tipo** valores de las propiedades son ambos **adTypeText** o ambos **adTypeBinary**). Para el texto **flujo** objetos, puede cambiar la [Charset](../../../ado/reference/ado-api/charset-property-ado.md) configuración de la propiedad del destino de **flujo** para traducir de un juego de caracteres a otro. Además, texto **flujo** objetos pueden copiarse correctamente en binario **flujo** objetos pero binario **flujo** no se copiarán los objetos en texto **flujo**  objetos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
