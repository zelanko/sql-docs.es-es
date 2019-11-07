---
title: Tipos de datos de Java admitidos en SQL Server 2019
titleSuffix: SQL Server Language Extensions
description: Asigne tipos de datos de Java a SQL Server para las estructuras de datos de entrada y salida, así como para los parámetros de entrada en sp_execute_external_script.
author: dphansen
ms.author: davidph
ms.date: 09/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9daca9c607befe077fcccec20385a36c82b04c6f
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "73588839"
---
# <a name="java-and-sql-server-supported-data-types"></a>Tipos de datos compatibles con Java y SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se asignan tipos de datos de SQL Server a tipos de datos de Java para las estructuras de datos y parámetros en [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

Actualmente se admiten los siguientes tipos de datos de SQL y de Java para los conjuntos de datos de entrada/salida y para los parámetros de entrada y salida.

| Tipo de datos de SQL        | Tipo de datos de Java | Comentario | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| int | INT      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | String      | | |
| nvarchar(n) | String      | | |
| binary(n) | byte[]      | | |
| varbinary(n) | byte[]      | | |
| nvarchar(max) | String      | | |
| varbinary(max) | byte[]      | | |
| UNIQUEIDENTIFIER | String | | |
| char(n) | String | Solo se admiten cadenas UTF8 | |
| varchar(n) | String | Solo se admiten cadenas UTF8 | |
| ntext | String | Solo se admiten cadenas UTF8 | |
| Date | java.sql.date  | | |
| NUMERIC | java.math.BigDecimal  | | |
| Decimal | java.math.BigDecimal  | | |
| money | java.math.BigDecimal  | | |
| SMALLMONEY | java.math.BigDecimal  | | |
| smalldatetime | java.sql.timestamp  | | |
| DATETIME | java.sql.timestamp  | | |
| datetime2 | java.sql.timestamp  | | |


## <a name="next-steps"></a>Pasos siguientes

+ [Cómo llamar a Java en SQL Server](../how-to/call-java-from-sql.md)
