---
description: StreamWriteEnum
title: StreamWriteEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: c09a15f5c5aba9d36f038304b68cc1e64112ade3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988446"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
Especifica si un separador de línea se anexa a la cadena escrita en un objeto de [secuencia](./stream-object-ado.md) .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|Predeterminada. Escribe la cadena de texto especificada (especificada por el parámetro de *datos* ) en el objeto de **secuencia** .|  
|**adWriteLine**|1|Escribe una cadena de texto y un carácter separador de líneas en un objeto de **secuencia** . Si no se define la propiedad [LineSeparator](./lineseparator-property-ado.md) , se devuelve un error en tiempo de ejecución.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Estas constantes no tienen equivalentes de ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método WriteText](./writetext-method.md)