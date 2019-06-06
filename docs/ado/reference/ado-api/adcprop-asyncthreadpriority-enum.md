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
manager: jroth
ms.openlocfilehash: 18ffebe5cbf781212b6b8962f9f48d61281c7d30
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66703988"
---
# <a name="adcpropasyncthreadpriorityenum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
Para una RDS [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) de objetos, especifica la prioridad de ejecución del subproceso asincrónica que recupera los datos.  
  
 Utilice estas constantes con la **Recordset** "**prioridad de subproceso en segundo plano**" propiedad dinámica que se hace referencia en el índice de propiedades dinámicas de ADO y se documentan en el [ Servicio de cursores de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentación.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|Establece la prioridad entre normal y máxima.|  
|**adPriorityBelowNormal**|2|Establece la prioridad entre más baja y normal.|  
|**adPriorityHighest**|5|Establece la prioridad en el nivel más alto posible.|  
|**AdPriorityLowest**|1|Establece la prioridad en el nivel más bajo posible.|  
|**adPriorityNormal**|3|Establece la prioridad normal.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.AdcPropAsyncThreadPriority.ABOVENORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.BELOWNORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.HIGHEST|  
|AdoEnums.AdcPropAsyncThreadPriority.LOWEST|  
|AdoEnums.AdcPropAsyncThreadPriority.NORMAL|
