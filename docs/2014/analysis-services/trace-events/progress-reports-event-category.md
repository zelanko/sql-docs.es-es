---
title: Categoría de eventos de informes de progreso | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- progress events [Analysis Services]
- Progress Reports event category
- event classes [Analysis Services], progress reports
ms.assetid: c130f160-28ef-49bc-9ee6-da47dc9aab2a
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8bcfa530f87d7a8caaee6814c2e2e2282e2783ed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103639"
---
# <a name="progress-reports-event-category"></a>informes de progreso, categoría de eventos
  La categoría de eventos Informes de progreso tiene las clases de eventos que se describen en la siguiente tabla.  
  
|Clase de eventos|Identificador del evento|Descripción|  
|-----------------|--------------|-----------------|  
|Progress Report Begin|5|Recopila todos los eventos de inicio de informe de progreso desde que se inició el seguimiento.|  
|Progress Report End|6|Recopila todos los eventos de fin de informe de progreso desde que se inició el seguimiento.|  
|Progress Report Current|7|Recopila todos los eventos actuales de informe de progreso desde que se inició el seguimiento. Por ejemplo, durante el procesamiento, los informes actuales incluyen información de procesamiento acerca de los objetos que se están procesando (dimensiones, particiones, cubos, etc.).|  
|Progress Report Error|8|Recopila todos los eventos de error de informe de progreso desde que se inició el seguimiento.|  
  
 Todos los eventos Progress Report Begin se inician con un flujo de eventos de progreso y finalizan con un evento Progress Report End. El flujo puede incluir cualquier número de eventos Progress Report Current y Progress Report Error.  
  
 Para obtener información sobre las columnas asociadas a cada una de las clases de evento de Informes de progreso, vea [Progress Reports Data Columns](progress-reports-data-columns.md).  
  
## <a name="see-also"></a>Vea también  
 [Eventos de seguimiento de Analysis Services](analysis-services-trace-events.md)  
  
  