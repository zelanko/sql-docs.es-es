---
title: Cursores XTP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 84bf4654-3ef7-4d7f-a269-c8bb4ed4acad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b591aa8e89200ca863b1e8196c383c506401fc3e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63151063"
---
# <a name="xtp-cursors"></a>Cursores XTP
  El objeto de rendimiento Cursores XTP contiene contadores relacionados con los cursores internos del motor de XTP. Los cursores son los bloques de creación de bajo nivel que el motor de XTP utiliza para procesar consultas de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Por tanto, el usuario no tiene normalmente control directo sobre ellos.  
  
 En esta tabla se describen los contadores de **cursores XTP** .  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Contadores de rendimiento de OLTP &#40;en memoria&#41;](../../integration-services/performance/performance-counters.md)  
  
  
