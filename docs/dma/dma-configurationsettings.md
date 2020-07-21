---
title: Configurar las opciones de Data Migration Assistant
description: Obtenga información sobre cómo configurar las opciones de la Data Migration Assistant actualizando los valores del archivo de configuración.
ms.custom: seo-lt-2019
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.openlocfilehash: bc6805426251e87a8db3dcf4ad9da6343ac0ea12
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886002"
---
# <a name="configure-settings-for-data-migration-assistant"></a>Configurar las opciones de Data Migration Assistant

Puede ajustar el comportamiento de Data Migration Assistant estableciendo los valores de configuración en el archivo DMA. exe. config. En este artículo se describen los valores de configuración clave.

Puede encontrar el archivo DMA. exe. config para la aplicación de escritorio Data Migration Assistant y la utilidad de línea de comandos, en las siguientes carpetas de la máquina.

- Aplicación de escritorio

  % ProgramFiles% \\ Microsoft Data Migration Assistant \\ DMA. exe. config

- Utilidad de línea de comandos

  % ProgramFiles% \\ Microsoft Data Migration Assistant \\ dmacmd. exe. config 

Asegúrese de guardar una copia del archivo de configuración original antes de realizar cualquier modificación. Después de realizar los cambios, reinicie Data Migration Assistant para que los nuevos valores de configuración surtan efecto.

## <a name="number-of-databases-to-assess-in-parallel"></a>Número de bases de datos que se van a evaluar en paralelo

Data Migration Assistant evalúa varias bases de datos en paralelo. Durante la evaluación Data Migration Assistant extrae la aplicación de capa de datos (dacpac) para comprender el esquema de la base de datos.Esta operación puede agotar el tiempo de espera si varias bases de datos en el mismo servidor se evalúan en paralelo. 

A partir de Data Migration Assistant v 2.0, puede controlar esto estableciendo el valor de configuración parallelDatabases. El valor predeterminado es 8.

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>Número de bases de datos que se van a migrar en paralelo

Data Migration Assistant migra varias bases de datos en paralelo antes de migrar los inicios de sesión. Durante la migración, Data Migration Assistant realizará una copia de seguridad de la base de datos de origen y, opcionalmente, copiará la copia de seguridad y, a continuación, la restaurará en el servidor de destino. Es posible que se produzcan errores de tiempo de espera cuando se seleccionan varias bases de datos para la migración. 

A partir de Data Migration Assistant v 2.0, si experimenta este problema, puede reducir el valor de configuración parallelDatabases. Puede aumentar el valor para reducir el tiempo total de migración.

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases="8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>Configuración de DacFX

Durante la evaluación, Data Migration Assistant extrae la aplicación de capa de datos (dacpac) para comprender el esquema de la base de datos. Esta operación puede producir un error en los tiempos de espera de las bases de datos extremadamente grandes o si el servidor está bajo carga. A partir de Data Migration v 1.0, puede modificar los siguientes valores de configuración para evitar errores. 

> [!NOTE]
> La &lt; entrada dacfx completa &gt; está comentada de forma predeterminada. Quite los comentarios y, a continuación, modifique el valor según sea necesario.

- commandTimeout

   Este parámetro establece la propiedad IDbCommand. CommandTimeout en *segundos*.(Valor predeterminado = 60)

- databaseLockTimeout

   Este parámetro equivale a establecer el tiempo de [ \_ espera \_ de bloqueo](../t-sql/statements/set-lock-timeout-transact-sql.md) en *milisegundos*.(Valor predeterminado = 5000)

- maxDataReaderDegreeOfParallelism

  Este parámetro establece el número de conexiones de grupo de conexiones SQL que se van a utilizar.(Valor predeterminado = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```

## <a name="stretch-database-recommendation-threshold"></a>Stretch Database: umbral de recomendación

Con [SQL Server Stretch Database](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database), puede ampliar dinámicamente los datos transaccionales activos e inactivos de Microsoft SQL Server 2016 a Azure. Stretch Database se dirige a las bases de datos transaccionales con grandes cantidades de datos inactivos. En la recomendación de Stretch Database, en la recomendación de características de almacenamiento, primero se identifican las tablas que considera que se beneficiarán de esta característica y, a continuación, se identifican los cambios que se deben realizar para habilitar la tabla para esta característica.

A partir de Data Migration Assistant v 2.0, puede controlar este umbral para que una tabla pueda optar a la característica de Stretch Database mediante el valor de configuración recommendedNumberOfRows. El valor predeterminado es 100.000 filas. Si desea analizar las capacidades de stretch para tablas incluso más pequeñas, disminuya el valor en consecuencia.

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>Tiempo de espera de conexión SQL

Puede controlar el [tiempo de espera de conexión de SQL](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx) para las instancias de origen y de destino durante la ejecución de una evaluación o migración, estableciendo el valor de tiempo de espera de la conexión en un número de segundos especificado. El valor predeterminado es 15 segundos.

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```

## <a name="ignore-error-codes"></a>Omitir códigos de error

Cada regla tiene un código de error en su título. Si no necesita reglas y desea omitirlas, use la propiedad ignoreErrorCodes. Puede especificar para omitir un solo error o varios errores. Para omitir varios errores, use un punto y coma, por ejemplo, ignoreErrorCodes = "46010; 71501". El valor predeterminado es 71501, que está asociado a las referencias no resueltas identificadas cuando un objeto hace referencia a objetos del sistema como procedimientos, vistas, etc.

```
<workflowSettings>

<assessment parallelDatabases="8" ignoreErrorCodes="71501" />

</workflowSettings>
```

## <a name="see-also"></a>Consulte también

[Descargar Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)
