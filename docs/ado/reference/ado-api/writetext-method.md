---
title: Método WriteText | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_WriteText
- _Stream::WriteText
helpviewer_keywords:
- WriteText method [ADO]
ms.assetid: 7a669048-13f4-4574-a2b1-985e089729d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3b50db388151de1f5b99d8d9a3f48904e6d7c2c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47679893"
---
# <a name="writetext-method"></a>Método WriteText
Escribe una cadena de texto especificado en un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Datos*  
 Un **cadena** valor que contiene el texto de caracteres que se escribirá.  
  
 *Opciones*  
 Opcional. Un [StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md) valor que especifica si se debe escribir un carácter separador de línea al final de la cadena especificada.  
  
## <a name="remarks"></a>Comentarios  
 Cadenas especificadas se escriben en el **Stream** objeto sin espacios intermedios ni caracteres entre cada cadena.  
  
 Actual [posición](../../../ado/reference/ado-api/position-property-ado.md) se establece en el carácter que sigue a los datos escritos. El **WriteText** método no trunca el resto de los datos en una secuencia. Si desea truncar estos caracteres, llame a [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 Si escribe más allá de la actual [EOS](../../../ado/reference/ado-api/eos-property.md) posición, el [tamaño](../../../ado/reference/ado-api/size-property-ado-stream.md) de la **Stream** se incrementará para contener los caracteres nuevos, y **EOS** se moverá hasta el último byte nuevo en el **Stream**.  
  
> [!NOTE]
>  El **WriteText** método se utiliza con secuencias de texto ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**). Para secuencias binarias (**tipo** es **adTypeBinary**), utilice [escribir](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método Write](../../../ado/reference/ado-api/write-method.md)
