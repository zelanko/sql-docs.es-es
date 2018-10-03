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
manager: craigg
ms.openlocfilehash: d0f42561d7b324a13068c14d0fc7971d3d46d83b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633493"
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
