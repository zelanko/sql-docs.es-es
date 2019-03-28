---
title: 'Documentación de las extensiones de aprendizaje automático y programación de R y Python: SQL Server Machine Learning'
description: R y Python en SQL Server, con modelado de ciencia de datos integrado y algoritmos de aprendizaje automático para el análisis de datos empresariales a escala.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/10/2019
ms.topic: overview
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 20acdf2789158bf067319930a5be65770eae67f3
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512232"
---
# <a name="sql-server-machine-learning"></a>SQL Server Machine Learning

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"

## <a name="sql-server-machine-learning-and-programming-extensions-documentation"></a>Documentación de las extensiones de aprendizaje automático y programación de SQL Server

Aprenda a usar bibliotecas y lenguajes externos de R y Python en datos relacionales residentes con nuestras guías de inicio rápido, tutoriales y artículos de procedimientos. Las bibliotecas de R y Python en [aprendizaje automático de SQL Server](what-is-sql-server-machine-learning.md) incluyen distribuciones base, modelos de ciencia de datos, algoritmos de aprendizaje automático y funciones para realizar análisis de alto rendimiento a escala, sin tener que transferir datos a través de la red.

En SQL Server 2019, la ejecución de código de Java emplea el mismo marco de extensibilidad que R y Python, pero no incluye bibliotecas de funciones de aprendizaje automático y ciencia de datos. Para más información sobre las nuevas características, consulte [Novedades de SQL Server Machine Learning Services](what-s-new-in-sql-server-machine-learning-services.md).

|   |   |
|---|:--|
| ![Logotipo de R](media/index/logo_r.png) | R de código abierto, ampliado con [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) y los algoritmos de AI de Microsoft en [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package). Estas bibliotecas le proporcionan modelos de previsión y predicción, análisis estadísticos, visualización y manipulación de datos a escala.<br/>La integración de R se inicia en [SQL Server 2016](install/sql-r-services-windows-install.md) y también está disponible en [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| ![Logotipo de Python](media/index/logo_python.png) | Los desarrolladores de Python pueden usar las bibliotecas [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) y [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) de Microsoft para análisis predictivo y aprendizaje automático a escala. Las bibliotecas compatibles con Anaconda y Python 3.5 son la distribución base.<br/>La integración de Python se inicia en [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| ![Logotipo de Java](media/index/logo_java.png) | Los desarrolladores de Java pueden usar la [extensión de lenguaje de Java](java/extension-java.md) para encapsular el código en procedimientos almacenados o en un formato binario accesible mediante Transact-SQL.<br/>La integración de Java se inicia en la [versión preliminar de SQL Server 2019](install/sql-machine-learning-services-ver15.md). |
| &nbsp; | &nbsp; |
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017"

## <a name="sql-server-machine-learning-r-and-python-documentation"></a>Documentación de Python y R de SQL Server Machine Learning

Aprenda a usar bibliotecas y lenguajes externos de R y Python en datos relacionales residentes con nuestras guías de inicio rápido, tutoriales y artículos de procedimientos. Las bibliotecas de R y Python en [aprendizaje automático de SQL Server](what-is-sql-server-machine-learning.md) incluyen distribuciones base, modelos de ciencia de datos, algoritmos de aprendizaje automático y funciones para realizar análisis de alto rendimiento a escala, sin tener que transferir datos a través de la red.

|   |   |
|---|:--|
| ![Logotipo de R](media/index/logo_r.png) | R de código abierto, ampliado con [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) y los algoritmos de AI de Microsoft en [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package). Estas bibliotecas le proporcionan modelos de previsión y predicción, análisis estadísticos, visualización y manipulación de datos a escala.<br/>La integración de R se inicia en [SQL Server 2016](install/sql-r-services-windows-install.md) y también está disponible en [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| ![Logotipo de Python](media/index/logo_python.png) | Los desarrolladores de Python pueden usar las bibliotecas [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) y [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) de Microsoft para análisis predictivo y aprendizaje automático a escala. Las bibliotecas compatibles con Anaconda y Python 3.5 son la distribución base.<br/>La integración de Python se inicia en [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| &nbsp; | &nbsp; |
::: moniker-end

## <a name="5-minute-quickstarts"></a>Guías de inicio rápido en 5 minutos

- [Crear un modelo predictivo en R](tutorials/rtsql-create-a-predictive-model-r.md)

- [Predecir y trazar desde el modelo mediante R](tutorials/rtsql-predict-and-plot-from-model.md)

## <a name="step-by-step-tutorials"></a>Tutoriales paso a paso

- [Cómo agregar aprendizaje automático y el marco de extensibilidad a SQL Server](install/sql-machine-learning-services-windows-install.md)

- [Cómo ejecutar R desde T-SQL y los procedimientos almacenados](tutorials/sqldev-in-database-r-for-sql-developers.md)

- [Cómo usar análisis integrado en Python](tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="video-introduction"></a>Vídeo de introducción

> [!VIDEO https://www.youtube.com/embed/ACejZ9optCQ]

## <a name="reference"></a>Referencia

| Paquete | Lenguaje | Descripción |
|:--------|:---------|:------------|
| [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) | R | Procesamiento distribuido y en paralelo de tareas de R: transformación de datos, exploración, visualización, análisis estadístico y predictivo. |
| [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package) | R | Funciones basadas en algoritmos de inteligencia artificial de Microsoft, adaptadas para R. |
| [olapR](/machine-learning-server/r-reference/olapr/olapr) | R | Importa datos de cubos de OLAP. |
| [sqlRUtils](/machine-learning-server/r-reference/sqlrutils/sqlrutils) | R | Funciones auxiliares para encapsular R y T-SQL. |
[revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Python | Procesamiento distribuido y en paralelo de tareas de Python: transformación de datos, exploración, visualización, análisis estadístico y predictivo. |
| [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Python | Funciones basadas en algoritmos de inteligencia artificial de Microsoft, adaptadas para Python. |
| &nbsp; | &nbsp; | &nbsp; |
