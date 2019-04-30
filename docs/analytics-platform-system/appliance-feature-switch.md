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
ms.openlocfilehash: b4fa05bcc33c9a305253563e40bf071338f19461
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63276146"
---
# <a name="appliance-feature-switches"></a>Modificadores de características del dispositivo

El **modificador de característica** página muestra información sobre los conmutadores de característica que se presentan en Analytics Platform System AU7 y versiones posteriores. Utilice esta página de configuración para habilitar o deshabilitar características y la configuración de Analytics Platform System o actualizar.

> [!NOTE]
> Los cambios en los valores de conmutador de característica requieren un reinicio del servicio.

![Cambio de características del dispositivo de DWConfig](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "cambio de características del dispositivo DWConfig")

## <a name="autostatsenabled"></a>AutoStatsEnabled

Controla la característica de estadísticas automática. Este modificador de característica se establece en true de forma predeterminada después de actualizar a AU7. Cualquier base de datos creada después de la actualización heredarán la creación automática y la actualización asincrónica de estadísticas. Para las bases de datos existentes, pueden permitir que los administradores de base de datos automática de estadísticas con [ALTER DATABASE (almacenamiento de datos paralelos)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw). Para obtener más información sobre las estadísticas, consulte [estadísticas](../relational-databases/statistics/statistics.md).

## <a name="maxdopforinsertqueries"></a>MaxDOPForInsertQueries

Permite seleccionar la configuración de maxdop mayor que 1 para las operaciones insert o select. Opciones para esta configuración son 0, 1, 2 y 4, con el valor predeterminado es 1.

## <a name="optimizecommonsubexpressions"></a>OptimizeCommonSubExpressions

Mejora el rendimiento de las consultas mediante la eliminación de movimiento de datos de la subexpresión común en el optimizador de consultas SQL. Puede encontrar una explicación detallada de esta característica [aquí](common-sub-expression-elimination.md).

## <a name="usecatalogqueries"></a>UseCatalogQueries

Uso de los objetos de catálogo para algunas llamadas de metadatos en lugar de usar SMO ha demostrado mejora del rendimiento. Establecido en true de forma predeterminada en CU7.1, este modificador controla ese comportamiento.

## <a name="dmsprocessstopmessagetimeoutinseconds"></a>DmsProcessStopMessageTimeoutInSeconds

Controla el tiempo de espera del servicio de movimiento de datos (DMS) para sincronizar en un sistema ocupado cuando se cancela una consulta que implique el movimiento de datos. Actualizar a AU7 establece este valor en 900 segundos (15 minutos) de forma predeterminada. El intervalo válido es 0 - 3600 segundos.
