---
title: SeekEnum | Documentos de Microsoft
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
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 25585f77de1e5a05051d4fad8e1cdca7ca1172c6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="seekenum"></a>SeekEnum
Especifica el tipo de [Seek](../../../ado/reference/ado-api/seek-method.md) para ejecutar.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|Busca la primera clave igual a *KeyValue*.|  
|**adSeekLastEQ**|2|Busca la última clave igual a *KeyValue*.|  
|**adSeekAfterEQ**|4|Busca una clave igual a *KeyValue* o justo después de donde se habría producido esa coincidencia.|  
|**adSeekAfter**|8|Busca una clave justo después de where una coincidencia con *KeyValue* hubiera tenido lugar.|  
|**adSeekBeforeEQ**|16|Busca una clave igual a *KeyValue*o justo antes de donde se habría producido esa coincidencia.|  
|**adSeekBefore**|32|Busca una clave justo antes de que una coincidencia con *KeyValue* hubiera tenido lugar.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.Seek.FIRSTEQ|  
|AdoEnums.Seek.LASTEQ|  
|AdoEnums.Seek.AFTEREQ|  
|AdoEnums.Seek.AFTER|  
|AdoEnums.Seek.BEFOREEQ|  
|AdoEnums.Seek.BEFORE|  
  
## <a name="applies-to"></a>Se aplica a  
 [El método de búsqueda](../../../ado/reference/ado-api/seek-method.md)
