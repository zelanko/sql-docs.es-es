---
title: 'WideWorldImporters generar datos: base de datos de ejemplo SQL | Microsoft Docs'
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 38ba117051ad10d788c2357dfb70d36c2b5e50d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091267"
---
# <a name="wideworldimporters-data-generation"></a>Generación de datos de WideWorldImporters
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Las versiones publicadas de las bases de datos WideWorldImporters y WideWorldImportersDW tengan datos desde el 1 de enero de 2013, hasta el día en que se generaron las bases de datos.

Al usar estas bases de datos de ejemplo, desea incluir datos de ejemplo más recientes.

## <a name="data-generation-in-wideworldimporters"></a>Generación de datos WideWorldImporters

Para generar datos de ejemplo hasta la fecha actual:

1. Si no lo ha hecho, instale una versión limpia de la base de datos WideWorldImporters. Para obtener instrucciones de instalación, consulte [instalación y configuración](wide-world-importers-oltp-install-configure.md).
2. Ejecute la instrucción siguiente en la base de datos:

    ```
        EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
            @AverageNumberOfCustomerOrdersPerDay = 60,
            @SaturdayPercentageOfNormalWorkDay = 50,
            @SundayPercentageOfNormalWorkDay = 0,
            @IsSilentMode = 1,
            @AreDatesPrinted = 1;
    ```

    Esta instrucción agrega datos de compras y ventas de ejemplo para la base de datos, hasta la fecha actual. Muestra el progreso de la generación de datos por día. Generación de datos puede tardar unos 10 minutos para cada año que necesita que los datos. Debido a un factor aleatorio en la generación de datos, hay algunas diferencias en los datos que se generaron entre ejecuciones.

    Para aumentar o disminuir la cantidad de datos generados para los pedidos por día, cambie el valor del parámetro `@AverageNumberOfCustomerOrdersPerDay`. Use los parámetros `@SaturdayPercentageOfNormalWorkDay` y `@SundayPercentageOfNormalWorkDay` para determinar el volumen de pedidos para los días de la semana.

## <a name="import-generated-data-in-wideworldimportersdw"></a>Datos de importación generada en WideWorldImportersDW

Para importar datos de ejemplo hasta la fecha actual en la base de datos WideWorldImportersDW OLAP:

1. Ejecutar la lógica de generación de datos en la base de datos WideWorldImporters OLTP mediante los pasos en la sección anterior.
2. Si aún no lo ha hecho, instale una versión limpia de la base de datos WideWorldImportersDW. Para obtener instrucciones de instalación, consulte [instalación y configuración](wide-world-importers-oltp-install-configure.md).
3. Reinicialice la base de datos OLAP mediante la ejecución de la siguiente instrucción en la base de datos:

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. Ejecute el *ETL.ispac diario* paquete SQL Server Integration Services para importar los datos en la base de datos OLAP. Para obtener información sobre cómo ejecutar el trabajo ETL, consulte [flujo de trabajo de WideWorldImporters ETL](wide-world-importers-perform-etl.md).

## <a name="generate-data-in-wideworldimportersdw-for-performance-testing"></a>Generar datos en WideWorldImportersDW para pruebas de rendimiento

WideWorldImportersDW arbitrariamente puede aumentar el tamaño de los datos para pruebas de rendimiento. Por ejemplo, puede aumentar el tamaño de datos que se usará con la indexación de almacén de columnas agrupado.

Uno de los desafíos es mantener el tamaño de la descarga lo suficientemente pequeño como para fácilmente, descargar, pero de gran tamaño suficiente para demostrar las características de rendimiento de SQL Server. Por ejemplo, se obtienen ventajas significativas para los índices de almacén de columnas solo cuando se trabaja con un mayor número de filas. 

Puede usar el `Application.Configuration_PopulateLargeSaleTable` procedimiento para aumentar el número de filas de la `Fact.Sale` tabla. Las filas se insertan en el año 2012 para evitar el conflicto con los datos de World Wide Importers existentes que comienza el 1 de enero de 2013.

### <a name="procedure-details"></a>Detalles del procedimiento

#### <a name="name"></a>NOMBRE

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>Parámetros

  `@EstimatedRowsFor2012` **bigint** (con un valor predeterminado de 12000000)

#### <a name="result"></a>Resultado

Aproximadamente el número necesario de las filas se inserta en el `Fact.Sale` tabla en el año 2012. El procedimiento artificialmente limita el número de filas a 50 000 por día. Puede cambiar esta limitación, pero la limitación ayuda a evitar overinflations accidentales de la tabla.

El procedimiento también aplica si ya no se ha aplicado la indización de almacén de columnas agrupado.
