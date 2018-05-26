---
title: Estadísticas automáticas (Analytics Platform System)
description: Describe la característica de estadísticas de automática integrada en AU7 de sistema de plataforma de análisis.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1c0f4623adad35ab874330b42aa54f6e1b91d961
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2018
---
# <a name="configure-auto-statistics"></a>Configurar estadísticas automáticamente

Obtenga información acerca de cómo configurar el almacenamiento de datos paralelos para utilizar estadísticas automáticamente para crear y actualizar estadísticas automáticamente.  Utilizar esta capacidad para mejorar los planes de consulta y, por lo tanto, mejorar el rendimiento de las consultas.

**Se aplica a:** APS (a partir de AU7)

## <a name="what-are-statistics"></a>¿Cuáles son las estadísticas?
Las estadísticas de optimización de la consulta son objetos que contienen información estadística sobre la distribución de valores en una o varias columnas de una tabla. El optimizador de consultas utiliza estas estadísticas para estimar la cardinalidad o provocar el número de filas de la consulta. Estas estimaciones de cardinalidad habilitar el optimizador de consultas crear un plan de consulta de alta calidad. Por ejemplo, los puntos de acceso, los usos del optimizador de consultas MPP estimaciones de cardinalidad para elegir en orden aleatorio o replicar el menor de dos tablas que se utilizan en una cláusula de combinación y si lo hace, mejoran el rendimiento de consulta.  Para obtener más información, consulte [estadísticas](../relational-databases/statistics/statistics.md) y [DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)

## <a name="what-are-auto-statistics"></a>¿Qué estadísticas automáticamente?
Estadísticas automáticamente son las estadísticas que el optimizador de consultas crea y se actualiza automáticamente para mejorar el plan de consulta. Las estadísticas pueden quedarse obsoletas después de la carga, insertan, actualizan y elimina las operaciones. Sin estadísticas automáticamente, debe realizar su propio análisis para comprender qué columnas necesitan estadísticas y cuando las estadísticas deben actualizarse.

Estadísticas automáticamente incluyen las siguientes tres configuraciones: 

### <a name="autocreatestatistics"></a>AUTO_CREATE_STATISTICS
Cuando el automático crear estadísticas, AUTO_CREATE_STATISTICS es ON, el optimizador de consultas crea las estadísticas en columnas individuales en el predicado de consulta, según sea necesario, para mejorar las estimaciones de cardinalidad para el plan de consulta. Estas estadísticas de columna única se crean en las columnas que aún no tienen un histograma en un objeto de estadísticas existente.

### <a name="autoupdatestatistics"></a>AUTO_UPDATE_STATISTICS 
Cuando está activada la opción automática de actualización de estadísticas, AUTO_UPDATE_STATISTICS, el optimizador de consultas determina cuándo las estadísticas pueden estar desfasadas y las actualiza cuando son usadas por una consulta. Las estadísticas que se vuelven obsoletas después de las operaciones inserción, update, eliminarán o combinarán cambian la distribución de datos en la tabla o vista indizan. El optimizador de consultas determina cuándo han podido quedar obsoletas las estadísticas contando el número de modificaciones de datos desde la actualización más reciente de las estadísticas, comparando el número de modificaciones con respecto a un umbral. El umbral se basa en el número de filas de la tabla o la vista indizada.

### <a name="autoupdatestatisticsasync"></a>AUTO_UPDATE_STATISTICS_ASYNC
La opción de actualización asincrónica de estadísticas AUTO_UPDATE_STATISTICS_ASYNC determina si el Optimizador de consultas utiliza actualizaciones sincrónicas o asincrónicas de las estadísticas. Para puntos de acceso, la opción de actualización de estadísticas asincrónicas es ON de forma predeterminada y el optimizador de consultas actualiza las estadísticas de forma asincrónica. La opción AUTO_UPDATE_STATISTICS_ASYNC se aplica a los objetos de estadísticas creados para índices y columnas únicas de predicados de consulta y las estadísticas creadas con la instrucción CREATE STATISTICS.

## <a name="configuration-settings-for-system-administrators"></a>Valores de configuración para los administradores del sistema
Después de actualizar a AU7 de APS, automática de estadísticas está habilitada de forma predeterminada. El administrador del sistema puede habilitar o deshabilitar automática de las estadísticas con la [característica conmutador](appliance-feature-switch.md) opción en el Administrador de configuración de dispositivo.  Una vez habilitada, los usuarios pueden cambiar la configuración de estadísticas de cada base de datos.
Cambiar los valores de modificador de función requiere un reinicio del servicio en puntos de acceso.

## <a name="change-auto-statistics-settings-on-a-database"></a>Cambiar la configuración de las estadísticas automáticamente en una base de datos
Cuando se habilita estadísticas automáticamente por el administrador del sistema, puede usar [ALTER DATABASE (almacenamiento de datos paralelos)](/sql/t-sql/statements/alter-database-parallel-data-warehouse) para cambiar la configuración de las estadísticas en una base de datos. Si está habilitado el modificador de características de las estadísticas automáticamente por el administrador del sistema, las bases de datos creadas después de actualizar a AU7 tendrá estadísticas automáticamente habilitadas. Todas las bases de datos que existían antes de la actualización a AU7 tienen estadísticas automáticamente deshabilitadas. En el ejemplo siguiente se habilita estadísticas automáticamente en el myPDW de base de datos existente.

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
Opción AUTO_UPDATE STATISTICS_ASYNC sólo funciona si AUTO_UPDATE_STATISTICS es ON.  Por lo tanto, las estadísticas no se actualizan cuando AUTO_UPDATE_STATISTICS es OFF y AUTO_UPDATE_STATISTICS_ASYNC es ON. 

### <a name="error-messages"></a>Mensajes de error
Podría recibir el mensaje de error "no se admite esta opción en PDW".  Este error se produce cuando el administrador del sistema no ha habilitado el estadísticas automáticamente y se intenta establecer cualquiera de la automáticamente opciones de estadísticas en ALTER DATABASE. 

### <a name="limitations-and-restrictions"></a>Limitaciones y restricciones
Estadísticas automáticamente no funcionan con las tablas externas. 

### <a name="check-the-current-values"></a>Compruebe los valores actuales
La siguiente consulta devuelve los valores actuales de la configuración de estadísticas automáticas para todas las bases de datos.

```sql
SELECT NAME
    , IS_AUTO_CREATE_STATS_ON 
    , IS_AUTO_UPDATE_STATS_ON
    , IS_AUTO_UPDATE_STATS_ASYNC_ON
FROM
    sys.databases;
```

Un valor devuelto de 1 significa que la configuración se encuentra en y 0 significa que la configuración está desactivada. 

## <a name="next-steps"></a>Pasos siguientes
Para ver el rendimiento de las consultas, vea [supervisión consultas activas](monitoring-active-queries.md)
