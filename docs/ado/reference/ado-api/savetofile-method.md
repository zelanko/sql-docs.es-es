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
ms.openlocfilehash: c2e56178ad306d5b39c2445c391c3bbabe4fc424
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917032"
---
# <a name="savetofile-method"></a>Método SaveToFile
Guarda el contenido binario de una [secuencia](../../../ado/reference/ado-api/stream-object-ado.md) en un archivo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>Parámetros  
 *FileName*  
 Valor de **cadena** que contiene el nombre completo del archivo en el que se guardará el contenido de la **secuencia** . Puede guardar en cualquier ubicación local válida o en cualquier ubicación a la que tenga acceso a través de un valor UNC.  
  
 *SaveOptions*  
 Valor [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md) que especifica si **SaveToFile**debe crear un nuevo archivo, si aún no existe. El valor predeterminado es **adSaveCreateNotExists**. Con estas opciones, puede especificar que se produzca un error si el archivo especificado no existe. También puede especificar que **SaveToFile** sobrescriba el contenido actual de un archivo existente.  
  
> [!NOTE]
>  Si sobrescribe un archivo existente (cuando se establece **adSaveCreateOverwrite** ), **SaveToFile** truncará cualquier byte del archivo existente original que siga el nuevo [EOS](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Observaciones  
 **SaveToFile** se puede usar para copiar el contenido de un objeto de **secuencia** en un archivo local. No hay ningún cambio en el contenido o las propiedades del objeto de **secuencia** . El objeto de **secuencia** debe estar abierto antes de llamar a **SaveToFile**.  
  
 Este método no cambia la Asociación del objeto de **secuencia** a su origen subyacente. El objeto de **secuencia** todavía se asociará a la dirección URL o **registro** original que era su origen al abrirse.  
  
 Después de una operación de **SaveToFile** , la posición actual ([posición](../../../ado/reference/ado-api/position-property-ado.md)) en la secuencia se establece en el principio de la secuencia (0).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Open (método, secuencia de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Save (método)](../../../ado/reference/ado-api/save-method.md)
