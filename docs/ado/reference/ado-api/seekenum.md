---
title: SeekEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 886825b4d32354572a5162487add419b00ec35d6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931062"
---
# <a name="seekenum"></a>SeekEnum
Especifica el tipo de [búsqueda](../../../ado/reference/ado-api/seek-method.md) que se va a ejecutar.  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|Busca la primera clave igual a *keyValues*.|  
|**adSeekLastEQ**|2|Busca la última clave igual a *keyValues*.|  
|**adSeekAfterEQ**|4|Busca una clave igual a *keyValues* o justo después de donde se hubiera producido esa coincidencia.|  
|**adSeekAfter**|8|Busca una clave justo después de donde se habría producido una coincidencia con *keyValues* .|  
|**adSeekBeforeEQ**|16|Busca una clave igual a *keyValues*o justo antes de que se hubiera producido esa coincidencia.|  
|**adSeekBefore**|32|Busca una clave justo antes de que se hubiera producido una coincidencia con *keyValues* .|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. Seek. FIRSTEQ|  
|AdoEnums. Seek. LASTEQ|  
|AdoEnums. Seek. AFTEREQ|  
|AdoEnums. Seek. AFTER|  
|AdoEnums. Seek. BEFOREEQ|  
|AdoEnums. Seek. BEFORe|  
  
## <a name="applies-to"></a>Se aplica a  
 [Seek (método)](../../../ado/reference/ado-api/seek-method.md)
