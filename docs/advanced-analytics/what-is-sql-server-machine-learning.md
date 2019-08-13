---
title: ¿Qué es SQL Server Machine Learning Services (Python y R)?
titleSuffix: ''
description: Machine Learning Services es una característica de SQL Server que proporciona la capacidad de ejecutar scripts de Python y R con datos relacionales. Puede usar los paquetes y marcos de código abierto y los paquetes de Microsoft Python y R para el análisis predictivo y el aprendizaje automático. Los scripts se ejecutan en la base de datos sin mover los datos fuera de SQL Server o a través de la red. En este artículo se explican los conceptos básicos de SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/07/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4a1a9a3b0f712458466051ce2c67c0a725ef0a76
ms.sourcegitcommit: 12b7e3447ca2154ec2782fddcf207b903f82c2c0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957437"
---
# <a name="what-is-sql-server-machine-learning-services-python-and-r"></a>¿Qué es SQL Server Machine Learning Services (Python y R)?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Machine Learning Services es una característica de SQL Server que proporciona la capacidad de ejecutar scripts de Python y R con datos relacionales. Puede usar los paquetes y marcos de código abierto y los paquetes de [Microsoft Python y R](#packages) para el análisis predictivo y el aprendizaje automático. Los scripts se ejecutan en la base de datos sin mover los datos fuera de SQL Server o a través de la red. En este artículo se explican los conceptos básicos de SQL Server Machine Learning Services.

En Azure SQL Database, [Machine Learning Services](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview) se encuentra actualmente en versión preliminar pública.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> Para ejecutar Java en SQL Server, consulte la [documentación de las extensiones de lenguaje](../language-extensions/language-extensions-overview.md).
::: moniker-end

## <a name="what-is-machine-learning-services"></a>¿Qué es Machine Learning Services?

SQL Server Machine Learning Services permite ejecutar scripts de Python y R en la base de datos. Puede utilizarlo para preparar y limpiar los datos, realizar ingeniería de características y entrenar, evaluar e implementar modelos de aprendizaje automático en una base de datos. La característica ejecuta los scripts donde residen los datos y elimina la transferencia de los datos a través de la red a otro servidor.

Las distribuciones base de Python y R se incluyen en Machine Learning Services. Puede usar marcos y paquetes de código abierto, como PyTorch, TensorFlow y scikit-Learn, además de los paquetes de Microsoft [revoscalepy](python/ref-py-revoscalepy.md) y [microsoftml](python/ref-py-microsoftml.md) para Python, y [RevoScaleR](r/ref-r-revoscaler.md), [microsoftml](r/ref-r-microsoftml.md), [olapr ](r/ref-r-olapr.md)y [Sqlrutils](r/ref-r-sqlrutils.md) para R.

Machine Learning Services usa un marco de extensibilidad para ejecutar scripts de Python y R en SQL Server. Más información sobre cómo funciona:

+ [Marco de extensibilidad](concepts/extensibility-framework.md)
+ [Extensión de Python](concepts/extension-python.md)
+ [Extensión de R](concepts/extension-r.md)

## <a name="what-can-i-do-with-machine-learning-services"></a>¿Qué puedo hacer con Machine Learning Services?

Puede usar Machine Learning Services para compilar y entrenar modelos de aprendizaje automático y aprendizaje profundo en SQL Server. También puede implementar modelos existentes para Machine Learning Services y usar datos relacionales para las predicciones.

Entre los ejemplos del tipo de predicciones que puede usar SQL Server Machine Learning Services para, se incluyen:

|||
|-|-|
|Clasificación/categorización|Dividir automáticamente los comentarios de los clientes en categorías positivas y negativas|
|Valores continuos de regresión y predicción|Predecir el precio de las casas en función del tamaño y la ubicación|
|Detección de anomalías|Detectar transacciones bancarias fraudulentas |
|Recomendaciones|Sugiera productos que los compradores en línea pueden querer comprar, en función de las compras anteriores|

### <a name="how-to-execute-python-and-r-scripts"></a>Cómo ejecutar scripts de Python y R

Hay dos maneras de ejecutar scripts de Python y R en Machine Learning Services:

+ La manera más común es usar el procedimiento almacenado [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)de T-SQL.

+ También puede usar el cliente de Python o R que prefiera y escribir scripts que inserten la ejecución (denominada *contexto de cálculo remoto*) en un SQL Server remoto. Vea cómo configurar un cliente de ciencia de datos para el [desarrollo de Python](python/setup-python-client-tools-sql.md) y desarrollo de [R](r/set-up-a-data-science-client.md) para obtener más información.

<a name="packages"></a>

## <a name="python-and-r-packages"></a>Paquetes de Python y R

Puede usar los paquetes y marcos de código abierto, además de los paquetes de empresa de Microsoft. Los paquetes de Python y R de código abierto más comunes están preinstalados en Machine Learning Services. También se incluyen los siguientes paquetes de Python y R de Microsoft:

| Lenguaje | Paquete | Descripción |
|-|-|-|
| Python | [revoscalepy](python/ref-py-revoscalepy.md) | Paquete principal para Python escalable. Transformaciones y manipulación de datos, resumen estadístico, visualización y muchas formas de modelado. Además, las funciones de este paquete distribuyen automáticamente las cargas de trabajo entre los núcleos disponibles para el procesamiento en paralelo. |
| Python | [microsoftml](python/ref-py-microsoftml.md) | Agrega algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de texto, el análisis de imágenes y el análisis de opiniones. | 
| R | [RevoScaleR](r/ref-r-revoscaler.md) | Paquete principal para transformaciones y manipulaciones de datos de R escalables, resumen estadístico, visualización y muchas formas de modelado. Además, las funciones de este paquete distribuyen automáticamente las cargas de trabajo entre los núcleos disponibles para el procesamiento en paralelo. |
| R | [MicrosoftML (R)](r/ref-r-microsoftml.md) | Agrega algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de texto, el análisis de imágenes y el análisis de opiniones. |
| R | [olapR](r/ref-r-olapr.md) | Funciones de R utilizadas para las consultas MDX en un cubo OLAP de SQL Server Analysis Services. |
| R | [sqlrutils](r/ref-r-sqlrutils.md) | Un mecanismo para usar scripts de R en un procedimiento almacenado de T-SQL, registrar ese procedimiento almacenado en una base de datos y ejecutar el procedimiento almacenado desde un [entorno de desarrollo de R](r/set-up-a-data-science-client.md). |
| R | [Microsoft R Open](https://mran.microsoft.com/rro) | Microsoft R Open (MRO) es la distribución mejorada de R de Microsoft. Es una plataforma de código abierto completa para el análisis estadístico y la ciencia de datos. Se basa en y 100% compatible con R e incluye capacidades adicionales para mejorar el rendimiento y la reproducibilidad. |

## <a name="how-do-i-get-started-with-machine-learning-services"></a>Cómo Introducción a Machine Learning Services?

1. [Instalar SQL Server Machine Learning Services](install/sql-machine-learning-services-windows-install.md)

1. Configure las herramientas de desarrollo. Puede usar:

    + [Azure Data Studio](../azure-data-studio/what-is.md) o [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) para usar T-SQL y el procedimiento almacenado [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para ejecutar el script de Python o R.
    + Python o R en su propio equipo portátil o estación de trabajo de desarrollo para ejecutar scripts. Puede extraer datos de forma local o insertar la ejecución de forma remota en SQL Server con [revoscalepy](python/ref-py-revoscalepy.md) y [RevoScaleR](r/ref-r-revoscaler.md). Vea cómo configurar un cliente de ciencia de datos para el [desarrollo de Python](python/setup-python-client-tools-sql.md) y desarrollo de [R](r/set-up-a-data-science-client.md) para obtener más información.

1. Escribir el primer script de Python o R

    + Inicio rápido: Ejecutar un script "Hello World" [en Python](tutorials/quickstart-python-run-using-t-sql.md) o [en R](tutorials/quickstart-r-run-using-tsql.md)
    + Inicio rápido: Creación de un modelo predictivo [en Python](tutorials/quickstart-python-train-score-in-tsql.md) o [en R](tutorials/quickstart-r-create-predictive-model.md)
    + Tutorial: [Usar Python en T-SQL](tutorials/sqldev-in-database-python-for-sql-developers.md): Explorar datos, realizar ingeniería de características, entrenar e implementar modelos y realizar predicciones (serie de cinco partes)
    + Tutorial: [Uso de R en T-SQL](tutorials/sqldev-in-database-r-for-sql-developers.md): Explorar datos, realizar ingeniería de características, entrenar e implementar modelos y realizar predicciones (serie de cinco partes)
    + Tutorial: [Use Machine Learning Services en herramientas de R](tutorials/walkthrough-data-science-end-to-end-walkthrough.md): Explorar datos, crear gráficos y trazados, realizar ingeniería de características, entrenar e implementar modelos y realizar predicciones (serie de seis partes)

## <a name="next-steps"></a>Pasos siguientes

+ [Instalar SQL Server Machine Learning Services](install/sql-machine-learning-services-windows-install.md)
+ Configuración de un cliente de ciencia de datos para el [desarrollo de Python](python/setup-python-client-tools-sql.md) y [desarrollo de R](r/set-up-a-data-science-client.md)
