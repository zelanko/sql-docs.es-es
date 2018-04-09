---
title: WideWorldImporters generar datos - base de datos de ejemplo SQL | Documentos de Microsoft
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: samples
ms.technology:
- " database-engine "
ms.topic: article
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: d99cdfacbe08cd3b81fb46bb61b49cab290780f4
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2018
---
# <a name="wideworldimporters-data-generation"></a>Generación de datos WideWorldImporters
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Las versiones publicadas de las bases de datos WideWorldImporters y WideWorldImportersDW contiene los datos a partir del 1 de enero de 2013, hasta el día en que se generaron estas bases de datos.

Al utilizar las bases de datos de ejemplo, puede resultar beneficioso incluir datos de ejemplo más recientes.

## <a name="data-generation-in-wideworldimporters"></a>Generación de datos en WideWorldImporters

Para generar datos de ejemplo hasta la fecha actual, siga estos pasos:

1. Si aún no lo ha hecho, instale una versión limpia de la base de datos WideWorldImporters. Para obtener instrucciones de instalación, **WideWorldImporters instalación y configuración**.
2. Ejecute la instrucción siguiente en la base de datos:

```
    EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
        @AverageNumberOfCustomerOrdersPerDay = 60,
        @SaturdayPercentageOfNormalWorkDay = 50,
        @SundayPercentageOfNormalWorkDay = 0,
        @IsSilentMode = 1,
        @AreDatesPrinted = 1;
```

Esta instrucción agrega datos de compra y de ventas de ejemplo en la base de datos, hasta la fecha actual. Genera el progreso de los datos de generación por días. Puede tardar unos 10 minutos para cada año que necesita que los datos. Hay algunas diferencias en los datos generados entre ejecuciones, dado que no hay un factor aleatorio en la generación de datos.

Para aumentar o disminuir la cantidad de datos generados en términos de pedidos por día, cambie el valor para el parámetro `@AverageNumberOfCustomerOrdersPerDay`. Los parámetros `@SaturdayPercentageOfNormalWorkDay` y `@SundayPercentageOfNormalWorkDay` se usan para determinar el volumen de pedidos para los días de la semana.

## <a name="importing-generated-data-in-wideworldimportersdw"></a>Importación de datos generados en WideWorldImportersDW

Para importar datos de ejemplo hasta la fecha actual en la base de datos OLAP WideWorldImportersDW, siga estos pasos:

1. Ejecutar la lógica de generación de datos en la base de datos WideWorldImporters OLTP, siguiendo los pasos anteriores.
2. Si aún no lo ha hecho, instale una versión limpia de la base de datos de WideWorldImportersDW. Para obtener instrucciones de instalación, **WideWorldImporters instalación y configuración**.
3. Reinicializar la base de datos OLAP mediante la ejecución de la siguiente instrucción en la base de datos:

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. Ejecutar el paquete SSIS **ETL.ispac diaria** para importar los datos en la base de datos OLAP. Para obtener instrucciones sobre cómo ejecutar el trabajo ETL, consulte **flujo de trabajo de ETL WideWorldImporters**.

## <a name="generating-data-in-wideworldimportersdw-for-performance-testing"></a>Generar datos en WideWorldImportersDW para pruebas de rendimiento

WideWorldImportersDW tiene la capacidad de aumentar el tamaño de los datos, con el fin de pruebas de rendimiento, por ejemplo con el almacén de columnas agrupado arbitrariamente.

Uno de los desafíos es mantener el tamaño de la descarga lo suficientemente pequeño como para fácilmente, descargar pero grandes suficiente para mostrar las características de rendimiento de SQL Server. Por ejemplo, ventajas significativas para los índices de almacén de columnas ocurrir solamente cuando se trabaja con un gran número de filas. 

El procedimiento `Application.Configuration_PopulateLargeSaleTable` puede utilizarse para aumentar considerablemente el número de filas de la `Fact.Sale` tabla. Tenga en cuenta que las filas se insertan en el año 2012 para evitar el conflicto con los datos de World Wide Importers existentes a partir del 1 de enero de 2013.

### <a name="procedure-details"></a>Detalles del procedimiento

#### <a name="name"></a>Nombre: 

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>Parámetros:

  `@EstimatedRowsFor2012` **bigint** (su valor predeterminado es 12000000)

#### <a name="result"></a>Resultado:

Aproximadamente el número necesario de filas se inserta en la `Fact.Sale` tabla en el año 2012. El procedimiento limita artificialmente el número de filas por día a 50000. Esta limitación podría modificarse, pero está ahí para evitar overinflations accidentales de la tabla.

Además, el procedimiento aplica indización de almacén de columnas agrupado, si ya no se han aplicado.
