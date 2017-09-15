---
title: StreamWriteEnum | Documentos de Microsoft
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
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 586920fc4f7673f9c5e25c92f252013920acaa8d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="streamwriteenum"></a>StreamWriteEnum
Especifica si se agrega un separador de línea a la cadena escrita en un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|Predeterminado: Escribe la cadena de texto especificado (especificado por el *datos* parámetro) a la **flujo** objeto.|  
|**adWriteLine**|1|Escribe una cadena de texto y un carácter de separador de línea a un **flujo** objeto. Si el [separador de línea](../../../ado/reference/ado-api/lineseparator-property-ado.md) propiedad no está definida, a continuación, se devuelve un error en tiempo de ejecución.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)
