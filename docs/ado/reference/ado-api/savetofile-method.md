---
title: Método SaveToFile | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SaveToFile
- _Stream::SaveToFile
helpviewer_keywords:
- SaveToFile method [ADO]
ms.assetid: 8a8594f2-422b-4d2e-94f8-7fe337445900
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6afe36c7b3923c9ebf33fd615a1c21e34955e62d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63315218"
---
# <a name="savetofile-method"></a>Método SaveToFile
Guarda el contenido binario de un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) a un archivo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>Parámetros  
 *FileName*  
 Un **cadena** valor que contiene el nombre completo del archivo al que el contenido de la **Stream** se guardarán. Puede guardar en cualquier ubicación local válida o cualquier ubicación tiene acceso a través de un valor UNC.  
  
 *SaveOptions*  
 Un [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md) valor que especifica si se debe crear un nuevo archivo por **SaveToFile**, si aún no existe. Valor predeterminado es **adSaveCreateNotExists**. Con estas opciones puede especificar que se produce un error si el archivo especificado no existe. También puede especificar que **SaveToFile** sobrescribe el contenido actual de un archivo existente.  
  
> [!NOTE]
>  Si sobrescribe un archivo existente (cuando **adSaveCreateOverwrite** está establecido), **SaveToFile** truncará los bytes del archivo existente original que siguen a la nueva [EOS](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Comentarios  
 **SaveToFile** puede utilizarse para copiar el contenido de un **Stream** objeto en un archivo local. No hay ningún cambio en el contenido o las propiedades de la **Stream** objeto. El **Stream** objeto debe estar abierto antes de llamar a **SaveToFile**.  
  
 Este método no cambia la asociación de la **Stream** objeto a su origen subyacente. El **Stream** objeto aún estará asociado con la dirección URL original o **registro** que era su origen al abrirse.  
  
 Después de un **SaveToFile** operación, la posición actual ([posición](../../../ado/reference/ado-api/position-property-ado.md)) en la secuencia se establece en el principio de la secuencia (0).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método Open (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Save (método)](../../../ado/reference/ado-api/save-method.md)
