---
title: 'Conversiones: SQL Server Machine Learning tipos de datos de Python para SQL'
description: Revise el tipo de datos implícitas y explícitas converstions entre Python y SQL Server en soluciones de aprendizaje automático y ciencia de datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9578f81146f0dab42e7a607b9e8ab410313958d4
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/15/2018
ms.locfileid: "53431985"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Asignaciones de tipos de datos entre Python y SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Para las soluciones de Python que se ejecutan en la característica de integración de Python en SQL Server Machine Learning Services, revise la lista de tipos de datos no admitidos y conversiones de tipos de datos que pueden realizarse de forma implícita cuando se pasan datos entre Python y SQL Server.

## <a name="python-version"></a>Versión de Python

Distribución de SQL Server 2017 Anaconda 4.2 y Python 3.6.

Un subconjunto de las funciones de RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees, quizás algunas otras) se proporciona mediante las API de Python, con un nuevo paquete de Python **revoscalepy**. Puede usar este paquete para trabajar con datos mediante consultas de datos SQL, archivos XDF o tramas de datos de Pandas.

Para obtener más información, consulte [módulo revoscalepy en SQL Server](ref-py-revoscalepy.md) y [referencia de funciones de revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

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

## <a name="see-also"></a>Vea también

