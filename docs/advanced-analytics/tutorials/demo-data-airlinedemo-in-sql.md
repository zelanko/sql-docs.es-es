---
title: Demostración de llegadas de líneas aéreas y retraso conjunto de datos para los tutoriales de Python de SQL Server y R | Microsoft Docs
Description: Create a database containing the Airline dataset from R and Python. This dataset is used in exercises showing how to wrap R language or Python code in a SQL Server stored procedure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2ba431ecbc4f7d63415fdf6b351c5135ed0cdd8d
ms.sourcegitcommit: 70e47a008b713ea30182aa22b575b5484375b041
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2018
ms.locfileid: "49947447"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>Datos de líneas aéreas vuelos llegada demostración de tutoriales de Python de SQL Server y R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este ejercicio, creará una base de datos de SQL Server para almacenar los datos importados de R o Python integradas Airline demo conjuntos de datos. Las distribuciones de R y Python proporcionan datos equivalentes, que se pueden importar a una base de datos de SQL Server mediante Management Studio.

Para completar este ejercicio, debe tener [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) u otra herramienta que puede ejecutar consultas de T-SQL.

Tutoriales y guías de inicio rápido con este conjunto de datos incluyen lo siguiente:

+  [Crear un modelo de Python mediante revoscalepy](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>Crear la base de datos

1. Inicie SQL Server Management Studio, conéctese a una instancia del motor de base de datos que presenta la integración de R o Python.  

2. En el Explorador de objetos, haga clic en **bases de datos** y crear una base de datos nueva denominada **flightdata**.

3. Haga clic en **flightdata**, haga clic en **tareas**, haga clic en **importar archivo plano**.

4. Abra el archivo AirlineDemoData.csv proporcionado en la distribución de R o Python, dependiendo del lenguaje que ha instalado.

   Para R, busque **AirlineDemoSmall.csv** en C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData
   
   Para Python, busque **AirlineDemoSmall.csv** en C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Lib\site packages\revoscalepy\data\sample_data
  
Al seleccionar el archivo, se rellenan los valores predeterminados para el esquema y nombre de tabla.

  ![Asistente para la importación de archivos planos que muestra los valores predeterminados de airline demo](media/import-airlinedemosmall.png)

Haga clic en las páginas restantes, acepte los valores predeterminados, para importar los datos.


## <a name="query-the-data"></a>Consultar los datos

Como paso de validación, ejecute una consulta para confirmar que se han cargado los datos.

1. En el Explorador de objetos, en las bases de datos, haga clic en el **flightdata** , inicie una nueva consulta y base de datos.

2. Ejecute algunas consultas sencillas:

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>Pasos siguientes

En la siguiente lección, creará un modelo de regresión lineal basado en estos datos.

+ [Crear un modelo de Python mediante revoscalepy](use-python-revoscalepy-to-create-model.md)
