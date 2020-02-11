---
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22a8cd4bb8d1bdddbaaa68e92349d9c728557ac0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921467"
---
# <a name="adcprop_asyncthreadpriority_enum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
Para un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) RDS, especifica la prioridad de ejecución del subproceso asincrónico que recupera los datos.  
  
 Use estas constantes con la propiedad dinámica "**prioridad del subproceso en segundo plano**" del **conjunto de registros** , a la que se hace referencia en el índice de propiedades dinámicas de ADO a OLE DB y que se documenta en el [servicio de cursores de Microsoft para obtener OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentación.  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|Establece la prioridad entre normal y superior.|  
|**adPriorityBelowNormal**|2|Establece la prioridad entre el nivel más bajo y el normal.|  
|**adPriorityHighest**|5|Establece la prioridad del valor más alto posible.|  
|**AdPriorityLowest**|1|Establece la prioridad de la más baja posible.|  
|**adPriorityNormal**|3|Establece la prioridad en normal.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. AdcPropAsyncThreadPriority. ABOVENORMAL|  
|AdoEnums. AdcPropAsyncThreadPriority. BELOWNORMAL|  
|AdoEnums. AdcPropAsyncThreadPriority. HIGHEST|  
|AdoEnums. AdcPropAsyncThreadPriority. más bajo|  
|AdoEnums. AdcPropAsyncThreadPriority. NORMAL|
