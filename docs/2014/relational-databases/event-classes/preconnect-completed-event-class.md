---
title: PreConnect:Completed, clase de eventos |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- PreConnect:Completed Event Class
ms.assetid: 7ed2f620-6511-4985-9961-d2927c2b1759
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5a91728174a11ecf1cdd008b5aa1c9829da890ff
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150696"
---
# <a name="preconnectcompleted-event-class"></a>PreConnect:Completed, clase de eventos
  La clase de eventos PreConnect:Completed indica cuándo finaliza la ejecución de un desencadenador de LOGON o la función clasificadora de Regulador de recursos.  
  
## <a name="preconnectcompleted-event-class-data-columns"></a>Columnas de datos de la clase de eventos PreConnect:Completed  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|`int`|216|27|no|  
|SPID|`int`|El Id. del proceso de servidor que dispara este evento.|12|Sí|  
|EventSubClass|`int`|1 para la función clasificadora definida por el usuario.|21|Sí|  
|StartTime|`datetime`|La hora en la que se inicia la función clasificadora definida por el usuario.|14|Sí|  
|EndTime|`datetime`|La hora en la que se inicia la función clasificadora definida por el usuario.|15|Sí|  
|Duration|`bigint`|La cantidad de tiempo, en microsegundos, que ha utilizado la función clasificadora.|13|Sí|  
|ObjectID|`int`|El Id. del objeto clasificador definido por el usuario.|22|Sí|  
|CPU|`int`|Uso de la CPU en milisegundos.|18|Sí|  
|Reads|`int`|El número de lecturas lógicas.|16|Sí|  
|Writes|`int`|El número de escrituras lógicas.|17|Sí|  
|GroupID|`int`|El Id. del grupo de cargas de trabajo clasificado.|66|Sí|  
|Error|`int`|El último número de error en caso de que la función clasificadora definida por el usuario no se ejecute.|31|Sí|  
|State|`int`|El estado del último error.|30|Sí|  
|TargetUserName|`sysname`|El valor devuelto (nombre de grupo de cargas de trabajo) para la función clasificadora definida por el usuario en caso de que el sistema no encuentre el grupo activo correspondiente. De lo contrario, esta columna se establece en NULL.|39|Sí|  
|ObjectName|`nvarchar(256)`|El nombre de dos partes de la función del clasificador definida por el usuario. Por ejemplo, dbo.classifier.|34|Sí|  
  
## <a name="see-also"></a>Vea también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [PreConnect:Starting, clase de eventos](preconnect-starting-event-class.md)   
 [Regulador de recursos](../resource-governor/resource-governor.md)  
  
  
