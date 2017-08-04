---
title: "Generación de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 01/30/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.technology:
- " database-engine "
ms.topic: article
ms.assetid: f387273b-8b5f-4687-b033-09499ea2d68f
caps.latest.revision: 4
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c17ad40220d46ab6e19054818ce2abfdce7251f4
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="wideworldimporters-data-generation"></a>Generación de datos WideWorldImporters
Las versiones publicadas de las bases de datos WideWorldImporters y WideWorldImportersDW contiene los datos a partir del 1 de enero de 2013, hasta el día en que se generaron estas bases de datos.

Si se utilizan las bases de datos de ejemplo en una fecha posterior, para fines de demostración o ilustración, puede ser beneficioso incluir datos de ejemplo más recientes en la base de datos.

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

Esta instrucción agrega datos de compra y de ventas de ejemplo en la base de datos, hasta la fecha actual. Genera el progreso de los datos de generación por días. Tardará rougly 10 minutos para que todos los años que necesita que los datos. Tenga en cuenta que hay algunas diferencias en los datos generados entre ejecuciones, dado que no hay un factor aleatorio en la generación de datos.

Para aumentar o disminuir la cantidad de datos generados en términos de pedidos por día, cambie el valor para el parámetro `@AverageNumberOfCustomerOrdersPerDay`. Los parámetros `@SaturdayPercentageOfNormalWorkDay` y `@SundayPercentageOfNormalWorkDay` se usan para determinar el volumen de pedidos para los días de la semana.

## <a name="importing-generated-data-in-wideworldimportersdw"></a>Importación de datos generados en WideWorldImportersDW

Para importar datos de ejemplo hasta la fecha actual en la base de datos OLAP WideWorldImportersDW, siga estos pasos:

1. Ejecutar la lógica de generación de datos en la base de datos WideWorldImporters OLTP, siguiendo los pasos anteriores.
2. Si aún no lo ha hecho, instale una versión limpia de la base de datos de WideWorldImportersDW. Para obtener instrucciones de instalación, **WideWorldImporters instalación y configuración**.
3. Reinicializar la base de datos OLAP mediante la ejecución de la siguiente instrucción en la base de datos:

```
    EXECUTE [Application].Configuration_ReseedETL
```

4. Ejecutar el paquete SSIS **ETL.ispac diaria** para importar los datos en la base de datos OLAP. Para obtener instrucciones sobre cómo ejecutar el trabajo ETL, consulte **flujo de trabajo de ETL WideWorldImporters**.

## <a name="generating-data-in-wideworldimportersdw-for-performance-testing"></a>Generar datos en WideWorldImportersDW para pruebas de rendimiento

WideWorldImportersDW tiene la capacidad de aumentar el tamaño de los datos, con el fin de pruebas de rendimiento, por ejemplo con el almacén de columnas agrupado arbitrariamente.

Uno de los desafíos al enviar un ejemplo como World Wide Importers es mantener el tamaño de la descarga suficientemente pequeño como para ser distribuibles pero lo suficientemente grande como para poder mostrar las características de rendimiento de SQL Server. Un área donde esto es un reto particular es cuando se trabaja con índices de almacén de columnas. Ventajas significativas proceden solamente cuando se trabaja con un gran número de filas. 

El procedimiento `Application.Configuration_PopulateLargeSaleTable` puede utilizarse para aumentar considerablemente el número de filas de la `Fact.Sale` tabla. Tenga en cuenta que las filas se insertan en el año 2012 para evitar el conflicto con los datos de World Wide Importers existentes a partir de 1 de enero de 2013.

### <a name="procedure-details"></a>Detalles del procedimiento

#### <a name="name"></a>Nombre: 

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>Parámetros:

  `@EstimatedRowsFor2012`**bigint** (su valor predeterminado es 12000000)

#### <a name="result"></a>Resultado:

Aproximadamente el número necesario de filas se inserta en la `Fact.Sale` tabla en el año 2012. El procedimiento limita artificialmente el número de filas por día a 50000. Esto podría cambiarse pero no existe evitar overinflations a las medidas de la tabla.

Además, el procedimiento aplica indización de almacén de columnas agrupado, si ya no se han aplicado.
