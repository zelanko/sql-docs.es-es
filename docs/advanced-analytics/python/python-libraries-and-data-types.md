---
title: Bibliotecas de Python | Documentos de Microsoft
ms.custom: 
ms.date: 03/30/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f5ca6889b9f64475d5c2beeba5e15e009bc4710f
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="python-libraries-and-data-types"></a>Tipos de datos y las bibliotecas de Python

En este tema se describe las bibliotecas de Python que se incluyen con los siguientes productos:

+ Equipo con SQL Server (en bases de datos) de servicios de aprendizaje
+ Microsoft Machine Learning Server (independiente)

Este tema también enumeran los tipos de datos no admitidos y tipo de datos de listas de las conversiones que pueden realizarse de forma implícita cuando los datos se pasan entre Python y SQL Server.

## <a name="python-version"></a>Versión de Python

SQL Server de 2017 CTP 2.0 incluye una parte de la distribución de Anaconda y 3.6 de Python.

Un subconjunto de las funciones de RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees, quizá algunas otras) se proporciona mediante la API de Python, utilizando un nuevo paquete de Python **RevoScalePy**. Puede usar este paquete para trabajar con datos utilizando tramas de datos de Pandas. Archivos xdf., o las consultas de datos SQL.

Para obtener más información, consulte [revoscalepy ¿qué es?](what-is-revoscalepy.md).

## <a name="python-and-sql-data-types"></a>Python y tipos de datos SQL

Python es compatible con un número limitado de tipos de datos en comparación con SQL Server.

Como resultado, cada vez que usa los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en scripts de Python, datos pueden convertirse implícitamente a un tipo de datos compatible. Sin embargo, a menudo una conversión exacta no se puede realizar automáticamente y se devuelve un error.

Esta tabla enumeran las conversiones implícitas que se proporcionan. No se admiten otros tipos de datos.

|SQLtype|Tipo de Python|
|-|-|
|**bigint**|`numeric`|
|**binario**|`raw`|
|**bit**|`bool`|
|**char**|`str`|
|**float**|`float64`|
|**int**|`int32`|
|**nchar**|`str`|
|**nvarchar**|`str`|
|**nvarchar(max)**|`str`|
|**real**|`float32`|
|**smallint**|`int16`|
|**tinyint**|`uint8`|
|**varbinary**|`bytes`|
|**varbinary(max)**|`bytes`|
|**varchar(n)**|`str`|
|**ntext**|`str`|



