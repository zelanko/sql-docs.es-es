---
title: Configuración del filtro | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.filtersettings.f1
ms.assetid: 1b401d7d-db8a-4ba1-acb1-b8dec14e3311
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 58750ffba9d8eb19c02ceb4870fda0ddffeb5a7d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85653142"
---
# <a name="filter-settings"></a>Configuración del filtro
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
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
  
## <a name="see-also"></a>Consulte también  
 [Supervisar la replicación](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
