---
title: Modificador de características (Analytics Platform System)
description: Muestra información acerca de los modificadores de dos características que se introducen en AU7 de sistema de plataforma de análisis.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e384a252584fed0e7543a7a4000fc9a70f6533e7
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2018
---
#<a name="appliance-feature-switch"></a>Modificador de características del dispositivo
El **característica conmutador** página muestra información acerca de los modificadores de dos características que se introducen en AU7 de sistema de plataforma de análisis. Utilice esta página para actualizar o habilitar o deshabilitar características y configuración de sistema de la plataforma de análisis. Cambiar valores de modificador de características, requiere un reinicio del servicio.

![Modificador de características del dispositivo de DWConig](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig modificador de características de dispositivo") 

##<a name="autostatsenabled-switch"></a>Conmutador AutoStatsEnabled
Controla la característica de estadísticas automáticamente. Esta característica modificador se establece en true de forma predeterminada después de actualizar a AU7. Cualquier base de datos creada después de la actualización heredarán la creación automática y la actualización asincrónica de estadísticas. Para bases de datos existentes, los administradores de base de datos pueden habilitar estadísticas automáticamente con [Modificar base de datos] (/ sql/t-sql/statements/alter-database-parallel-data-warehouse). Para obtener más información sobre las estadísticas, vea [estadísticas](../relational-databases/statistics/statistics.md).

##<a name="dmsprocessstopmessagetimeoutinseconds-switch"></a>Conmutador DmsProcessStopMessageTimeoutInSeconds
Controla el tiempo de espera del servicio de movimiento de datos (DMS) para sincronizar en un sistema ocupado cuando se cancela una consulta que incluye el movimiento de datos. Actualizar a AU7 establece este valor a 900 segundos (15 minutos) de forma predeterminada. El intervalo válido es 0 y 3600 segundos.
