---
title: Configuración del filtro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.filtersettings.f1
ms.assetid: 1b401d7d-db8a-4ba1-acb1-b8dec14e3311
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bd4c6f3729d4d090854a48a65ce6d6a2465a98e2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721209"
---
# <a name="filter-settings"></a>Configuración del filtro
  El cuadro de diálogo **Configuración del filtro** permite definir los filtros para las cuadrículas del Monitor de replicación. Por ejemplo, para mostrar únicamente las suscripciones activas en la pestaña **Todas las suscripciones** , seleccione **Estado** en la columna **Nombre de columna** , **Es igual a** en la columna **Operador** y **Activo** en la columna **Valor1** . Después de definir un filtro basado en una o más columnas, se aplica el filtro para que la cuadrícula muestre solo el subconjunto de filas que coinciden con los criterios de filtro.  
  
## <a name="options"></a>Opciones  
 **Nombre de la columna**  
 Seleccione el nombre de la columna en la que desea filtrar. Puede basar un filtro en una o más columnas.  
  
 **Operador**  
 Seleccione un operador para el filtro, como por ejemplo **Menor o igual que**.  
  
 **Valor1** y **Valor2**  
 Escriba o seleccione un valor para el filtro. La mayoría de los operadores solo requieren un valor en la columna **Valor1** ; sin embargo, los operadores **Entre** y **No entre** también requieren un valor en la do columna **Valor2** .  
  
 **Borrar filtro**  
 Haga clic en este botón para borrar todos los filtros definidos. Para quitar un único filtro, seleccione el filtro y presione la tecla Supr.  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la replicación](monitoring-replication.md)  
  
  
