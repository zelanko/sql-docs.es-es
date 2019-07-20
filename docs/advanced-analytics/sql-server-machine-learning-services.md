---
title: Documentación de machine learning de R y Python
description: R y Python en SQL Server, con modelado de ciencia de datos integrado y algoritmos de aprendizaje automático para el análisis de datos empresariales a escala.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 8eb391ac4b64c93de255214d748c77f44dccb1b3
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344738"
---
# <a name="sql-server-machine-learning-services"></a>Machine Learning Services en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

## <a name="sql-server-machine-learning-services-r-and-python-documentation"></a>Documentación de SQL Server Machine Learning Services (R y Python)

Aprenda a usar bibliotecas y lenguajes externos de R y Python en datos relacionales residentes con nuestras guías de inicio rápido, tutoriales y artículos de procedimientos. Las bibliotecas de R y Python en [SQL Server Machine Learning Services](what-is-sql-server-machine-learning.md) incluyen distribuciones base, modelos de ciencia de datos, algoritmos de aprendizaje automático y funciones para realizar análisis de alto rendimiento a escala, sin tener que transferir datos a través de la Storage.

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
> [!NOTE]
> Para consultar la documentación sobre Java, consulte la documentación de las [extensiones de lenguaje de SQL Server](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview).
::: moniker-end

|   |   |
|---|:--|
| ![Logotipo de R](media/index/logo_r.png) | R de código abierto, ampliado con [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) y los algoritmos de AI de Microsoft en [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package). Estas bibliotecas le proporcionan modelos de previsión y predicción, análisis estadísticos, visualización y manipulación de datos a escala.<br/>La integración de R se inicia en [SQL Server 2016](install/sql-r-services-windows-install.md) y también está disponible en [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| ![Logotipo de Python](media/index/logo_python.png) | Los desarrolladores de Python pueden usar las bibliotecas [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) y [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) de Microsoft para análisis predictivo y aprendizaje automático a escala. Las bibliotecas compatibles con Anaconda y Python 3.5 son la distribución base.<br/>La integración de Python se inicia en [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| &nbsp; | &nbsp; |

## <a name="5-minute-quickstarts"></a>Guías de inicio rápido en 5 minutos

- [Crear un modelo predictivo en R](tutorials/rtsql-create-a-predictive-model-r.md)

- [Predecir y trazar desde el modelo mediante R](tutorials/rtsql-predict-and-plot-from-model.md)

## <a name="step-by-step-tutorials"></a>Tutoriales paso a paso

- [Cómo instalar Machine Learning Services en SQL Server](install/sql-machine-learning-services-windows-install.md)

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
