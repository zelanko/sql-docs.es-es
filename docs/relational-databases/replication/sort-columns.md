---
title: Ordenar columnas | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.sortcolumns.f1
ms.assetid: 66b44b6c-10a5-4e3f-a97b-7568609c88ac
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b699d8e81d79bd9364aaaa3efd892a2b28788988
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32962265"
---
# <a name="sort-columns"></a>Ordenar columnas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El cuadro de diálogo **Ordenar columnas** le permite ordenar las cuadrículas en el Monitor de replicación basado en una o más columnas. (También puede ordenar en una columna única haciendo clic en el encabezado de columna en la cuadrícula del Monitor de replicación). Por ejemplo, para ordenar suscripciones en la pestaña **Todas las suscripciones** basándose en el estado y después el tipo de conexión, siga estos pasos:  
  
1.  En la primera fila de la cuadrícula, seleccione **Estado** de la columna **Nombre de columna** y un valor de la columna **Criterio de ordenación**  
  
2.  En la segunda fila de la cuadrícula, seleccione **Tipo de conexión** de la columna **Nombre de columna** y un valor de la columna **Criterio de ordenación** .  
  
## <a name="options"></a>Opciones  
 **Nombre de columna**  
 El nombre de la columna en la que desea ordenar. Puede ordenar en una o más columnas. No puede ordenar en las columnas **Rendimiento medio actual** o **Peor rendimiento actual** en la pestaña **Publicaciones** , debido a la manera en la que se calculan estos valores de columna.  
  
 **Criterio de ordenación**  
 Especifique un valor **Ascendente** o **Descendente**.  
  
 **Borrar todo**  
 Quite todas las filas de la cuadrícula de ordenación. Para quitar una fila única, seleccione la fila y presione la tecla Suprimir.  
  
## <a name="see-also"></a>Ver también  
 [Supervisar la replicación](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
