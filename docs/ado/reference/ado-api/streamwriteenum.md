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
author: rothja
ms.author: jroth
ms.openlocfilehash: 479bc032cf779752f11dccca73ee56fc05a8ebdd
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759571"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
Especifica si un separador de línea se anexa a la cadena escrita en un objeto de [secuencia](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|Predeterminada. Escribe la cadena de texto especificada (especificada por el parámetro de *datos* ) en el objeto de **secuencia** .|  
|**adWriteLine**|1|Escribe una cadena de texto y un carácter separador de líneas en un objeto de **secuencia** . Si no se define la propiedad [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) , se devuelve un error en tiempo de ejecución.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Estas constantes no tienen equivalentes de ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)
