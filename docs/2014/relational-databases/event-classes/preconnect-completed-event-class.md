---
title: PreConnect:Completed, clase de eventos |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- PreConnect:Completed Event Class
ms.assetid: 7ed2f620-6511-4985-9961-d2927c2b1759
author: stevestein
ms.author: sstein
ms.openlocfilehash: 56af8e7de291c81736d2b83abf8a31a972653c8f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85052788"
---
# <a name="preconnectcompleted-event-class"></a>PreConnect:Completed, clase de eventos
  La clase de eventos PreConnect:Completed indica cuándo finaliza la ejecución de un desencadenador de LOGON o la función clasificadora de Regulador de recursos.  
  
## <a name="preconnectcompleted-event-class-data-columns"></a>Columnas de datos de la clase de eventos PreConnect:Completed  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|`int`|216|27|No|  
|SPID|`int`|El Id. del proceso de servidor que dispara este evento.|12|Yes|  
|EventSubClass|`int`|1 para la función clasificadora definida por el usuario.|21|Yes|  
|StartTime|`datetime`|La hora en la que se inicia la función clasificadora definida por el usuario.|14|Yes|  
|EndTime|`datetime`|La hora en la que se inicia la función clasificadora definida por el usuario.|15|Sí|  
|Duration|`bigint`|La cantidad de tiempo, en microsegundos, que ha utilizado la función clasificadora.|13|Yes|  
|ObjectID|`int`|El Id. del objeto clasificador definido por el usuario.|22|Yes|  
|CPU|`int`|Uso de la CPU en milisegundos.|18|Sí|  
|Lecturas|`int`|El número de lecturas lógicas.|16|Yes|  
|Escrituras|`int`|El número de escrituras lógicas.|17|Sí|  
|GroupID|`int`|El Id. del grupo de cargas de trabajo clasificado.|66|Yes|  
|Error|`int`|El último número de error en caso de que la función clasificadora definida por el usuario no se ejecute.|31|Yes|  
|State|`int`|El estado del último error.|30|Yes|  
|TargetUserName|`sysname`|El valor devuelto (nombre de grupo de cargas de trabajo) para la función clasificadora definida por el usuario en caso de que el sistema no encuentre el grupo activo correspondiente. De lo contrario, esta columna se establece en NULL.|39|Yes|  
|ObjectName|`nvarchar(256)`|El nombre de dos partes de la función del clasificador definida por el usuario. Por ejemplo, dbo.classifier.|34|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [Preconnect: Starting (clase de eventos)](preconnect-starting-event-class.md)   
 [Regulador de recursos](../resource-governor/resource-governor.md)  
  
  
