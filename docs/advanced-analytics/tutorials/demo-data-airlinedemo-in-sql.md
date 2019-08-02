---
title: Conjunto de datos de demostración de vuelos de avión para SQL Server tutoriales de Python y R
Description: Cree una base de datos que contenga el conjunto de datos de línea aérea de R y Python. Este conjunto de DataSet se usa en ejercicios que muestran cómo ajustar el lenguaje R o el código Python en un SQL Server procedimiento almacenado.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b7f28dd4b3e7e6990e037dbd9afe164d8d0e4bec
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714811"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>Datos de demostración de la llegada de vuelos de líneas aéreas para SQL Server tutoriales de Python y R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este ejercicio, cree una base de datos de SQL Server para almacenar los datos importados de los conjuntos de datos de demostración de líneas aéreas integradas de R o Python. Las distribuciones de R y Python proporcionan datos equivalentes, que puede importar a una base de datos de SQL Server mediante Management Studio.

Para completar este ejercicio, debe tener [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) u otra herramienta que pueda ejecutar consultas de T-SQL.

Entre los tutoriales y las guías de inicio rápido que usan este conjunto de datos se incluyen los siguientes:

+  [Creación de un modelo de Python mediante revoscalepy](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>Crear la base de datos

1. Inicie SQL Server Management Studio, conéctese a una instancia del motor de base de datos que tenga integración de R o Python.  

2. En Explorador de objetos, haga clic con el botón derecho en **bases** de datos y cree una nueva base de datos denominada **flightdata**.

3. Haga clic con el botón secundario en **flightdata**, haga clic en **tareas**y en **Importar archivo plano**.

4. Abra el archivo AirlineDemoData. csv proporcionado en la distribución de R o Python, según el idioma que haya instalado.

   Para R, busque **AirlineDemoSmall. csv** en C:\Archivos de Programa\microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData
   
   Para Python, busque **AirlineDemoSmall. csv** en C:\Archivos de Programa\microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\data\sample_data
  
Al seleccionar el archivo, los valores predeterminados se rellenan para el nombre y el esquema de la tabla.

  ![Asistente para importación de archivos planos con valores predeterminados de demo de líneas aéreas](media/import-airlinedemosmall.png)

Haga clic en las páginas restantes y acepte los valores predeterminados para importar los datos.


## <a name="query-the-data"></a>Consultar los datos

Como paso de validación, ejecute una consulta para confirmar que se cargaron los datos.

1. En Explorador de objetos, en bases de datos, haga clic con el botón secundario en la base de datos **flightdata** e inicie una nueva consulta.

2. Ejecute algunas consultas sencillas:

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>Pasos siguientes

En la lección siguiente, creará un modelo de regresión lineal basado en estos datos.

+ [Creación de un modelo de Python mediante revoscalepy](use-python-revoscalepy-to-create-model.md)
