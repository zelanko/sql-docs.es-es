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
ms.openlocfilehash: 4cc9de1481cc683bddafe2f92959977319600f6a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928630"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
Especifica si un separador de línea se anexa a la cadena escrita en un objeto de [secuencia](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|Default. Escribe la cadena de texto especificada (especificada por el parámetro de *datos* ) en el objeto de **secuencia** .|  
|**adWriteLine**|1|Escribe una cadena de texto y un carácter separador de líneas en un objeto de **secuencia** . Si no se define la propiedad [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) , se devuelve un error en tiempo de ejecución.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Estas constantes no tienen equivalentes de ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)
