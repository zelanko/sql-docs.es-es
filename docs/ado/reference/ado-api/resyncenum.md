---
title: ResyncEnum | Documentos de Microsoft
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
f1_keywords: ResyncEnum
helpviewer_keywords: ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f7ad5525f2f9e7ce7e915b97d397d3d7d372a27
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="resyncenum"></a>ResyncEnum
Especifica si se sobrescriben los valores subyacentes por una llamada a [Resync](../../../ado/reference/ado-api/resync-method.md).  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|Predeterminado: Sobrescribe los datos y se cancelan las actualizaciones pendientes.|  
|**adResyncUnderlyingValues**|1|No sobrescribir los datos y no se cancelan las actualizaciones pendientes.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>Se aplica a  
 [Método Resync](../../../ado/reference/ado-api/resync-method.md)
