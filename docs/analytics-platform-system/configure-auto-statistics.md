---
title: Estadísticas automáticas (Analytics Platform System)
description: Describe la característica de estadísticas automática introducida en Analytics Platform System AU7.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: e48d40d78c25431fd6e5592dacfa410723b31f82
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057068"
---
# <a name="configure-auto-statistics"></a>Configuración automática de estadísticas

Obtenga información sobre cómo configurar el almacenamiento de datos paralelos para utilizar estadísticas automáticamente para crear y actualizar estadísticas automáticamente.  Utilizar esta capacidad para mejorar los planes de consulta y, por lo tanto, mejorar el rendimiento de las consultas.

**Se aplica a:** Puntos de acceso (a partir de 2016 AU7)

## <a name="what-are-statistics"></a>¿Cuáles son las estadísticas?
Las estadísticas de optimización de la consulta son objetos que contienen información estadística sobre la distribución de valores en una o varias columnas de una tabla. El optimizador de consultas utiliza estas estadísticas para estimar la cardinalidad o tienen como resultado el número de filas de la consulta. Estas estimaciones de cardinalidad habilitar el optimizador de consultas crear un plan de consulta de alta calidad. Por ejemplo, los puntos de acceso, los usos del optimizador de consultas MPP estimaciones de cardinalidad para elegir en orden aleatorio o replicar el menor de dos tablas que se utilizan en una cláusula join y hacerlo mejoran el rendimiento de la consulta.  Para obtener más información, consulte [estadísticas](../relational-databases/statistics/statistics.md) y [DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)

## <a name="what-are-auto-statistics"></a>¿Cuáles son las estadísticas automáticamente?
Estadísticas automáticamente son las estadísticas que el optimizador de consultas crea y se actualiza automáticamente para mejorar el plan de consulta. Las estadísticas pueden quedar desfasadas después las cargas, insertan, actualizan y eliminan las operaciones. Sin estadísticas automáticamente, deberá realizar su propio análisis para entender qué columnas necesitan estadísticas y cuando las estadísticas deben actualizarse.

Automática de estadísticas incluye los tres valores siguientes: 

### <a name="autocreatestatistics"></a>AUTO_CREATE_STATISTICS
Cuando está activada la opción automática de creación de estadísticas, AUTO_CREATE_STATISTICS, el optimizador de consultas crea las estadísticas en columnas individuales en el predicado de consulta, según sea necesario, para mejorar las estimaciones de cardinalidad del plan de consulta. Estas estadísticas de columna única se crean en las columnas que aún no tienen un histograma en un objeto de estadísticas existente.

### <a name="autoupdatestatistics"></a>AUTO_UPDATE_STATISTICS 
Cuando está activada la opción automática de actualización de estadísticas, AUTO_UPDATE_STATISTICS, el optimizador de consultas determina cuándo las estadísticas pueden estar desfasadas y las actualiza cuando son usadas por una consulta. Las estadísticas se vuelven obsoletas después de que las operaciones de inserción, actualización, eliminación o combinación cambien la distribución de los datos en la tabla o la vista indexada. El optimizador de consultas determina cuándo han podido quedar obsoletas las estadísticas contando el número de modificaciones de datos desde la actualización más reciente de las estadísticas, comparando el número de modificaciones con respecto a un umbral. El umbral se basa en el número de filas de la tabla o la vista indizada.

### <a name="autoupdatestatisticsasync"></a>AUTO_UPDATE_STATISTICS_ASYNC
La opción de actualización asincrónica de estadísticas AUTO_UPDATE_STATISTICS_ASYNC determina si el Optimizador de consultas utiliza actualizaciones sincrónicas o asincrónicas de las estadísticas. Para los puntos de acceso, la opción de actualización de estadísticas asincrónica es ON de forma predeterminada y el optimizador de consultas actualiza las estadísticas de forma asincrónica. La opción AUTO_UPDATE_STATISTICS_ASYNC se aplica a los objetos de estadística creados para índices y columnas únicas de los predicados de consulta, así como a las estadísticas creadas con la instrucción CREATE STATISTICS.

## <a name="configuration-settings-for-system-administrators"></a>Opciones de configuración para los administradores del sistema
Después de actualizar a AU7 APS, automática de estadísticas está habilitada de forma predeterminada. El administrador del sistema puede habilitar o deshabilitar estadísticas automáticamente con el [modificador de característica](appliance-feature-switch.md) opción en el Administrador de configuración de dispositivo.  Una vez habilitada, los usuarios pueden cambiar la configuración de las estadísticas por base de datos.
Cambiar los valores de conmutador de característica requiere un reinicio del servicio en puntos de acceso.

## <a name="change-auto-statistics-settings-on-a-database"></a>Cambiar la configuración de las estadísticas automáticamente en una base de datos
Cuando las estadísticas automáticamente está habilitada el administrador del sistema, puede usar [ALTER DATABASE (almacenamiento de datos paralelos)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) para cambiar la configuración de las estadísticas en una base de datos. Si el modificador de característica de estadísticas automática está habilitado por el administrador del sistema, las bases de datos creadas después de actualizar a AU7 tendrá automática de estadísticas habilitada. Todas las bases de datos que existían antes de la actualización a AU7 tienen estadísticas automáticamente deshabilitadas. El ejemplo siguiente habilita las estadísticas automáticamente en el myPDW de base de datos existente.

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
Opción AUTO_UPDATE STATISTICS_ASYNC sólo funciona si AUTO_UPDATE_STATISTICS es ON.  Por lo tanto, no se actualizan las estadísticas cuando AUTO_UPDATE_STATISTICS es OFF y AUTO_UPDATE_STATISTICS_ASYNC es ON. 

### <a name="error-messages"></a>Mensajes de error
Podría recibir el mensaje de error "no se admite esta opción en PDW".  Este error se produce cuando el administrador del sistema no ha habilitado estadísticas automáticamente y se intenta establecer cualquiera del automáticamente las opciones de estadísticas en ALTER DATABASE. 

### <a name="limitations-and-restrictions"></a>Limitaciones y restricciones
Estadística automática no funciona en las tablas externas. 

### <a name="check-the-current-values"></a>Compruebe los valores actuales
La consulta siguiente devuelve los valores actuales de la configuración de las estadísticas automáticas para todas las bases de datos.

```sql
SELECT NAME
    , IS_AUTO_CREATE_STATS_ON 
    , IS_AUTO_UPDATE_STATS_ON
    , IS_AUTO_UPDATE_STATS_ASYNC_ON
FROM
    sys.databases;
```

Un valor devuelto de 1 significa que en la configuración se encuentra en y 0 significa que la opción está desactivada. 

## <a name="next-steps"></a>Pasos siguientes
Para ver cómo funcionan las consultas, consulte [supervisión de consultas activas](monitoring-active-queries.md)
