---
title: Modificador de característica (Analytics Platform System)
description: Muestra información acerca de los modificadores de dos características que se introducen en Analytics Platform System AU7.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: d9657b1433b0647d7165cb427da6333c0a325583
ms.sourcegitcommit: 0cda14b1151d9bce1253d96dea038c038484f07a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/08/2018
ms.locfileid: "39400928"
---
#<a name="appliance-feature-switch"></a>Cambio de características del dispositivo
El **modificador de característica** página muestra información sobre los modificadores de dos características que se introducen en Analytics Platform System 2016-AU7. Utilice esta página para habilitar o deshabilitar características y la configuración de Analytics Platform System o actualizar. Cambiar los valores de conmutador de característica requiere un reinicio del servicio.

![Cambio de características del dispositivo DWConig](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig cambio de características de dispositivo") 

##<a name="autostatsenabled-switch"></a>Conmutador AutoStatsEnabled
Controla la característica de estadísticas automática. Este modificador de característica se establece en true de forma predeterminada después de actualizar a AU7. Cualquier base de datos creada después de la actualización heredarán la creación automática y la actualización asincrónica de estadísticas. Para las bases de datos existentes, pueden permitir que los administradores de base de datos automática de estadísticas con [ALTER DATABASE (almacenamiento de datos paralelos)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw). Para obtener más información sobre las estadísticas, consulte [estadísticas](../relational-databases/statistics/statistics.md).

##<a name="dmsprocessstopmessagetimeoutinseconds-switch"></a>Conmutador DmsProcessStopMessageTimeoutInSeconds
Controla el tiempo de espera del servicio de movimiento de datos (DMS) para sincronizar en un sistema ocupado cuando se cancela una consulta que implique el movimiento de datos. Actualizar a AU7 establece este valor en 900 segundos (15 minutos) de forma predeterminada. El intervalo válido es 0 y 3600 segundos.
