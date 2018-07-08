---
title: Configurar opciones para Data Migration Assistant (SQL Server) | Microsoft Docs
description: Aprenda a configurar la configuración de Data Migration Assistant actualizando los valores del archivo de configuración
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
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
ms.openlocfilehash: a8ab80d5e83ef5f7650f87f8c4618466eb3dee74
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/04/2018
ms.locfileid: "37783996"
---
# <a name="configure-settings-for-data-migration-assistant"></a>Configurar opciones para Data Migration Assistant

Puede ajustar estableciendo los valores de configuración en el archivo dma.exe.config ciertos comportamientos de Data Migration Assistant. En este artículo se describe los valores de configuración de la clave.

Puede encontrar el archivo dma.exe.config para la aplicación de escritorio Data Migration Assistant y la utilidad de línea de comandos, en las siguientes carpetas en el equipo.

- Aplicación de escritorio

  % ProgramFiles %\\Microsoft Data Migration Assistant\\dma.exe.config

- Utilidad de línea de comandos

  % ProgramFiles %\\Microsoft Data Migration Assistant\\dmacmd.exe.config 

No olvide guardar una copia del archivo de configuración original antes de realizar modificaciones. Después de realizar cambios, reinicie Data Migration Assistant para los nuevos valores de configuración para que surta efecto.

## <a name="number-of-databases-to-assess-in-parallel"></a>Número de bases de datos para evaluar en paralelo

Data Migration Assistant evalúa varias bases de datos en paralelo. Durante la evaluación de Data Migration Assistant extrae la aplicación de capa de datos (dacpac) para comprender el esquema de base de datos. Esta operación puede tiempo de espera si varias bases de datos en el mismo servidor que se evalúan en paralelo. 

Comenzando con la versión 2.0 de Data Migration Assistant, puede controlar esto estableciendo el parallelDatabases del valor de configuración. Valor predeterminado es 8.

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>Número de bases de datos para la migración en paralelo

Data Migration Assistant migra varias bases de datos en paralelo, antes de migrar los inicios de sesión. Durante la migración, Data Migration Assistant se realice una copia de seguridad de la base de datos de origen, si lo desea copiar la copia de seguridad y, a continuación, restaurarla en el servidor de destino. Cuando se seleccionan varias bases de datos para la migración, podrían producirse errores de tiempo de espera. 

Comenzando con la versión 2.0 de Data Migration Assistant, si experimenta este problema puede reducir el valor de configuración parallelDatabases. Puede aumentar el valor para reducir el tiempo de migración general.

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases=”8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>Configuración de DacFX

Durante la valoración, Data Migration Assistant extrae la aplicación de capa de datos (dacpac) para comprender el esquema de base de datos. Esta operación puede producir un error con tiempos de espera para las bases de datos extremadamente grandes, o si el servidor está bajo carga. Comenzando con la versión 1.0 de la migración de datos, puede modificar los valores de configuración siguiente para evitar errores. 

> [!NOTE]
> Toda la &lt;dacfx&gt; entrada está marcada como predeterminada. Quite los comentarios y, a continuación, modifique el valor según sea necesario.

- commandTimeout

   Esto establece la propiedad IDbCommand.CommandTimeout *segundos*. (Predeterminado = 60)

- databaseLockTimeout

   Esto es equivalente a [establecer bloqueo\_tiempo de espera de tiempo de espera\_período ](../t-sql/statements/set-lock-timeout-transact-sql.md) en *milisegundos*. (Predeterminado = 5000)

- maxDataReaderDegreeOfParallelism

   Número de conexiones de grupo de conexión SQL a usar. (Predeterminado = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```


## <a name="stretch-database-recommendation-threshold"></a>Stretch Database: Umbral de recomendación

Con [SQL Server Stretch Database](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database), puede ampliar dinámicamente los datos activos e inactivos transaccionales de Microsoft SQL Server 2016 en Azure. Stretch Database destinos bases de datos transaccionales con grandes cantidades de datos inactivos. La recomendación de Stretch Database, en la recomendación de característica de almacenamiento, primero identifica las tablas que piensa que se beneficiará de esta característica y, a continuación, identifica los cambios que deben realizarse para permitir que la tabla para esta característica.

A partir de la versión 2.0 de Data Migration Assistant, puede controlar este umbral para una tabla calificar para la característica Stretch Database con el valor de configuración recommendedNumberOfRows. Valor predeterminado es 100.000 filas. Si desea analizar las capacidades de stretch para tablas incluso más pequeñas, disminuya el valor en consecuencia.

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>Tiempo de espera de conexión de SQL

Puede controlar la [tiempo de espera de conexión SQL](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx) para las instancias de origen y de destino mientras se ejecuta una evaluación o la migración, estableciendo el valor de tiempo de espera de conexión a un número especificado de segundos. El valor predeterminado es 15 segundos.

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```


## <a name="see-also"></a>Vea también

[Descarga de Ayudante de migración de datos](https://www.microsoft.com/download/details.aspx?id=53595)
