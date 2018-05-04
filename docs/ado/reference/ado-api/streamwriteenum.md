---
title: StreamWriteEnum | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c7fb6df40fc26bb264459080a42654370112fc7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="streamwriteenum"></a>StreamWriteEnum
Especifica si se agrega un separador de línea a la cadena escrita en un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|Predeterminado: Escribe la cadena de texto especificado (especificado por el *datos* parámetro) a la **flujo** objeto.|  
|**adWriteLine**|1|Escribe una cadena de texto y un carácter de separador de línea a un **flujo** objeto. Si el [separador de línea](../../../ado/reference/ado-api/lineseparator-property-ado.md) propiedad no está definida, a continuación, se devuelve un error en tiempo de ejecución.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)
