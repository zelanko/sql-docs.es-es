---
title: Cursores XTP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 84bf4654-3ef7-4d7f-a269-c8bb4ed4acad
caps.latest.revision: 4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c5eab11a0ee57a8545a2d19f8a7472392635e690
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37206985"
---
# <a name="xtp-cursors"></a>Cursores XTP
  El objeto de rendimiento Cursores XTP contiene contadores relacionados con los cursores internos del motor de XTP. Los cursores son los bloques de creación de bajo nivel que el motor de XTP utiliza para procesar consultas de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Por tanto, el usuario no tiene normalmente control directo sobre ellos.  
  
 Esta tabla se describen los **cursores XTP** contadores.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|**Eliminaciones de cursor/s**|Número de eliminaciones de cursor (en promedio), por segundo.|  
|**Inserciones de cursor/s**|Número de inserciones de cursor (en promedio), por segundo.|  
|**Recorridos de cursor iniciados/s**|Número de recorridos de cursor iniciados (en promedio), por segundo.|  
|**Infracciones de restricciones UNIQUE de cursor/s**|Número de infracciones de restricciones UNIQUE (en promedio), por segundo.|  
|**Actualizaciones de cursor/s**|Número de actualizaciones de cursor (en promedio), por segundo.|  
|**Conflictos de escritura de cursor/s**|Número de conflictos de escritura contra escritura en la misma versión de fila (en promedio), por segundo.|  
|**Reintentos de recorrido de esquinas sucias/s (emitidos por el usuario)**|Número de reintentos de recorrido debido a conflictos de escritura durante los rastreos de esquinas sucias emitidos por un recorrido de tabla completo del usuario (en promedio), por segundo. Es un contador de nivel muy bajo, no está pensado para uso de los clientes.|  
|**Filas expiradas quitadas/s**|Número de filas expiradas quitadas mediante cursores (en promedio), por segundo.|  
|**Filas expiradas tocadas/s**|Número de filas expiradas tocadas mediante cursores (en promedio), por segundo.|  
|**Filas devueltas/s**|Número de filas devueltas mediante cursores (en promedio), por segundo.|  
|**Filas tocadas/s**|Número de filas tocadas mediante cursores (en promedio), por segundo.|  
|**Filas tocadas eliminadas provisionalmente/s**|Número de filas que van a expirar tocadas mediante cursores (en promedio), por segundo. Una fila va a expirar si la transacción que la eliminó permanece activa (es decir, no se confirma o anula).|  
  
## <a name="see-also"></a>Vea también  
 [XTP &#40;OLTP en memoria&#41; los contadores de rendimiento](../../integration-services/performance/performance-counters.md)  
  
  
