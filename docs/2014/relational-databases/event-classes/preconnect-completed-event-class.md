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
manager: craigg
ms.openlocfilehash: eaad0a80fd77257c6e79e092733d75c0c8df5df5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62827086"
---
# <a name="preconnectcompleted-event-class"></a>PreConnect:Completed, clase de eventos
  La clase de eventos PreConnect:Completed indica cuándo finaliza la ejecución de un desencadenador de LOGON o la función clasificadora de Regulador de recursos.  
  
## <a name="preconnectcompleted-event-class-data-columns"></a>Columnas de datos de la clase de eventos PreConnect:Completed  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|`int`|216|27|No|  
|SPID|`int`|El Id. del proceso de servidor que dispara este evento.|12|Sí|  
|EventSubClass|`int`|1 para la función clasificadora definida por el usuario.|21|Sí|  
|StartTime|`datetime`|La hora en la que se inicia la función clasificadora definida por el usuario.|14|Sí|  
|EndTime|`datetime`|La hora en la que se inicia la función clasificadora definida por el usuario.|15|Sí|  
|Duration|`bigint`|La cantidad de tiempo, en microsegundos, que ha utilizado la función clasificadora.|13|Sí|  
|ObjectID|`int`|El Id. del objeto clasificador definido por el usuario.|22|Sí|  
|CPU|`int`|Uso de la CPU en milisegundos.|18|Sí|  
|Lecturas|`int`|El número de lecturas lógicas.|16|Sí|  
|Escrituras|`int`|El número de escrituras lógicas.|17|Sí|  
|GroupID|`int`|El Id. del grupo de cargas de trabajo clasificado.|66|Sí|  
|Error|`int`|El último número de error en caso de que la función clasificadora definida por el usuario no se ejecute.|31|Sí|  
|State|`int`|El estado del último error.|30|Sí|  
|TargetUserName|`sysname`|El valor devuelto (nombre de grupo de cargas de trabajo) para la función clasificadora definida por el usuario en caso de que el sistema no encuentre el grupo activo correspondiente. De lo contrario, esta columna se establece en NULL.|39|Sí|  
|ObjectName|`nvarchar(256)`|El nombre de dos partes de la función del clasificador definida por el usuario. Por ejemplo, dbo.classifier.|34|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [Preconnect: Starting (clase de eventos)](preconnect-starting-event-class.md)   
 [Regulador de recursos](../resource-governor/resource-governor.md)  
  
  
