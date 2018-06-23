---
title: Las transacciones XTP | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 443d67e4-1c7f-41d7-b18d-2d657f58c22a
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6b890ec229755db9c6ee9b292bf632d110e9c189
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111124"
---
# <a name="xtp-transactions"></a>Transacciones XTP
  El objeto de rendimiento Transacciones XTP contiene contadores relacionados con las transacciones del motor de XTP en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 En esta tabla se describen los contadores de **Transacciones XTP** .  
  
|Contador|Descripción|  
|-------------|-----------------|  
|**Anulaciones en cascada/s**|Número de transacciones revertidas debido a una reversión de dependencia de confirmación (en promedio), por segundo.|  
|**Dependencias de confirmación realizadas/s**|Número de dependencias de confirmación realizadas por transacciones (en promedio), por segundo.|  
|**Transacciones de solo lectura preparadas/s**|Número de transacciones de solo lectura que se prepararon para el procesamiento de confirmaciones, por segundo.|  
|**Actualizaciones de punto de retorno/s**|Número de veces que se "actualizó" un punto de retorno (en promedio), por segundo. Una actualización de punto de retorno es cuando un punto de retorno existente se restablece al momento actual de la duración de la transacción.|  
|**Reversiones de punto de retorno/s**|Número de veces que se revertió una transacción a un punto de retorno (en promedio), por segundo.|  
|**Puntos de retorno creados/s**|Número de puntos de retorno creados (en promedio), por segundo.|  
|**Errores de validación de transacciones/s**|Número de transacciones que produjeron error en el procesamiento de validación (en promedio), por segundo.|  
|**Transacciones anuladas por el usuario/s**|Número de transacciones que el usuario anuló (en promedio), por segundo.|  
|**Transacciones anuladas/s**|Número de transacciones anuladas (tanto por el usuario como por el sistema, en promedio), por segundo.|  
|**Transacciones creadas/s**|Número de transacciones creadas en el sistema (en promedio), por segundo.<br /><br /> Las transacciones XTP se cuentan de manera distinta que las transacciones basadas en disco (según se refleja en Bases de datos: Transacciones/seg). Por ejemplo, Transacciones creadas/seg cuenta las transacciones de solo lectura, mientras que Bases de datos: Transacciones/seg no.|  
  
## <a name="see-also"></a>Vea también  
 [XTP &#40;OLTP en memoria&#41; contadores de rendimiento](../../integration-services/performance/performance-counters.md)  
  
  