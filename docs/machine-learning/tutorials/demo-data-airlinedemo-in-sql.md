---
description: Datos de demostración de la llegada de vuelos de líneas aéreas para tutoriales de Python y R de SQL Server
title: Datos de demostración de vuelos de líneas aéreas para tutoriales
Description: Cree una base de datos que contenga el conjunto de datos para líneas aéreas de R y Python. Este conjunto de datos se utiliza en los tutoriales de R y Python para SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/22/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 3b19e905d68d53764a496ab5ee7745e3529484cf
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489905"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>Datos de demostración de la llegada de vuelos de líneas aéreas para tutoriales de Python y R de SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

En este ejercicio, va a crear una base de datos de SQL Server para almacenar los datos importados de los conjuntos de datos de demostración de líneas aéreas integradas en R o Python. Las distribuciones de R y Python proporcionan datos equivalentes, que puede importar a una base de datos de SQL Server mediante Management Studio.

Para completar este ejercicio, debe tener [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) u otra herramienta que pueda ejecutar consultas de T-SQL.

Entre los tutoriales y las guías de inicio rápido que usan este conjunto de datos se incluyen los siguientes:

+  [Creación de un modelo de Python mediante revoscalepy](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>Creación de la base de datos

1. Inicie SQL Server Management Studio, conéctese a una instancia del motor de base de datos que tenga integración con R o Python.  

2. En Explorador de objetos, haga clic con el botón derecho en **Bases de datos** y cree una nueva base de datos denominada **flightdata**.

3. Haga clic con el botón derecho en **flightdata**, haga clic en **Tareas** y haga clic en **Importar archivo plano**.

4. Abra el archivo AirlineDemoData.csv proporcionado en la distribución de R o Python, en función del lenguaje de computación que haya instalado.

   Para R, vaya a **AirlineDemoSmall.csv** en C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData
   
   Para Python, vaya a **AirlineDemoSmall.csv** at C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\data\sample_data
  
Al seleccionar el archivo, el nombre y el esquema de la tabla se rellenan con los valores predeterminados.

  ![Asistente para la importación de archivos planos en el que se muestran los valores predeterminados de demostración para líneas aéreas](media/import-airlinedemosmall.png)

Haga clic en las páginas restantes y acepte los valores predeterminados para importar los datos.


## <a name="query-the-data"></a>Consultar los datos

Como paso de validación, ejecute una consulta para confirmar que se han cargado los datos.

1. En Explorador de objetos, debajo de Bases de datos, haga clic con el botón derecho en la base de datas **flightdata** e inicie una nueva consulta.

2. Ejecute algunas consultas sencillas:

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>Pasos siguientes

En la lección siguiente, creará un modelo de regresión lineal basado en estos datos.

+ [Creación de un modelo de Python mediante revoscalepy](use-python-revoscalepy-to-create-model.md)
