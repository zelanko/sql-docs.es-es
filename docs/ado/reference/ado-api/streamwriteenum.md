---
title: StreamWriteEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f34ff1bba827678273590fdc1b39a001b5931644
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710827"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
Especifica si se agrega un separador de línea a la cadena escrita en un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|Predeterminado: Escribe la cadena de texto especificado (especificado por el *datos* parámetro) a la **Stream** objeto.|  
|**adWriteLine**|1|Escribe una cadena de texto y un carácter de separador de línea para un **Stream** objeto. Si el [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) propiedad no está definida y, después, se devuelve un error de tiempo de ejecución.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Estas constantes no tienen equivalentes de ADO y WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)
