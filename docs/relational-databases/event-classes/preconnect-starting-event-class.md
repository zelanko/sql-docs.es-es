---
title: PreConnect:Starting, clase de eventos |Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PreConnect:Starting Event Class
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de236e420c1f8f754b4af60a6710a0e9fafc7acf
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="preconnectstarting-event-class"></a>PreConnect:Starting, clase de eventos
  La clase de eventos PreConnect:Starting indica cuándo se inicia la ejecución un desencadenador de LOGON o la función clasificadora del regulador de recursos.  
  
## <a name="preconnectstarting-event-class-data-columns"></a>Columnas de datos de la clase de eventos PreConnect:Starting  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|**int**|215|27|No|  
|SPID|**int**|El Id. del proceso de servidor que dispara este evento.|12|Sí|  
|EventSubClass|**int**|1 para la función clasificadora definida por el usuario.|21|Sí|  
|StartTime|**datetime**|La hora en la que se inicia la función clasificadora definida por el usuario.|14|Sí|  
|ObjectID|**int**|El Id. del objeto clasificador definido por el usuario.|22|Sí|  
|ObjectName|**nvarchar(256)**|El nombre de dos partes de la función del clasificador definida por el usuario. Por ejemplo, dbo.classifier.|34|Sí|  
  
## <a name="see-also"></a>Vea también  
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)   
 [PreConnect:Completed, clase de eventos](../../relational-databases/event-classes/preconnect-completed-event-class.md)   
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)  
  
  
