---
title: Tutorial de análisis de R incrustado para los desarrolladores de aprendizaje automático de SQL Server | Documentos de Microsoft
description: Tutorial que muestra cómo incrustar R en SQL Server los procedimientos almacenados y funciones de T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3d2b77d73bb1b8f5d4c507b884d0a09f4647012b
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2018
ms.locfileid: "35250028"
---
# <a name="tutorial-embedded-r-in-stored-procedures-and-t-sql-functions"></a>Tutorial: Incrustar R en los procedimientos almacenados y funciones de T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El objetivo de este tutorial es proporcionar a los programadores SQL con experiencia práctica para crear un solución de SQL Server de aprendizaje automático. En este tutorial, aprenderá cómo incorporar R en una aplicación o solución BI insertando código R en los procedimientos almacenados.

> [!NOTE]
> 
> La misma solución está disponible en Python. Se requiere SQL Server 2017. Vea [en bases de datos análisis para los desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="overview"></a>Información general

El proceso de creación de una solución integral normalmente incluye la obtención y limpieza de los datos, la exploración de los datos y la ingeniería de características, el entrenamiento y la optimización del modelo, y por último la implementación del modelo en producción. Desarrollo y prueba del código real se realiza mejor usar un entorno de desarrollo dedicado. En caso de R, que podría significar RStudio o [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)].

Pero una vez creada la solución puede implementarla fácilmente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el entorno de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]que ya conoce.

En este tutorial, se supone que se le ha proporcionado todo el código de R necesario para la solución y se centran en la creación e implementación de la solución con SQL Server.

- [Lección 1: Descargar los datos de ejemplo y scripts](../tutorials/sqldev-download-the-sample-data.md)

- [Lección 2: Configurar el entorno de tutorial](../r/sqldev-import-data-to-sql-server-using-powershell.md)

- [Lección 3: Explorar y visualizar de forma de datos y la distribución mediante una llamada a funciones de R en los procedimientos almacenados](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [Lección 4: Crear características de datos con R en funciones de T-SQL](../tutorials/sqldev-create-data-features-using-t-sql.md)
  
- [Lección 5: Entrenar y guardar un modelo de R mediante procedimientos almacenados y funciones](../r/sqldev-train-and-save-a-model-using-t-sql.md)
  
- [Lección 6: Código de ajuste R en un procedimiento almacenado para la puesta en marcha](../tutorials/sqldev-operationalize-the-model.md). 
  Después de que el modelo se ha guardado en la base de datos, llame al modelo de predicción desde [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante procedimientos almacenados.

## <a name="scenario"></a>Escenario

Este tutorial usa un conjunto de datos público conocido, en función de viajes en taxis ciudad de Nueva York. Para que el ejemplo de código se ejecute más rápido, creamos una muestra representativa de 1% de los datos. Usará estos datos para crear un modelo de clasificación binaria que predice si un viaje determinado es probable que obtenga una sugerencia o no, en función de las columnas como la hora del día, la distancia y la ubicación de recogida.

## <a name="requirements"></a>Requisitos

Este tutorial supone que está familiarizado con las operaciones de base de datos básicos, como crear bases de datos y tablas, la importación de datos y escribir consultas SQL. No suponga que sabe R. Por lo tanto, se proporciona todo el código de R. Un programador experimentado de SQL puede usar un script de PowerShell proporcionado, datos de ejemplo en GitHub, y [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para completar este ejemplo. 

Antes de iniciar el tutorial:

- Compruebe que dispone de una instancia configurada de [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) o [servicios de aprendizaje de SQL Server 2017 máquina con R habilitado](../install/sql-machine-learning-services-windows-install.md#verify-installation). Además, [confirmar que dispone de las bibliotecas de R](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location).
- El inicio de sesión que utilizas para este tutorial debe tener permisos para crear bases de datos y otros objetos, debe cargar los datos, seleccione datos y ejecutan procedimientos almacenados.

> [!NOTE]
> Te recomendamos que hagas **no** usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para escribir o probar el código de R. Si el código que incrusta en un procedimiento almacenado tiene algún problema, la información que se devuelve desde el procedimiento almacenado es normalmente inadecuada entender la causa del error.
> 
> Para la depuración, se recomienda utilizar una herramienta como [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)], o RStudio. Los scripts de R que se proporcionan en este tutorial ya han sido desarrollados y depurados mediante las herramientas tradicionales de R.

## <a name="next-lesson"></a>Lección siguiente

[Lección 1: Descargar los datos de ejemplo](../tutorials/sqldev-download-the-sample-data.md)
