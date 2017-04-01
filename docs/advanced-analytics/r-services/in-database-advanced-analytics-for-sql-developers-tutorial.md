---
title: "In-Database Advanced Analytics for SQL Developers (Tutorial) (An&#225;lisis avanzado en base de datos para desarrolladores de SQL (Tutorial)) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: c18cb249-2146-41b7-8821-3a20c5d7a690
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# In-Database Advanced Analytics for SQL Developers (Tutorial) (An&#225;lisis avanzado en base de datos para desarrolladores de SQL (Tutorial))
El objetivo de este tutorial es proporcionar a los programadores SQL la experiencia práctica para crear una solución de análisis avanzado mediante [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. En este tutorial, aprenderá cómo incorporar R en una aplicación o solución BI ajustando código de R en procedimientos almacenados.  
  
## Información general  
El proceso de creación de una solución integral normalmente incluye la obtención y limpieza de los datos, la exploración de los datos y la ingeniería de características, el entrenamiento y la optimización del modelo, y por último la implementación del modelo en producción. El desarrollo y prueba del código de R se realiza mejor mediante un entorno de desarrollo integrado para R, como RStudio o [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]. Pero una vez creada la solución puede implementarla fácilmente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el entorno de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] que ya conoce.  
  
Por tanto, en este tutorial, asumiremos que se le ha proporcionado todo el código de R necesario para la solución y se centrará en la creación e implementación de una solución analítica avanzada que ya se ha codificado en R.  
  
-   [Paso 1: Descargar los datos de ejemplo](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md).    Descargue el conjunto de datos de ejemplo y los archivos de script SQL de ejemplo en un equipo local.  
  
-   [Paso 2: Importar datos a SQL Server mediante PowerShell](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md).  Ejecute un script de PowerShell que crea una base de datos y una tabla en la instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y carga los datos de ejemplo en la tabla.  
  
-   [Paso 3: Explorar y visualizar los datos](../../advanced-analytics/r-services/step-3-explore-and-visualize-the-data-in-database-advanced-analytics-tutorial.md).   Realice la exploración y visualización básicas de los datos, llamando a paquetes y funciones de R desde procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   [Paso 4: Crear características de datos mediante T-SQL](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md).  Cree nuevas características de datos mediante funciones personalizadas de SQL.  
  
-   [Paso 5: Entrenar y guardar un modelo con T-SQL](../../advanced-analytics/r-services/step-5-train-and-save-a-model-using-t-sql.md).  Cree y guarde el modelo de aprendizaje automático mediante procedimientos almacenados.  
  
-   [Paso 6: Hacer operativo el modelo](../../advanced-analytics/r-services/step-6-operationalize-the-model-in-database-advanced-analytics-tutorial.md).  Después de que el modelo se ha guardado en la base de datos, llame al modelo de predicción desde [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante procedimientos almacenados.  
  
> [!NOTE]  
> Se recomienda no usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para escribir o probar el código de R. Si el código R que se incrusta en un procedimiento almacenado tiene algún problema, la información que se devuelve desde el procedimiento almacenado no suele ser adecuada para entender la causa del error.   
>   
> Para la depuración, se recomienda usar una herramienta como RStudio o [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]. Los scripts de R que se proporcionan en este tutorial ya han sido desarrollados y depurados mediante las herramientas tradicionales de R.  
>   
> Si está interesado en aprender a desarrollar scripts de R que se puedan ejecutar en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], consulte este tutorial: [Tutorial integral de ciencia de datos](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md))  
  
### Escenario  
Este tutorial usa el conocido conjunto de datos NYC Taxi. Este conjunto de datos público contiene 20 GB de archivos CSV comprimidos (~ 48 GB sin comprimir), que describen los detalles de más de 173 millones de carreras de taxi individuales en 2013, así como las tarifas pagadas por cada carrera. Para realizar este tutorial de forma rápida y sencilla, hemos creado una muestra representativa de los datos: el 1 % de los datos, o 1 703 957 filas y 23 columnas. En este tutorial, va a usar estos datos para crear un modelo de clasificación binaria que predice si un viaje concreto es probable que obtenga una propina o no, basándose en columnas como la hora del día, la distancia y la ubicación de recogida.  
  
  
### Requisitos  
Este tutorial está destinado a usuarios que ya están familiarizados con las operaciones de base de datos fundamentales, como la creación de tablas y bases de datos, la importación de datos a tablas y la creación de consultas SQL. Se proporciona todo el código de R, por lo que no es necesario ningún entorno de desarrollo de R. Un programador experimentado de SQL debe ser capaz de completar este tutorial con [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o mediante la ejecución de los scripts de PowerShell proporcionados.  
  
Pero antes de iniciar el tutorial debe completar estos preparativos:  
  
-   Conectarse a una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con SQL Server R Services habilitado (requiere CTP 3 o posterior). Para obtener más detalles, consulte las instrucciones de instalación: [Configurar SQL Server R Services (en bases de datos)](https://msdn.microsoft.com/library/mt696069.aspx)  
  
 -   El inicio de sesión que use para este tutorial debe tener permisos para crear bases de datos y otros objetos, cargar datos, seleccionar datos y ejecutar procedimientos almacenados.  
  
## Paso siguiente  
[Paso 1: Descargar los datos de ejemplo](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md)  
  
## Vea también  
[Tutoriales de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
[SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  
  
