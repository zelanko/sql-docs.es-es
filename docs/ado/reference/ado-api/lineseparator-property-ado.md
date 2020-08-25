---
description: Separador de línea (propiedad, ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: fe0976fda4a390f93f7d634fac9e1cbc52104b29
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774634"
---
# <a name="lineseparator-property-ado"></a>Separador de línea (propiedad, ADO)
Indica el carácter binario que se va a utilizar como separador de línea en los objetos de [flujo](./stream-object-ado.md) de texto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de [LineSeparatorsEnum](./lineseparatorsenum.md) que indica el carácter separador de línea utilizado en la **secuencia**. El valor predeterminado es **adCRLF**.  
  
## <a name="remarks"></a>Observaciones  
 **LineSeparator** se usa para interpretar las líneas al leer el contenido de una **secuencia**de texto. Las líneas se pueden omitir con el método [SkipLine](./skipline-method.md) .  
  
 **LineSeparator** solo se utiliza con objetos de **flujo** de texto (el[tipo](./type-property-ado-stream.md) es **adTypeText**). Esta propiedad se omite si el **tipo** es **adTypeBinary**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Objeto de secuencia (ADO)](./stream-object-ado.md)