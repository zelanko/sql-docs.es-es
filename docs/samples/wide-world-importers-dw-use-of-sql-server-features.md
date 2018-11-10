---
title: 'Base de datos WideWorldImporters OLAP: uso de SQL Server | Microsoft Docs'
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 57936009880849b3ca1e566110e688b699f6835b
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269739"
---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>Uso de WideWorldImportersDW de capacidades y características de SQL Server
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW está diseñada para presentar muchas de las características claves de SQL Server que son adecuadas para el almacenamiento de datos y análisis. La siguiente es una lista de características de SQL Server y las capacidades y una descripción de cómo se utilizan en WideWorldImportersDW.

## <a name="polybase"></a>PolyBase

[Se aplica a SQL Server (2016 y versiones posteriores)]

PolyBase se usa para combinar la información de ventas de WideWorldImportersDW con un conjunto de datos públicos sobre datos demográficos para saber qué ciudades podrían ser de interés para la expansión de más de las ventas.

Para habilitar el uso de PolyBase en la base de datos de ejemplo, asegúrese de que está instalado y ejecute el siguiente procedimiento almacenado en la base de datos:

    EXEC [Application].[Configuration_ApplyPolyBase]

Esto creará una tabla externa `dbo.CityPopulationStatistics` que hace referencia a un conjunto de datos público que contiene los datos de población de las ciudades de Estados Unidos, hospedada en Azure blob storage. Se recomienda revisar el código en el procedimiento almacenado para comprender el proceso de configuración. Si desea hospedar sus propios datos en Azure blob storage y mantener la seguridad de acceso público general, deberá realizar los pasos de configuración adicionales. La siguiente consulta devuelve los datos de ese conjunto de datos externos:

    SELECT CityID, StateProvinceCode, CityName, YearNumber, LatestRecordedPopulation FROM dbo.CityPopulationStatistics;

Para saber qué ciudades podrían ser de interés para la expansión más, la siguiente consulta examina la tasa de crecimiento de las ciudades y devuelve las ciudades más grandes de primeros 100 con un crecimiento significativo, y donde Wide World Importers no tiene una presencia en ventas. La consulta implica una combinación entre la tabla remota `dbo.CityPopulationStatistics` y la tabla local `Dimension.City`y un filtro de la tabla local `Fact.Sales`.

    WITH PotentialCities
    AS
    (
        SELECT cps.CityName,
               cps.StateProvinceCode,
               MAX(cps.LatestRecordedPopulation) AS PopulationIn2016,
               (MAX(cps.LatestRecordedPopulation) - MIN(cps.LatestRecordedPopulation)) * 100.0
                   / MIN(cps.LatestRecordedPopulation) AS GrowthRate
        FROM dbo.CityPopulationStatistics AS cps
        WHERE cps.LatestRecordedPopulation IS NOT NULL
        AND cps.LatestRecordedPopulation <> 0
        GROUP BY cps.CityName, cps.StateProvinceCode
    ),
    InterestingCities
    AS
    (
        SELECT DISTINCT pc.CityName,
                        pc.StateProvinceCode,
                        pc.PopulationIn2016,
                        FLOOR(pc.GrowthRate) AS GrowthRate
        FROM PotentialCities AS pc
        INNER JOIN Dimension.City AS c
        ON pc.CityName = c.City
        WHERE GrowthRate > 2.0
        AND NOT EXISTS (SELECT 1 FROM Fact.Sale AS s WHERE s.[City Key] = c.[City Key])
    )
    SELECT TOP(100) CityName, StateProvinceCode, PopulationIn2016, GrowthRate
    FROM InterestingCities
    ORDER BY PopulationIn2016 DESC;

## <a name="clustered-columnstore-indexes"></a>Índices clúster de almacén de columnas

(Versión completa del ejemplo)

Los índices de almacén de columnas en clúster (CCI) se usan con todas las tablas de hechos para reducir el consumo de almacenamiento y mejorar el rendimiento de las consultas. Con el uso de CCI, el almacenamiento de base para las tablas de hechos usa compresión de columnas.

Los índices no clúster se utilizan en la parte superior del índice agrupado, para facilitar la clave principal y restricciones de clave externa. Estas restricciones se agregaron fuera de una gran cantidad de precaución: el proceso ETL orígenes de los datos de la base de datos WideWorldImporters, que tiene restricciones para exigir la integridad. Quitar las restricciones de clave principales y externas y sus índices auxiliares, podría reducir el consumo de almacenamiento de las tablas de hechos.

**Tamaño de los datos**

La base de datos de ejemplo tiene limitado el tamaño de los datos, para que sea fácil de descargar e instalar el ejemplo. Sin embargo, para ver las ventajas de rendimiento real de los índices de almacén de columnas, desearía usar un conjunto de datos más grande.

Puede ejecutar la instrucción siguiente para aumentar el tamaño de la `Fact.Sales` tabla mediante la inserción de otra de 12 millones de filas de datos de ejemplo. Todas estas filas se insertan durante el año 2012, tal que no hay interferencias con el proceso ETL.

    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]

Esta instrucción tardará aproximadamente 5 minutos para ejecutar. Para insertar más de 12 millones de filas, pase el número deseado de filas que se va a insertar como un parámetro a este procedimiento almacenado.

Para comparar el rendimiento de las consultas con y sin almacén de columnas, puede quitar o volver a crear el índice de almacén de columnas agrupado.

Para quitar el índice:

    DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]

Para volver a crear:

    CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]

## <a name="partitioning"></a>Particiones

(Versión completa del ejemplo)

Tamaño de los datos en un almacén de datos puede crecer muy grande. Por lo tanto, es recomendable utilizar la creación de particiones para administrar el almacenamiento de las tablas grandes en la base de datos.

Todas las tablas de hechos más grandes se particionan por año. La única excepción es `Fact.Stock Holdings`, que no está basado en la fecha y con el tamaño de datos limitados en comparación con las otras tablas de hechos.

Es la función de partición que se usa para las tablas con particiones de todos los `PF_Date`, y el esquema de partición que se va a usar es `PS_Date`.

## <a name="in-memory-oltp"></a>OLTP en memoria

(Versión completa del ejemplo)

WideWorldImportersDW usa las tablas optimizadas para memoria SCHEMA_ONLY para las tablas de ensayo. Todos los `Integration.` * `_Staging` tablas son SCHEMA_ONLY optimizadas para memoria.

La ventaja de las tablas SCHEMA_ONLY es que no se ha iniciado y no requieren ningún acceso al disco. Esto mejora el rendimiento del proceso ETL. Dado que estas tablas no se ha iniciado sesión, su contenido se pierden si se produce un error. Sin embargo, el origen de datos sigue estando disponible, por lo que simplemente se puede reiniciar el proceso ETL, si se produce un error.
