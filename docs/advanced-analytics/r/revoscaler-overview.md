---
title: RevoScaleR | Documentos de Microsoft
ms.custom: 
ms.date: 11/29/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 6df09f4ff1541ac0458013d55fbe643c4f0cc8d6
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="revoscaler"></a>RevoScaleR

RevoScaleR es un paquete de funciones de aprendizaje de máquina, proporcionado por Microsoft, que admite la ciencia de datos a escala.

+ Las funciones admiten la importación de datos, transformación de datos, resumen, visualización y análisis.

+ _A escala_ significa que las operaciones se pueden realizar con grandes conjuntos de datos en paralelo y distribuidas en los sistemas de archivos. Algoritmos pueden operar en conjuntos de datos que no caben en la memoria, mediante fragmentación y volver a montar los resultados cuando operaciones se completan.

+ RevoScaleR proporciona muchas mejoras con respecto a las funciones de R de código abierto. Hay funciones de RevoScaleR correspondiente a muchas de las funciones de R de base más populares. Funciones de RevoScaleR se denotan con un **rx** o **Rx** prefijo para que sean fáciles de identificar.

+ RevoScaleR actúa como una plataforma para la ciencia de datos distribuidos. Por ejemplo, puede utilizar las transformaciones y los contextos de proceso de RevoScaleR con los algoritmos de última generación en [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package). También puede usar [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) para ejecutar funciones de R base en paralelo.

Para obtener ejemplos de RevoScaleR en acción, vea estos blogs: 

+ [Compilar e implementar un modelo de predicción mediante R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [Predicciones de un millón por segundo con el servidor de aprendizaje de máquina](https://blogs.msdn.microsoft.com/mlserver/2017/10/15/1-million-predictionssec-with-machine-learning-server-web-service/)

+ [Predecir taxi las sugerencias MicrosoftML](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/01/17/predicting-nyc-taxi-tips-using-microsoftml/)

+ [Optimización del rendimiento con rxExec](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/11/14/performance-optimization-when-using-rxexec-to-parallelize-algorithms/)

## <a name="how-to-get-revoscaler"></a>Cómo obtener RevoScaleR

El paquete RevoScaleR para R se instala de forma gratuita en el cliente de Microsoft R. Si tiene servidores de aprendizaje de máquina o usa R en SQL Server, RevoScaleR se incluye de forma predeterminada.

Si usas Python, el [revoscalepy](../python/what-is-revoscalepy.md) paquete proporciona una funcionalidad equivalente.

> [!IMPORTANT]
> El paquete RevoScaleR no puede ser descargado o utilizarse independientemente de los productos y servicios que proporcionan dichos.

## <a name="use-revoscaler-in-sql-server"></a>Usar RevoScaleR en SQL Server

Estos tutoriales y ejemplos muestran cómo utilizar las funciones de RevoScaleR para obtener datos de SQL Server, crear modelos y guardar modelos en una base de datos para puntuar.

+ [Aprender a usar los contextos de proceso](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R para desarrolladores de SQL: entrenar y poner un modelo](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Muestras de productos de Microsoft en GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)

## <a name="learn-more-about-revoscaler"></a>Obtener más información sobre RevoScaleR

Estos tutoriales muestran el uso de RevoScaleR en otros contextos de proceso admitidas [servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), incluidos los Hadoop.

+ [¿Qué es RevoScaleR?](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler)

+ [Explorar RevoScaleR en 25 funciones](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)

+ [Referencia del paquete RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)

