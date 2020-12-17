---
title: Tipo de datos de Java
titleSuffix: SQL Server Language Extensions
description: Asigne tipos de datos de Java a SQL Server para las estructuras de datos de entrada y salida, así como para los parámetros de entrada en sp_execute_external_script.
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: d5703470849f627cca87c471ea666b7c1b0e7e85
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471746"
---
# <a name="java-and-sql-server-supported-data-types"></a>Tipos de datos compatibles con Java y SQL Server
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

En este artículo se asignan tipos de datos de SQL Server a tipos de datos de Java para las estructuras de datos y parámetros en [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Actualmente se admiten los siguientes tipos de datos de SQL y de Java para los conjuntos de datos de entrada/salida y para los parámetros de entrada y salida.

| Tipo de datos de SQL        | Tipo de datos de Java | Comentario |
| ------------- |-------------|-|
| bit      | boolean | |
| Tinyint      | short      | |
| Smallint | short      | |
| Int | int      | |
| Real | FLOAT      | |
| Bigint | long      | |
| FLOAT | double      | |
| nchar(n) | String      | |
| nvarchar(n) | String      | |
| binary(n) | byte[]      | |
| varbinary(n) | byte[]      | |
| nvarchar(max) | String      | |
| varbinary(max) | byte[]      | |
| UNIQUEIDENTIFIER | String | |
| char(n) | String | Solo se admiten cadenas UTF8 |
| varchar(n) | String | Solo se admiten cadenas UTF8 |
| ntext | String | Solo se admiten cadenas UTF8 |
| date | java.sql.date  | |
| NUMERIC | java.math.BigDecimal  | |
| Decimal | java.math.BigDecimal  | |
| money | java.math.BigDecimal  | |
| SMALLMONEY | java.math.BigDecimal  | |
| smalldatetime | java.sql.timestamp  | |
| datetime | java.sql.timestamp  | |
| datetime2 | java.sql.timestamp  | |


## <a name="next-steps"></a>Pasos siguientes

+ [Cómo llamar a Java en SQL Server](../how-to/call-java-from-sql.md)