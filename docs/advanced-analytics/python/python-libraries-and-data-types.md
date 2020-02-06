---
title: Conversión de tipos de datos de Python y SQL
description: Revise las conversiones implícitas y explícitas de tipos de datos entre Python y SQL Server en soluciones de ciencia de datos y Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f22f838bc78d4791e73a1d107cd253aae314d205
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727516"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Asignaciones de tipos de datos entre Python y SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En el caso de las soluciones de Python que se ejecutan en la característica de integración de Python en SQL Server Machine Learning Services, revise la lista de tipos de datos no admitidos y conversiones de tipos de datos que se pueden realizar implícitamente cuando se pasan datos entre Python y SQL Server.

## <a name="python-version"></a>Versión de Python

Un subconjunto de la funcionalidad de RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees, quizás algunas más) se facilita a través de las API de Python mediante un nuevo paquete de Python: **revoscalepy**. Puede usar este paquete para trabajar con datos mediante tramas de datos de Pandas, archivos XDF o consultas de datos de SQL.

Para más información, vea [Módulo revoscalepy en SQL Server](ref-py-revoscalepy.md) y [Referencia de funciones de revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

En comparación con SQL Server, Python admite un número limitado de tipos de datos. Por consiguiente, cada vez que se usan datos de SQL Server en scripts de Python, es posible que los datos se conviertan implícitamente en un tipo de datos compatible. Si bien, a menudo no se puede realizar una conversión exacta automáticamente y se devuelve un error.

## <a name="python-and-sql-data-types"></a>Tipos de datos de SQL y Python

En esta tabla se enumeran las conversiones implícitas que se proporcionan. No se admiten otros tipos de datos.

|Tipo de SQL|Tipo de Python|
|-------|-----------|
|**bigint**|`numeric`|
|**binary**|`raw`|
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
