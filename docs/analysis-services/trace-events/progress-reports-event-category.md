---
title: "Informes de progreso (categor&#237;a de eventos) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "eventos de progreso [Analysis Services]"
  - "informes de progreso, categoría de eventos"
  - "clases de eventos [Analysis Services], informes de progreso"
ms.assetid: c130f160-28ef-49bc-9ee6-da47dc9aab2a
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 23
---
# Informes de progreso (categor&#237;a de eventos)
  La categoría de eventos Informes de progreso tiene las clases de eventos que se describen en la siguiente tabla.  
  
|Clase de eventos|Identificador del evento|Description|  
|-----------------|--------------|-----------------|  
|Progress Report Begin|5|Recopila todos los eventos de inicio de informe de progreso desde que se inició el seguimiento.|  
|Progress Report End|6|Recopila todos los eventos de fin de informe de progreso desde que se inició el seguimiento.|  
|Progress Report Current|7|Recopila todos los eventos actuales de informe de progreso desde que se inició el seguimiento. Por ejemplo, durante el procesamiento, los informes actuales incluyen información de procesamiento acerca de los objetos que se están procesando (dimensiones, particiones, cubos, etc.).|  
|Progress Report Error|8|Recopila todos los eventos de error de informe de progreso desde que se inició el seguimiento.|  
  
 Todos los eventos Progress Report Begin se inician con un flujo de eventos de progreso y finalizan con un evento Progress Report End. El flujo puede incluir cualquier número de eventos Progress Report Current y Progress Report Error.  
  
 Para obtener información sobre las columnas asociadas a cada una de las clases de evento de Informes de progreso, vea [Progress Reports Data Columns](../../analysis-services/trace-events/progress-reports-data-columns.md).  
  
## Vea también  
 [Eventos de seguimiento de Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  