---
title: "Separador de línea (propiedad, ADO) | Documentos de Microsoft"
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
- _Stream::LineSeparator
helpviewer_keywords:
- LineSeparator property [ADO]
ms.assetid: 0b20fbb8-6b83-48ec-b442-f96c8a4bafbb
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2be2e27fa93791647fd3e27945c3203cf1afe999
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="lineseparator-property-ado"></a>Separador de línea (propiedad, ADO)
Indica el carácter binario que se usará como separador de línea en texto [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objetos.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md) valor que indica el carácter de separador de línea utilizado en el **flujo**. El valor predeterminado es **adCRLF**.  
  
## <a name="remarks"></a>Comentarios  
 **Separador de línea** se usa para interpretar líneas al leer el contenido de un texto **flujo**. Las líneas se pueden omitir con el [SkipLine](../../../ado/reference/ado-api/skipline-method.md) método.  
  
 **Separador de línea** sólo se utiliza con texto **flujo** objetos ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**). Esta propiedad se omite si **tipo** es **adTypeBinary**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
