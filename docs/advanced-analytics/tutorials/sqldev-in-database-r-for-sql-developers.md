---
title: Tutorial para realizar análisis en bases de datos con R y SQL Server Machine Learning | Microsoft Docs
description: Tutorial que muestra cómo insertar código de R en SQL Server los procedimientos almacenados y funciones de Transact-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 16b3a19e8252e35fcefc817be2c8de11471b4eb3
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394520"
---
# <a name="tutorial-learn-in-database-analytics-using-r-in-sql-server"></a>Tutorial: Obtenga información sobre los análisis en bases de datos con R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial para programadores de SQL, obtener experiencia práctica con el lenguaje R para compilar e implementar un solución de aprendizaje ajustando el código de R en procedimientos almacenados de automático.

Este tutorial usa un conjunto de datos público conocido, en función de los viajes de taxis de Nueva York. Para que el código de ejemplo se ejecute con mayor rapidez, hemos creado una muestra representativa del 1% de los datos. Usará estos datos para crear un modelo de clasificación binaria que predice si un viaje concreto es probable que reciba una propina o no, en función de las columnas como la hora del día, la distancia y la ubicación de recogida.

> [!NOTE]
> 
> La misma solución está disponible en Python. Se requiere SQL Server 2017. Vea [en análisis base de datos para desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="overview"></a>Información general

El proceso de creación de una solución de extremo a otro normalmente consta de obtención y limpieza de datos, exploración de datos y diseño de características, entrenamiento del modelo y la optimización y, por último, implementación del modelo en producción. Desarrollo y pruebas del código real se realiza mejor mediante un entorno de desarrollo dedicado. Para R, que podría significar RStudio o [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)].

Pero una vez creada la solución puede implementarla fácilmente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el entorno de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]que ya conoce.

- [Lección 1: Configurar los datos de demostración de taxis de Nueva York](../tutorials/sqldev-download-the-sample-data.md)

- [Lección 2: Explorar y visualizar la distribución y la forma de datos mediante una llamada a funciones de R en procedimientos almacenados](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [Lección 3: Crear características de datos mediante R en las funciones de Transact-SQL](../tutorials/sqldev-create-data-features-using-t-sql.md)
  
- [Lección 4: Entrenar y guardar un modelo de R mediante procedimientos almacenados y funciones](../r/sqldev-train-and-save-a-model-using-t-sql.md)
  
- [La lección 5: Código encapsulado de R en un procedimiento almacenado para la operacionalización](../tutorials/sqldev-operationalize-the-model.md). 
  Después de que el modelo se ha guardado en la base de datos, llame al modelo de predicción desde [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante procedimientos almacenados.

## <a name="prerequisites"></a>Requisitos previos

Este tutorial supone que está familiarizado con operaciones de base de datos básica, como la creación de tablas y bases de datos, importación de datos y escribir consultas SQL. Supone que sabe R. Por lo tanto, se proporciona todo el código de R. Un programador experimentado de SQL puede usar un script de PowerShell proporcionado, datos de ejemplo en GitHub, y [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para completar este ejemplo. 

Antes de comenzar el tutorial:

- Compruebe que dispone de una instancia configurada de [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) o [SQL Server 2017 Machine Learning Services con R habilitado](../install/sql-machine-learning-services-windows-install.md#verify-installation). Además, [confirme que tiene las bibliotecas de R](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location).
- El inicio de sesión que usa para este tutorial debe tener permisos para crear bases de datos y otros objetos, para cargar los datos, seleccione datos y ejecutan procedimientos almacenados.

> [!NOTE]
> Se recomienda que realice **no** usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para escribir o probar el código de R. Si el código que se incrusta en un procedimiento almacenado tiene algún problema, la información que se devuelve desde el procedimiento almacenado es no suele ser adecuada para entender la causa del error.
> 
> Para la depuración, se recomienda usar una herramienta como [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)], o RStudio. Los scripts de R que se proporcionan en este tutorial ya han sido desarrollados y depurados mediante las herramientas tradicionales de R.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Lección 1: Descargar los datos de ejemplo](../tutorials/sqldev-download-the-sample-data.md)