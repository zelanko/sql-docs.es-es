---
title: "En bases de datos análisis de R para desarrolladores de SQL (tutorial) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: c18cb249-2146-41b7-8821-3a20c5d7a690
caps.latest.revision: "15"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: cb5b3b55f2051589ba9885c39077a0560ea35c13
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="in-database-r-analytics-for-sql-developers-tutorial"></a>Análisis de R en bases de datos para desarrolladores de SQL (tutorial)

El objetivo de este tutorial es proporcionar a los programadores SQL con experiencia práctica para crear un solución de SQL Server de aprendizaje automático. En este tutorial, aprenderá cómo incorporar R en una aplicación o solución BI insertando código R en los procedimientos almacenados.

> [!NOTE]
> 
> La misma solución está disponible en Python. Se requiere SQL Server 2017. Vea [en bases de datos análisis para los desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="overview"></a>Información general

El proceso de creación de una solución integral normalmente incluye la obtención y limpieza de los datos, la exploración de los datos y la ingeniería de características, el entrenamiento y la optimización del modelo, y por último la implementación del modelo en producción. Desarrollo y prueba del código real se realiza mejor usar un entorno de desarrollo dedicado. En caso de R, que podría significar RStudio o [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)].

Pero una vez creada la solución puede implementarla fácilmente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el entorno de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]que ya conoce.

En este tutorial, se supone que se le ha proporcionado todo el código de R necesario para la solución y se centran en la creación e implementación de la solución con SQL Server.

- [Lección 1: Descargar los datos de ejemplo](../tutorials/sqldev-download-the-sample-data.md)

    Descargue el conjunto de datos de ejemplo y los archivos de script SQL de ejemplo en un equipo local.

- [Lección 2: Importar datos a SQL Server usando PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)

    Ejecute un script de PowerShell que crea una base de datos y una tabla en la instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y carga los datos de ejemplo en la tabla.

- [Lección 3: Explorar y visualizar los datos](../tutorials/sqldev-explore-and-visualize-the-data.md)

    Realice la exploración y visualización básicas de los datos, llamando a paquetes y funciones de R desde procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] .

- [Lección 4: Crear características de datos mediante T-SQL](../tutorials/sqldev-create-data-features-using-t-sql.md)

    Cree nuevas características de datos mediante funciones personalizadas de SQL.
  
-   [Lección 5: Entrenar y guardar un modelo de R con T-SQL](../r/sqldev-train-and-save-a-model-using-t-sql.md)

    Crear un modelo de aprendizaje automático con R en los procedimientos almacenados. Guardar el modelo en una tabla de SQL Server.
  
-   [Lección 6: Poner el modelo](../tutorials/sqldev-operationalize-the-model.md)

    Después de que el modelo se ha guardado en la base de datos, llame al modelo de predicción desde [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante procedimientos almacenados.

### <a name="scenario"></a>Escenario

Este tutorial usa un conjunto de datos público conocido, en función de viajes en taxis ciudad de Nueva York. Para que el ejemplo de código se ejecute más rápido, creamos una muestra representativa de 1% de los datos. Usará estos datos para crear un modelo de clasificación binaria que predice si un viaje determinado es probable que obtenga una sugerencia o no, en función de las columnas como la hora del día, la distancia y la ubicación de recogida.

### <a name="requirements"></a>Requisitos

Este tutorial está destinado a usuarios que ya están familiarizados con las operaciones fundamentales de la base de datos, como la creación de tablas y bases de datos, importar datos en tablas y crear consultas SQL. Se proporciona todo el código de R, por lo que no es necesario ningún entorno de desarrollo de R. Un programador experimentado de SQL debe ser capaz de completar este ejemplo mediante el uso de [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y ejecutando los scripts de PowerShell proporcionados.

Sin embargo, antes de iniciar el tutorial, debe completar estos preparativos:

- Conéctese a una instancia de SQL Server 2016 con R Services o SQL Server 2017 con servicios de aprendizaje de máquina y R habilitado.
- El inicio de sesión que utilizas para este tutorial debe tener permisos para crear bases de datos y otros objetos, debe cargar los datos, seleccione datos y ejecutan procedimientos almacenados.

> [!NOTE]
> Te recomendamos que hagas **no** usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para escribir o probar el código de R. Si el código que incrusta en un procedimiento almacenado tiene algún problema, la información que se devuelve desde el procedimiento almacenado es normalmente inadecuada entender la causa del error.
> 
> Para la depuración, se recomienda utilizar una herramienta como [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)], o RStudio. Los scripts de R que se proporcionan en este tutorial ya han sido desarrollados y depurados mediante las herramientas tradicionales de R.

## <a name="next-lesson"></a>Lección siguiente

[Lección 1: Descargar los datos de ejemplo](../tutorials/sqldev-download-the-sample-data.md)
