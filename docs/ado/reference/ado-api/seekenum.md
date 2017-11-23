---
title: SeekEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: SeekEnum
helpviewer_keywords: SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 97a2a99c7310022e86e574a0f4b04227cee95726
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="seekenum"></a>SeekEnum
Especifica el tipo de [Seek](../../../ado/reference/ado-api/seek-method.md) para ejecutar.  
  
|Constante|Valor|Description|  
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
