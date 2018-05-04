---
title: Opciones de configuración (SQL Server datos Migration Assistant) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: b0cc5dc0b34e740034b6e0852163c70c9de9b09b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="configuration-settings-for-data-migration-assistant"></a>Opciones de configuración para el Asistente de migración de datos

Puede ajustar cierto comportamiento del Asistente para migración de datos con valores de configuración en el archivo dma.exe.config. Este artículo describen los valores de configuración de la clave.

Puede encontrar el archivo dma.exe.config para la aplicación de escritorio de Asistente de migración de datos y la utilidad de línea de comandos, en las siguientes carpetas en su equipo.

- Aplicación de escritorio

  % ProgramFiles %\\Asistente de migración de datos de Microsoft\\dma.exe.config

- Utilidad de línea de comandos

  % ProgramFiles %\\Asistente de migración de datos de Microsoft\\dmacmd.exe.config 

No olvide guardar una copia del archivo de configuración original antes de realizar cualquier modificación. Después de realizar cambios, reinicie datos Migration Assistant para los nuevos valores de configuración para que surta efecto.

## <a name="number-of-databases-to-assess-in-parallel"></a>Número de bases de datos para evaluar en paralelo

Asistente para migración de datos evalúa varias bases de datos en paralelo. Durante la evaluación de Asistente de migración de datos extrae la aplicación de capa de datos (dacpac) para conocer el esquema de base de datos. Esta operación puede tiempo de espera si varias bases de datos en el mismo servidor se evalúan en paralelo. 

A partir de datos Migration Assistant v2.0, puede controlar esto estableciendo el parallelDatabases del valor de configuración. Valor predeterminado es 8.

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>Número de bases de datos para la migración en paralelo

Asistente para migración de datos migra varias bases de datos en paralelo, antes de migrar los inicios de sesión. Durante la migración, el Asistente de migración de datos se realice una copia de seguridad de la base de datos de origen, si lo desea copiar la copia de seguridad y, a continuación, restaurarlo en el servidor de destino. Puede encontrar errores de tiempo de espera cuando se seleccionan varias bases de datos para la migración. 

A partir de datos Migration Assistant v2.0, si experimenta este problema puede reducir el valor de configuración parallelDatabases. Puede aumentar el valor para reducir el tiempo general de migración.

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases=”8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>Configuración de DacFX

Durante la evaluación, el Asistente de migración de datos extrae la aplicación de capa de datos (dacpac) para conocer el esquema de base de datos. Esta operación puede producir un error con tiempos de espera de bases de datos muy grandes, o si el servidor está bajo carga. A partir de v1.0 de migración de datos, puede modificar los siguientes valores de configuración para evitar errores. 

> [!NOTE]
> Toda la &lt;dacfx&gt; entrada se hace referencia de forma predeterminada. Quite los comentarios y, a continuación, modifique el valor según sea necesario.

- CommandTimeout

   Esto establece la propiedad IDbCommand.CommandTimeout *segundos*. (Predeterminado = 60)

- databaseLockTimeout

   Esto equivale a [bloqueo establecido\_tiempo de espera de tiempo de espera\_período ](../t-sql/statements/set-lock-timeout-transact-sql.md) en *milisegundos*. (Predeterminado = 5000)

- maxDataReaderDegreeOfParallelism

   Número de conexiones de grupo de conexión de SQL para usar. (Predeterminado = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```


## <a name="stretch-database-recommendation-threshold"></a>Ajuste de base de datos: Umbral de recomendación

Con [base de datos de SQL Server Stretch](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database), puede ajustar dinámicamente datos semiactivos e inactivos transaccionales de Microsoft SQL Server 2016 en Azure. Ajustar la base de datos destinos bases de datos transaccionales con grandes cantidades de datos inactivos. En primer lugar, la recomendación de Stretch Database, en la recomendación de la característica de almacenamiento, identifica las tablas que cree que puede beneficiarse de esta característica y, a continuación, identifica los cambios que deben realizarse para habilitar la tabla para esta característica.

A partir de datos Migration Assistant v2.0, puede controlar este umbral para una tabla para calificar para la característica Stretch Database con el valor de configuración recommendedNumberOfRows. Valor predeterminado es 100.000 filas. Si desea analizar las capacidades de stretch para tablas incluso más pequeñas, disminuya el valor en consecuencia.

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>Tiempo de espera de conexión de SQL

Puede controlar la [tiempo de espera de conexión de SQL](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx) para instancias de origen y de destino mientras se ejecuta una evaluación o la migración, estableciendo el valor de tiempo de espera de conexión a un número especificado de segundos. El valor predeterminado es 15 segundos.

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```


## <a name="see-also"></a>Vea también

[Descarga de Asistente de migración de datos](https://www.microsoft.com/download/details.aspx?id=53595)
