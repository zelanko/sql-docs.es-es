---
title: ¿Qué es SQL Server Machine Learning Services (Python y R)?
titleSuffix: ''
description: Machine Learning Services es una característica de SQL Server que proporciona la capacidad de ejecutar scripts de Python y R con datos relacionales. Para llevar a cabo análisis predictivo y aprendizaje automático, se pueden usar marcos y paquetes de código abierto, además de paquetes de Python y R de Microsoft. Los scripts se ejecutan en la base de datos sin mover los datos fuera de SQL Server o a través de la red. En este artículo se explican los conceptos básicos de SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/07/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fe7a83c66dba9af372e82fc2814828aae32d6a2d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75558294"
---
# <a name="what-is-sql-server-machine-learning-services-python-and-r"></a>¿Qué es SQL Server Machine Learning Services (Python y R)?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Machine Learning Services es una característica de SQL Server que proporciona la capacidad de ejecutar scripts de Python y R con datos relacionales. Para llevar a cabo análisis predictivo y aprendizaje automático, se pueden usar marcos y paquetes de código abierto, además de [paquetes de Python y R de Microsoft](#packages). Los scripts se ejecutan en la base de datos sin mover los datos fuera de SQL Server o a través de la red. En este artículo se explican los conceptos básicos de SQL Server Machine Learning Services.

En Azure SQL Database, [Machine Learning Services](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview) está en versión preliminar pública.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> Para ejecutar Java en SQL Server, consulte la [documentación sobre extensiones de lenguaje](../language-extensions/language-extensions-overview.md).
::: moniker-end

## <a name="what-is-machine-learning-services"></a>¿Qué es Machine Learning Services?

SQL Server Machine Learning Services permite ejecutar scripts de Python y R en la base de datos. Se puede usar para preparar y limpiar los datos, realizar ingeniería de características, y entrenar, evaluar e implementar modelos de aprendizaje automático en una base de datos. La característica ejecuta los scripts donde residen los datos y elimina la transferencia de los datos a otro servidor a través de la red.

Machine Learning Services incluye las distribuciones base de Python y R. Se pueden instalar y usar marcos y paquetes de código abierto, como PyTorch, TensorFlow y scikit-learn, además de los paquetes de Microsoft [revoscalepy](python/ref-py-revoscalepy.md) y [microsoftml](python/ref-py-microsoftml.md) para Python, y [RevoScaleR](r/ref-r-revoscaler.md), [MicrosoftML](r/ref-r-microsoftml.md), [olapr](r/ref-r-olapr.md) y [sqlrutils](r/ref-r-sqlrutils.md) para R.

Machine Learning Services usa un marco de extensibilidad para ejecutar scripts de Python y R en SQL Server. Más información sobre cómo funciona:

+ [Plataforma de extensibilidad](concepts/extensibility-framework.md)
+ [Extensión de Python](concepts/extension-python.md)
+ [Extensión de R](concepts/extension-r.md)

## <a name="what-can-i-do-with-machine-learning-services"></a>¿Qué se puede hacer con Machine Learning Services?

Machine Learning Services puede usarse para compilar y entrenar modelos de aprendizaje automático y de aprendizaje profundo en SQL Server. También es posible implementar modelos existentes en Machine Learning Services y usar datos relacionales para las predicciones.

Estos son algunos de los ejemplos del tipo de predicciones para los que se puede usar SQL Server Machine Learning Services:

|||
|-|-|
|Clasificación o categorización|División automática de los comentarios de los clientes en categorías positivas y negativas|
|Regresión o predicción de valores continuos|Predicción del precio de viviendas en función del tamaño y la ubicación|
|Detección de anomalías|Detección de transacciones bancarias fraudulentas |
|Recomendaciones|Sugerencias de productos que pueden interesar a los compradores en Internet en función de compras anteriores|

### <a name="how-to-execute-python-and-r-scripts"></a>Ejecución de scripts de Python y R

Hay dos maneras de ejecutar scripts de Python y R en Machine Learning Services:

+ La manera más común es usar el procedimiento almacenado de T-SQL [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ También puede usar su cliente de Python o R preferido y escribir scripts que fuercen la ejecución (denominada *contexto de proceso remoto*) en una instancia de SQL Server remota. Vea cómo configurar un cliente de ciencia de datos para [desarrollo de Python](python/setup-python-client-tools-sql.md) y [desarrollo de R](r/set-up-a-data-science-client.md) para obtener más información.

<a name="packages"></a>

## <a name="python-and-r-packages"></a>Paquetes de Python y R

Además de los paquetes de empresa de Microsoft, pueden usarse usar marcos y paquetes de código abierto. Los paquetes de Python y R de código abierto más comunes están preinstalados en Machine Learning Services. También se incluyen los siguientes paquetes de Python y R de Microsoft:

| Idioma | Paquete | Descripción |
|-|-|-|
| Python | [revoscalepy](python/ref-py-revoscalepy.md) | Es el paquete principal para Python escalable. Transformaciones y manipulación de datos, resumen estadístico, visualización y muchas formas de modelado. Además, las funciones de este paquete distribuyen automáticamente las cargas de trabajo entre los núcleos disponibles para su procesamiento paralelo. |
| Python | [microsoftml](python/ref-py-microsoftml.md) | Agrega algoritmos de aprendizaje automático para crear modelos personalizados dedicados al análisis de texto, imágenes y opiniones. | 
| R | [RevoScaleR](r/ref-r-revoscaler.md) | Este es el paquete principal para R escalable. Permite realizar transformaciones y manipulaciones de datos, resúmenes estadísticos, visualizaciones y muchas formas de modelado. Además, las funciones de este paquete distribuyen automáticamente las cargas de trabajo entre los núcleos disponibles para su procesamiento paralelo. |
| R | [MicrosoftML (R)](r/ref-r-microsoftml.md) | Agrega algoritmos de aprendizaje automático para crear modelos personalizados dedicados al análisis de texto, imágenes y opiniones. |
| R | [olapR](r/ref-r-olapr.md) | Se trata de funciones de R usadas para las consultas MDX en un cubo OLAP de SQL Server Analysis Services. |
| R | [sqlrutils](r/ref-r-sqlrutils.md) | Este es un mecanismo para usar scripts de R en un procedimiento almacenado de T-SQL, registrar dicho procedimiento almacenado en una base de datos y ejecutarlo en un [entorno de desarrollo de R](r/set-up-a-data-science-client.md). |
| R | [Microsoft R Open](https://mran.microsoft.com/rro) | Microsoft R Open (MRO) es la distribución mejorada de Microsoft R. Se trata de una plataforma de código abierto completa dedicada al análisis estadístico y la ciencia de datos. Basada en R y compatible al 100 % con ese lenguaje, incluye capacidades adicionales para mejorar el rendimiento y la reproducibilidad. |

Para obtener más información sobre los paquetes que se instalan con Machine Learning Services y cómo instalar otros paquetes, consulte:

+ [Obtención de información de paquetes de Python](package-management/python-package-information.md)
+ [Instalación de paquetes de Python con sqlmlutils](package-management/install-additional-python-packages-on-sql-server.md)
+ [Obtención de información de paquetes de R](package-management/r-package-information.md)
+ [Instalación de nuevos paquetes de R con sqlmlutils](package-management/install-additional-r-packages-on-sql-server.md)

## <a name="how-do-i-get-started-with-machine-learning-services"></a>Primeros pasos con Machine Learning Services

1. [Instalación de SQL Server Machine Learning Services](install/sql-machine-learning-services-windows-install.md)

1. Configure las herramientas de desarrollo. Puede usar:

    + [Azure Data Studio](../azure-data-studio/what-is.md) o [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) para usar T-SQL y el procedimiento almacenado [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) con el fin de ejecutar el script de Python o R script.
    + Python o R en su propio equipo portátil o estación de trabajo de desarrollo para ejecutar scripts. Puede extraer datos de forma local u ordenar la ejecución de forma remota en SQL Server con [revoscalepy](python/ref-py-revoscalepy.md) y [RevoScaleR](r/ref-r-revoscaler.md). Vea cómo configurar un cliente de ciencia de datos para [desarrollo de Python](python/setup-python-client-tools-sql.md) y [desarrollo de R](r/set-up-a-data-science-client.md) para obtener más información.

1. Escriba su primer script de Python o R.

    + Inicio rápido: [Creación y ejecución de scripts de R simples en SQL](tutorials/quickstart-r-create-script.md)
    + Inicio rápido: [Creación y entrenamiento de un modelo predictivo en R](tutorials/quickstart-r-train-score-model.md)
    + Tutorial: [Python en T-SQL](tutorials/sqldev-in-database-python-for-sql-developers.md): explore datos, realice ingeniería de características, entrene e implemente modelos y haga predicciones (serie de cinco partes).
    + Tutorial: [Uso de R en T-SQL](tutorials/sqldev-in-database-r-for-sql-developers.md): explore datos, realice ingeniería de características, entrene e implemente modelos y haga predicciones (serie de cinco partes).
    + Tutorial: [Uso de Machine Learning Services en herramientas de R](tutorials/walkthrough-data-science-end-to-end-walkthrough.md): explore datos, cree gráficos y trazados, realice ingeniería de características, entrene e implemente modelos y haga predicciones (serie de seis partes).

## <a name="next-steps"></a>Pasos siguientes

+ [Instalación de SQL Server Machine Learning Services](install/sql-machine-learning-services-windows-install.md)
+ Configuración de un cliente de ciencia de datos para el [desarrollo de Python](python/setup-python-client-tools-sql.md) y el [desarrollo de R](r/set-up-a-data-science-client.md)
