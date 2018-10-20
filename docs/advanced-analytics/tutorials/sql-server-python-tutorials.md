---
title: Tutoriales de Python de SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5cafb253cea118148bd654ea770234843f742838
ms.sourcegitcommit: b1990ec4491b5a8097c3675334009cb2876673ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/17/2018
ms.locfileid: "49383340"
---
# <a name="sql-server-python-tutorials"></a>Tutoriales de Python de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se proporciona una lista de tutoriales y ejemplos que muestran el uso de Python con SQL Server 2017. A través de estos ejemplos y demostraciones, aprenderá lo siguiente:

+ Ejecución de Python desde T-SQL
+ ¿Cuáles son los contextos de cálculo locales y remotos, y cómo pueden ejecutar código de Python con el equipo de SQL Server
+ Cómo ajustar el código de Python en un procedimiento almacenado
+ Optimizar el código de Python para un entorno de producción de SQL
+ Escenarios del mundo real para la incrustación en aplicaciones de aprendizaje automático

Para obtener información sobre los requisitos y el programa de instalación, consulte [requisitos previos](#bkmk_Prerequisites).

## <a name="bkmk_pythontutorials"></a>Tutoriales de Python

+ [Ejecutar Python en T-SQL](run-python-using-t-sql.md)

   Obtenga información sobre los conceptos básicos de cómo llamar a Python en T-SQL, mediante el mecanismo de extensibilidad introducidas por primera vez en SQL Server 2016.

+ [Crear un modelo de machine learning en Python mediante revoscalepy](use-python-revoscalepy-to-create-model.md)

   En esta lección se muestra cómo ejecutar el código desde un terminal de Python remoto, utilizando el contexto de proceso de SQL Server. Debe estar un poco familiarizado con los entornos y herramientas de Python. Código de ejemplo es que crea un modelo con **rxLinMod**, desde el nuevo **revoscalepy** biblioteca. 

+ [Análisis de Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md)

    En este tutorial de extremo a extremo muestra el proceso de creación de una solución completa de Python mediante procedimientos almacenado de Transact-SQL. Se incluye todo el código Python.


## <a name="python-samples"></a>Ejemplos de Python

Estos ejemplos y demostraciones proporcionadas por el equipo de desarrollo de SQL Server resaltan formas en que puede usar análisis insertados en aplicaciones del mundo real.

+ [Crear un modelo predictivo con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  Obtenga información sobre cómo una empresa de alquiler de esquís puede usar el aprendizaje automático para predecir alquileres futuros, que permite el plan de negocio y personal para satisfacer la demanda futura.

  > [!TIP]
  > ¡Ahora incluye la puntuación nativa de modelos de Python!

+ [Realizar el cliente agrupación en clústeres con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Obtenga información sobre cómo usar el algoritmo de Kmeans para realizar una agrupación en clústeres no supervisado de los clientes.

## <a name="see-also"></a>Vea también

[Tutoriales de R para SQL Server](sql-server-r-tutorials.md)
