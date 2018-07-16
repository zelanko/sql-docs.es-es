---
title: Configuración del publicador | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publishersettings.f1
helpviewer_keywords:
- Publisher Settings dialog box
ms.assetid: 4fb70427-082d-4179-82a1-34b235accc43
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: abcedc479df197258b9ad836a3dd62430fb1c69b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37301845"
---
# <a name="publisher-settings"></a>Configuración del publicador
  El cuadro de diálogo **Configuración del publicador** permite cambiar la configuración de los publicadores que se han agregado al panel izquierdo del Monitor de replicación.  
  
## <a name="options"></a>Opciones  
 **Conexión del publicador**  
 Haga clic para abrir el cuadro de diálogo **Conectar al servidor** , que permite ver y cambiar las propiedades de la conexión y las credenciales que utiliza el Monitor de replicación para conectarse a un publicador.  
  
 **Conexión del distribuidor**  
 Solo se muestra si el publicador utiliza un distribuidor remoto. Haga clic para abrir el cuadro de diálogo **Conectar al servidor** , que permite ver y cambiar las propiedades de la conexión y las credenciales que utiliza el Monitor de replicación para conectarse a un distribuidor remoto.  
  
 **Conectar automáticamente cuando se inicia el Monitor de replicación**  
 Active esta casilla para permitir que el Monitor de replicación se conecte automáticamente con el distribuidor y recupere información de estado para el publicador seleccionado en la cuadrícula de la parte superior del cuadro de diálogo. Si esta casilla está desactivada, debe conectarse manualmente después de iniciar el Monitor de replicación: haga clic con el botón secundario en el publicador en el panel izquierdo del Monitor de replicación y, a continuación, haga clic en **Conectar**.  
  
 **Actualizar automáticamente el estado de este publicador y sus publicaciones**  
 Active esta casilla para permitir que el Monitor de replicación actualice automáticamente el estado del publicador seleccionado en la cuadrícula de la parte superior del cuadro de diálogo. Si esta opción está activada, el Monitor de replicación sondea el distribuidor buscando información de estado en el publicador y sus publicaciones. El intervalo de sondeo se establece mediante la opción **Frecuencia de actualización** . Para obtener más información sobre la actualización en el Monitor de replicación, vea [Almacenamiento en caché, actualización y rendimiento del Monitor de replicación](monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Frecuencia de actualización**  
 Escriba un valor (en segundos) para especificar la frecuencia con la que el Monitor de replicación debe sondear el distribuidor en búsqueda de información de estado. Los valores más bajos producen un sondeo más frecuente, lo que puede afectar al rendimiento del distribuidor si se supervisa un gran número de publicadores. Se recomienda probar el sistema para determinar un valor adecuado. El valor **Frecuencia de actualización** también se utiliza si se selecciona **Actualizar automáticamente** en cualquiera de las ventanas de detalle del Monitor de replicación.  
  
 **Mostrar estos publicadores en el siguiente grupo**  
 Seleccione un grupo de publicadores de la lista. El publicador se muestra en este grupo en el panel izquierdo. Los grupos proporcionan una forma de organizar los publicadores y no afectan al funcionamiento de la replicación.  
  
 **Nuevo grupo**  
 Haga clic aquí para crear un nuevo grupo de publicadores. Un grupo de publicadores proporciona una forma cómoda de organizar publicadores en el Monitor de replicación. Los grupos no afectan a la replicación de datos ni a la relación entre los servidores de una topología de replicación.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar el Monitor de replicación](monitor/start-the-replication-monitor.md)   
 [Supervisar la replicación](monitoring-replication.md)  
  
  
