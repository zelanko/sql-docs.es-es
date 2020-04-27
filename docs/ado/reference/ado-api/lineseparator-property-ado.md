---
title: Propiedad LineSeparator (ADO) | Microsoft Docs
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
ms.openlocfilehash: 0343954f549f2cba4b535b8ab4ebafec5a842015
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918284"
---
# <a name="lineseparator-property-ado"></a>Separador de línea (propiedad, ADO)
Indica el carácter binario que se va a utilizar como separador de línea en los objetos de [flujo](../../../ado/reference/ado-api/stream-object-ado.md) de texto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de [LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md) que indica el carácter separador de línea utilizado en la **secuencia**. El valor predeterminado es **adCRLF**.  
  
## <a name="remarks"></a>Observaciones  
 **LineSeparator** se usa para interpretar las líneas al leer el contenido de una **secuencia**de texto. Las líneas se pueden omitir con el método [SkipLine](../../../ado/reference/ado-api/skipline-method.md) .  
  
 **LineSeparator** solo se utiliza con objetos de **flujo** de texto (el[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**). Esta propiedad se omite si el **tipo** es **adTypeBinary**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
