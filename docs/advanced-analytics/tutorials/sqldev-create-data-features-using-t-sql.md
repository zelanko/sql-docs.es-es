---
title: 'Características de datos de la lección 2 crear con funciones de R y T-SQL: SQL Server Machine Learning'
description: Tutorial que muestra cómo agregar cálculos a los procedimientos almacenados para su uso en los modelos de aprendizaje automático de R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 43086b8d3898e4d9096e82289ce6e6f196542997
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645404"
---
# <a name="lesson-2-create-data-features-using-r-and-t-sql"></a>Lección 2: Crear características de datos mediante R y T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo forma parte de un tutorial para desarrolladores de SQL sobre cómo usar R en SQL Server.

En este paso, aprenderá a crear características desde datos sin procesar mediante una función de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Después, llamaremos a esa función desde un procedimiento almacenado para crear una tabla que contiene los valores de las características.

## <a name="about-feature-engineering"></a>Acerca de ingeniería de características

Después de varias series de exploración de datos, ha recopilado conocimientos de los datos y está listo para pasar a la *ingeniería de funciones*. Este proceso de creación de características significativas de los datos sin procesar es un paso crítico en la creación de modelos analíticos.

En este conjunto de datos, los valores de distancia se basan en la distancia notificada del taxímetro y no representan necesariamente la distancia geográfica o la distancia real recorrida. Por tanto, debe calcular la distancia directa entre los puntos de origen y destino, usando las coordenadas disponibles en el conjunto de datos de origen NYC Taxi. Puede hacerlo mediante la [fórmula Haversine](https://en.wikipedia.org/wiki/Haversine_formula) en un función personalizada de [!INCLUDE[tsql](../../includes/tsql-md.md)] .

Usará una función personalizada de T-SQL, _fnCalculateDistance_, para calcular la distancia usando la fórmula Haversine, y una segunda función personalizada de T-SQL, _fnEngineerFeatures_, para crear una tabla que contiene todas las características.

El proceso general es como sigue:

- Cree la función de T-SQL que realiza los cálculos

- Llame a la función para generar los datos de características

- Guardar los datos de características a una tabla

## <a name="calculate-trip-distance-using-fncalculatedistance"></a>Calcular la distancia de viaje mediante fnCalculateDistance

La función _fnCalculateDistance_ debe haberse descargado y registrado con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como parte de la preparación para este tutorial. Tómese un minuto para revisar el código.
  
1. En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], expanda **Programación**, expanda **Funciones** y, después, **Funciones escalares**.   

2. Haga clic con el botón derecho en _fnCalculateDistance_y seleccione **Modificar** para abrir el script de [!INCLUDE[tsql](../../includes/tsql-md.md)] en una nueva ventana de consulta.
  
    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function that calculates the direct distance between two geographical coordinates.  
    RETURNS float  
    AS  
    BEGIN  
      DECLARE @distance decimal(28, 10)  
      -- Convert to radians  
      SET @Lat1 = @Lat1 / 57.2958  
      SET @Long1 = @Long1 / 57.2958  
      SET @Lat2 = @Lat2 / 57.2958  
      SET @Long2 = @Long2 / 57.2958  
      -- Calculate distance  
      SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))  
      --Convert to miles  
      IF @distance <> 0  
      BEGIN  
        SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);  
      END  
      RETURN @distance  
    END
    GO
    ```
  
    - La función es una función escalar y devuelve un único valor de datos de un tipo predefinido.
  
    - Toma los valores de latitud y longitud como entradas, obtenidos de las ubicaciones de origen y destino de los viajes. La fórmula Haversine convierte ubicaciones en radianes y usa esos valores para calcular la distancia directa en millas entre las dos ubicaciones.

## <a name="generate-the-features-using-fnengineerfeatures"></a>Generar las características mediante _fnEngineerFeatures_

Para agregar los valores calculados en una tabla que se puede usar para entrenar el modelo, deberá usar otra función _fnEngineerFeatures_. La nueva función llama a la función de T-SQL creada anteriormente, _fnCalculateDistance_, para obtener la distancia directa entre las ubicaciones de origen y destino. 

1. Tómese un minuto para revisar el código de la función personalizada de T-SQL, _fnEngineerFeatures_, que debe haberse creado como parte de la preparación para este tutorial.
  
    ```sql
    CREATE FUNCTION [dbo].[fnEngineerFeatures] (  
    @passenger_count int = 0,  
    @trip_distance float = 0,  
    @trip_time_in_secs int = 0,  
    @pickup_latitude float = 0,  
    @pickup_longitude float = 0,  
    @dropoff_latitude float = 0,  
    @dropoff_longitude float = 0)  
    RETURNS TABLE  
    AS
      RETURN
      (
      -- Add the SELECT statement with parameter references here
      SELECT
        @passenger_count AS passenger_count,
        @trip_distance AS trip_distance,
        @trip_time_in_secs AS trip_time_in_secs,
        [dbo].[fnCalculateDistance](@pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude) AS direct_distance
  
      )
    GO
    ```

    + Esta función con valores de tabla que toma varias columnas como entradas y genera una tabla con varias columnas de característica.

    + El propósito de esta función es crear nuevas características para su uso en la creación de un modelo.

2.  Para comprobar que esta función funciona, usarla para calcular la distancia geográfica de los viajes donde la distancia medida era 0 pero las ubicaciones de origen y destino eran diferentes.
  
    ```sql
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    Como puede ver, la distancia notificada por el taxímetro no siempre se corresponde con la distancia geográfica. Por eso es tan importante la ingeniería de características. Puede usar estas características mejoradas de los datos para entrenar un modelo de aprendizaje automático con R.

## <a name="next-lesson"></a>Lección siguiente

[Lección 3: Entrenar y guardar un modelo con T-SQL](sqldev-train-and-save-a-model-using-t-sql.md)

## <a name="previous-lesson"></a>Lección anterior

[Lección 1: Explorar y visualizar los datos mediante R y los procedimientos almacenados](sqldev-explore-and-visualize-the-data.md)
