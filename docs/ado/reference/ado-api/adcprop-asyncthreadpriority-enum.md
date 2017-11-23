---
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM | Documentos de Microsoft
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
f1_keywords: ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords: ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 39e10a6563e33ae1d1235bc220d7bd82826be853
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="adcpropasyncthreadpriorityenum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
Para un RDS [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) de objetos, especifica la prioridad de ejecución del subproceso asincrónico que recupera los datos.  
  
 Utilice estas constantes con la **Recordset** "**prioridad de subproceso en segundo plano**" propiedad dinámica, que se hace referencia en el índice de la propiedad dinámica de base de datos de ADO para OLE y se documentan en el [ Servicio de cursores de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentación.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|Establece la prioridad entre más altos y más normal.|  
|**adPriorityBelowNormal**|2|Establece la prioridad entre normal y más baja.|  
|**adPriorityHighest**|5|Establece la prioridad en el nivel más alto posible.|  
|**AdPriorityLowest**|1|Establece la prioridad en el nivel más bajo posible.|  
|**adPriorityNormal**|3|Establece la prioridad normal.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.AdcPropAsyncThreadPriority.ABOVENORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.BELOWNORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.HIGHEST|  
|AdoEnums.AdcPropAsyncThreadPriority.LOWEST|  
|AdoEnums.AdcPropAsyncThreadPriority.NORMAL|
