---
title: Conversión de tipos de datos de Python y SQL
description: Revise las conversiones implícitas y explícitas de tipos de datos entre Python y SQL Server en soluciones de ciencia de datos y Machine Learning.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/30/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0d1cfed615144b947281b87f88965474e88031d1
ms.sourcegitcommit: d56a834269132a83e5fe0a05b033936776cda8bb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/29/2020
ms.locfileid: "91529492"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Asignaciones de tipos de datos entre Python y SQL Server
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

En el caso de las soluciones de Python que se ejecutan en la característica de integración de Python en SQL Server Machine Learning Services, revise la lista de tipos de datos no admitidos y conversiones de tipos de datos que se pueden realizar implícitamente cuando se pasan datos entre Python y SQL Server.

## <a name="python-version"></a>Versión de Python

Un subconjunto de la funcionalidad de RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees, quizás algunas más) se facilita a través de las API de Python mediante un nuevo paquete de Python: **revoscalepy**. Puede usar este paquete para trabajar con datos mediante tramas de datos de Pandas, archivos XDF o consultas de datos de SQL.

Para más información, vea [Módulo revoscalepy en SQL Server](ref-py-revoscalepy.md) y [Referencia de funciones de revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package).

En comparación con SQL Server, Python admite un número limitado de tipos de datos. Por consiguiente, cada vez que se usan datos de SQL Server en scripts de Python, es posible que los datos se conviertan implícitamente en un tipo de datos compatible. Si bien, a menudo no se puede realizar una conversión exacta automáticamente y se devuelve un error.

## <a name="python-and-sql-data-types"></a>Tipos de datos de SQL y Python

En esta tabla se enumeran las conversiones implícitas que se proporcionan. No se admiten otros tipos de datos.

|Tipo de SQL|Tipo de Python|Descripción
|-------|-----------|---------------------------------------------------------------------------------------------|
|**bigint**|`float64`|
|**binary**|`bytes`|
|**bit**|`bool`|
|**char**|`str`|
|**date**|`datetime`|
|**datetime**|`datetime`|Compatible con SQL Server 2017 CU6 y versiones posteriores (con matrices **NumPy** de tipo `datetime.datetime` o **Pandas** `pandas.Timestamp`). `sp_execute_external_script` ahora admite tipos de `datetime` con fracciones de segundo.|
|**float**|`float64`|
|**int**|`int32`|
|**nchar**|`str`|
|**nvarchar**|`str`|
|**nvarchar(max)**|`str`|
|**real**|`float64`|
|**smalldatetime**|`datetime`|
|**smallint**|`int32`|
|**tinyint**|`int32`|
|**uniqueidentifier**|`str`|
|**varbinary**|`bytes`|
|**varbinary(max)**|`bytes`|
|**varchar(n)**|`str`|
|**ntext**|`str`|
