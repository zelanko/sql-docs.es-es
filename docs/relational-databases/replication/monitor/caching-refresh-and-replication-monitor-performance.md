---
title: Almacenamiento en caché, actualización y rendimiento del Monitor de replicación
description: Aprenda sobre el almacenamiento en caché, la actualización y la optimización del rendimiento del Monitor de replicación de SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], Replication Monitor
- cache [SQL Server], replication
- Replication Monitor, caching
- refreshing data
- Replication Monitor, refreshing
ms.assetid: a2d8b666-ed41-4f86-b2b8-c8e118416ab7
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 45cad9f38fadd8280b6cb155c0e44643448ac4bf
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "76286355"
---
# <a name="caching-refresh-and-replication-monitor-performance"></a>Almacenamiento en caché, actualización y rendimiento del Monitor de replicación
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  El Monitor de replicación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está diseñado para supervisar de manera eficaz un gran número de equipos en un sistema de producción. Las consultas que utiliza el Monitor de replicación para realizar cálculos y recopilar datos se almacenan en caché y se actualizan periódicamente. El almacenamiento en caché reduce el número de consultas y cálculos necesarios para ver diferentes páginas en el Monitor de replicación, y permite escalar la supervisión para varios usuarios.  
  
 Un trabajo del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , el **Actualizador de supervisión de replicación para distribución**, controla la actualización de la caché. El trabajo se ejecuta continuamente, pero la programación de actualización de la caché se basa en esperar determinado tiempo después de la actualización anterior:  
  
-   Si hay cambios en el historial del agente desde que se creó la caché por última vez, el tiempo de espera es el menor de los siguientes: 4 segundos o el tiempo necesario para crear la caché anterior.  
  
-   Si no hay cambios en el historial del agente desde que se creó la caché por última vez (aunque haya habido otros cambios), el tiempo de espera es el mayor de los siguientes: 30 segundos o el tiempo necesario para crear la caché anterior.  
  
## <a name="refreshing-the-replication-monitor-user-interface"></a>Actualizar la interfaz de usuario del Monitor de replicación  
 La interfaz de usuario del Monitor de replicación se puede actualizar de varias formas:  
  
-   La ventana principal del Monitor de replicación (y todas sus pestañas) se actualiza automáticamente, de manera predeterminada, cada cinco segundos. Las actualizaciones automáticas no obligan a actualizar la caché; la interfaz de usuario muestra la versión más reciente de los datos de la caché. Puede personalizar la velocidad de actualización utilizada para todas las ventanas asociadas con un publicador si modifica la configuración de éste. También puede deshabilitar las actualizaciones automáticas para un publicador.  
  
-   Las ventanas de detalles que se abren desde el Monitor de replicación no se actualizan automáticamente de manera predeterminada, con excepción de las ventanas relacionadas con las suscripciones de mezcla que se están sincronizando. Si especifica que se actualicen automáticamente las ventanas de detalles, se actualizarán con la misma programación que la ventana principal del Monitor de replicación.  
  
-   Todas las ventanas se pueden actualizar manualmente presionando F5, o haciendo clic con el botón secundario en un nodo del árbol del Monitor de replicación y, después, haciendo clic en **Actualizar**. La actualización manual fuerza una actualización de la caché.  
  
 Para más información, vea [Actualizar datos en el Monitor de replicación](../../../relational-databases/replication/monitor/refresh-data-in-replication-monitor.md).  
  
## <a name="performance-considerations"></a>Consideraciones de rendimiento  
 A pesar de que el Monitor de replicación está diseñado para ejecutarse de forma eficaz, debe tener en cuenta los siguientes aspectos:  
  
-   Si tiene un gran número de publicaciones o suscripciones, configure una programación de actualización automática menos frecuente para la interfaz de usuario.  
  
-   Evite ejecutar simultáneamente varias instancias del Monitor de replicación.  
  
-   Evite registrar un gran número de distribuidores y configurar el Monitor de replicación para que se conecte automáticamente a todos ellos.  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar trabajos de mantenimiento de replicación &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [Supervisar la replicación](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
