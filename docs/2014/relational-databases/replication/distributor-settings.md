---
title: Cuadro de diálogo de configuración del distribuidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.DistributorSettings.f1
helpviewer_keywords:
- Distributor Settings dialog box
ms.assetid: 8276a521-bdd1-4783-bdb6-7ab43499c0ca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d910cdb4baf1d65f67ece14c20a1f384af2a843b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721350"
---
# <a name="sql-server-replication-distributor-settings-dialog-box"></a>Cuadro de diálogo de configuración del distribuidor de replicación de SQL Server
  El cuadro de diálogo **Configuración del distribuidor** le permite cambiar la configuración de los distribuidores que se han agregado al panel izquierdo del Monitor de replicación.  
  
## <a name="options"></a>Opciones  
 **Conectar automáticamente cuando se inicia el Monitor de replicación**  
 Seleccione esta opción para permitir que el Monitor de replicación se conecte al distribuidor y recupere información de estado.  
  
 **Conexión**  
 Haga clic aquí para mostrar el cuadro de diálogo **Conectar con el servidor** . Esto le permite ver y cambiar las propiedades de conexión y las credenciales que el Monitor de replicación utiliza para conectarse al distribuidor.  
  
 **Actualizar automáticamente el estado de este distribuidor y sus publicaciones**  
 Seleccione esta opción para permitir que el Monitor de replicación actualice automáticamente el estado del distribuidor. Si esta opción está seleccionada, el Monitor de replicación sondea al distribuidor para obtener información de estado basada en el intervalo de sondeo establecido por la opción **Frecuencia de actualización** . Para obtener más información sobre la actualización en el Monitor de replicación, vea [Caching, Refresh, and Replication Monitor Performance](monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Frecuencia de actualización**  
 Escriba un valor (en segundos) para especificar la frecuencia con la que el Monitor de replicación debe sondear el distribuidor en búsqueda de información de estado. Los valores menores producen sondeos más frecuentes. Esto puede afectar al rendimiento del distribuidor si está supervisando muchos publicadores. Se recomienda probar el sistema para determinar un valor adecuado. El valor **Frecuencia de actualización** también se utiliza si se selecciona **Actualizar automáticamente** en cualquiera de las ventanas de detalle del Monitor de replicación.  
  
 **Mostrar todos los publicadores de este distribuidor en el siguiente grupo**  
 Seleccione un grupo de publicadores de la lista. El publicador se muestra en este grupo en el panel izquierdo. Los grupos proporcionan una forma de organizar los publicadores y no afectan al funcionamiento de la replicación.  
  
 **Nuevo grupo**  
 Haga clic aquí para crear un nuevo grupo de publicadores. Un grupo de publicadores proporciona una forma cómoda de organizar publicadores dentro del Monitor de replicación. Los grupos no afectan a la replicación de datos ni a la relación entre los servidores de una topología de replicación.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar el Monitor de replicación](monitor/start-the-replication-monitor.md)   
 [Supervisar la replicación](monitoring-replication.md)  
  
  
