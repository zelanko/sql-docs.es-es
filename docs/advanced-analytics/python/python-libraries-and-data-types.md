---
title: Tipos de datos y las bibliotecas de Python en SQL Server Machine Learning | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 384c8c94bdef65e41af999848c9bac63fc0c8d40
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43888371"
---
# <a name="python-libraries-and-data-types"></a>Bibliotecas de Python y tipos de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo describe las bibliotecas de Python que se incluyen con SQL Server Machine Learning Services (In-Database) y las instalaciones (independiente).

Este artículo también enumeran los tipos de datos no admitido, y se enumeran las conversiones que pueden realizarse de forma implícita cuando se pasan datos entre Python y SQL Server de tipo de datos.

## <a name="python-version"></a>Versión de Python

Distribución de SQL Server 2017 Anaconda 4.2 y Python 3.6.

Un subconjunto de las funciones de RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees, quizás algunas otras) se proporciona mediante las API de Python, con un nuevo paquete de Python **revoscalepy**. Puede usar este paquete para trabajar con datos mediante consultas de datos SQL, archivos XDF o tramas de datos de Pandas.

Para obtener más información, consulte [revoscalepy What ' s?](what-is-revoscalepy.md).

Python es compatible con un número limitado de tipos de datos en comparación con SQL Server. Como resultado, siempre que use datos de SQL Server en scripts de Python, datos pueden convertirse implícitamente a un tipo de datos compatible. Sin embargo, a menudo una conversión exacta no puede realizarse automáticamente y se devuelve un error.

## <a name="python-and-sql-data-types"></a>Tipos de datos SQL y Python

Esta tabla enumeran las conversiones implícitas que se proporcionan. No se admiten otros tipos de datos.

|SQLtype|Tipo de Python|
|-------|-----------|
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



