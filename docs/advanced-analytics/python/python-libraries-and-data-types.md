---
title: Conversiones de tipos de datos de Python a SQL
description: Revise el tipo de datos implícito y explícito converstions entre Python y SQL Server en soluciones de ciencia de datos y aprendizaje automático.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 043a27cc53c2dca955eb0bea1ed07433bc9183b8
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345508"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Asignaciones de tipos de datos entre Python y SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En el caso de las soluciones de Python que se ejecutan en la característica de integración de Python en SQL Server Machine Learning Services, revise la lista de tipos de datos no admitidos y conversiones de tipos de datos que se pueden realizar de forma implícita cuando se pasan datos entre Python y SQL Server.

## <a name="python-version"></a>Versión de Python

SQL Server 2017 Anaconda 4,2 y Python 3,6.

Un subconjunto de la funcionalidad de RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees, quizás algunas otras) se proporciona mediante las API de Python, mediante un nuevo paquete de Python **revoscalepy**. Puede usar este paquete para trabajar con datos mediante tramas de datos de pandas, archivos XDF o consultas de datos SQL.

Para obtener más información, vea [módulo revoscalepy en](ref-py-revoscalepy.md) la [referencia de funciones](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)de SQL Server y revoscalepy.

Python admite un número limitado de tipos de datos en comparación con SQL Server. Como resultado, cada vez que se usan datos de SQL Server en scripts de Python, los datos se pueden convertir implícitamente a un tipo de datos compatible. Sin embargo, a menudo no se puede realizar una conversión exacta automáticamente y se devuelve un error.

## <a name="python-and-sql-data-types"></a>Tipos de datos de Python y SQL

En esta tabla se enumeran las conversiones implícitas que se proporcionan. No se admiten otros tipos de datos.

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

