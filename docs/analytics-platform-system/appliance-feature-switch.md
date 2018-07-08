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
ms.openlocfilehash: b06c715549cd1c9cf464a13b03790764ebf40b97
ms.sourcegitcommit: 3e5f1545e5c6c92fa32e116ee3bff1018ca946a2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2018
ms.locfileid: "37107183"
---
#<a name="appliance-feature-switch"></a>Cambio de características del dispositivo
El **modificador de característica** página muestra información sobre los modificadores de dos características que se introducen en Analytics Platform System 2016-AU7. Utilice esta página para habilitar o deshabilitar características y la configuración de Analytics Platform System o actualizar. Cambiar los valores de conmutador de característica requiere un reinicio del servicio.

![Cambio de características del dispositivo DWConig](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig cambio de características de dispositivo") 

##<a name="autostatsenabled-switch"></a>Conmutador AutoStatsEnabled
Controla la característica de estadísticas automática. Este modificador de característica se establece en true de forma predeterminada después de actualizar a AU7. Cualquier base de datos creada después de la actualización heredarán la creación automática y la actualización asincrónica de estadísticas. Para las bases de datos existentes, pueden permitir que los administradores de base de datos automática de estadísticas con [alter database] (/ sql/t-sql/statements/alter-database-parallel-data-warehouse). Para obtener más información sobre las estadísticas, consulte [estadísticas](../relational-databases/statistics/statistics.md).

##<a name="dmsprocessstopmessagetimeoutinseconds-switch"></a>Conmutador DmsProcessStopMessageTimeoutInSeconds
Controla el tiempo de espera del servicio de movimiento de datos (DMS) para sincronizar en un sistema ocupado cuando se cancela una consulta que implique el movimiento de datos. Actualizar a AU7 establece este valor en 900 segundos (15 minutos) de forma predeterminada. El intervalo válido es 0 y 3600 segundos.
