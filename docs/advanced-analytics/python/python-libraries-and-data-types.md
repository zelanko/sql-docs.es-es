---
title: Tipos de datos y las bibliotecas de Python en aprendizaje automático de SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f8dfa7f343a3a179b05b624a083238e08011c4a5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="python-libraries-and-data-types"></a>Tipos de datos y las bibliotecas de Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo describen las bibliotecas de Python que se incluye con servicios de aprendizaje de máquina (en bases de datos) de SQL Server y las instalaciones (independiente).

Este artículo también enumeran los tipos de datos no admitidos y tipo de datos de listas de las conversiones que pueden realizarse de forma implícita cuando los datos se pasan entre Python y SQL Server.

## <a name="python-version"></a>Versión de Python

SQL Server de 2017 CTP 2.0 incluye una parte de la distribución de Anaconda y 3.6 de Python.

Un subconjunto de las funciones de RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees, quizá algunas otras) se proporciona mediante la API de Python, utilizando un nuevo paquete de Python **revoscalepy**. Puede usar este paquete para trabajar con datos mediante consultas de datos SQL, archivos xdf. o tramas de datos de Pandas.

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



