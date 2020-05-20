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
author: rothja
ms.author: jroth
ms.openlocfilehash: dca33c975b3d25347b0cb9bb804b852ec5f93d7d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765396"
---
# <a name="seekenum"></a>SeekEnum
Especifica el tipo de [búsqueda](../../../ado/reference/ado-api/seek-method.md) que se va a ejecutar.  
  
|Constante|Valor|Descripción|  
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
