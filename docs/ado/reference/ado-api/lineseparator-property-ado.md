---
title: LineSeparator (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::LineSeparator
helpviewer_keywords:
- LineSeparator property [ADO]
ms.assetid: 0b20fbb8-6b83-48ec-b442-f96c8a4bafbb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e3035e8614dbe57d131ee77dc77fb85605499c15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66694727"
---
# <a name="lineseparator-property-ado"></a>Separador de línea (propiedad, ADO)
Indica el carácter binario que se usará como separador de línea en texto [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objetos.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md) valor que indica el carácter de separador de línea utilizado en el **Stream**. El valor predeterminado es **adCRLF**.  
  
## <a name="remarks"></a>Comentarios  
 **LineSeparator** se usa para interpretar líneas al leer el contenido de un texto **Stream**. Se pueden omitir las líneas con el [SkipLine](../../../ado/reference/ado-api/skipline-method.md) método.  
  
 **LineSeparator** solo se usa con texto **Stream** objetos ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**). Esta propiedad se omite si **tipo** es **adTypeBinary**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
