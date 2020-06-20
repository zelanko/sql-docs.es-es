---
title: PreConnect:Starting, clase de eventos |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- PreConnect:Starting Event Class
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
author: stevestein
ms.author: sstein
ms.openlocfilehash: 67b642d369c73cc144af31f835786613766045f9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85028846"
---
# <a name="preconnectstarting-event-class"></a>PreConnect:Starting, clase de eventos
  La clase de eventos PreConnect:Starting indica cuándo se inicia la ejecución un desencadenador de LOGON o la función clasificadora del regulador de recursos.  
  
## <a name="preconnectstarting-event-class-data-columns"></a>Columnas de datos de la clase de eventos PreConnect:Starting  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|`int`|215|27|No|  
|SPID|`int`|El Id. del proceso de servidor que dispara este evento.|12|Yes|  
|EventSubClass|`int`|1 para la función clasificadora definida por el usuario.|21|Yes|  
|StartTime|`datetime`|La hora en la que se inicia la función clasificadora definida por el usuario.|14|Sí|  
|ObjectID|`int`|El Id. del objeto clasificador definido por el usuario.|22|Sí|  
|ObjectName|`nvarchar(256)`|El nombre de dos partes de la función del clasificador definida por el usuario. Por ejemplo, dbo.classifier.|34|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [Preconnect: Completed (clase de eventos)](preconnect-completed-event-class.md)   
 [Regulador de recursos](../resource-governor/resource-governor.md)  
  
  
