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
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 26c5e6f344d9fb0a14a21fa195214c4460673de0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748516"
---
# <a name="java-and-sql-server-supported-data-types"></a>Tipos de datos compatibles con Java y SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

En este artículo se asignan tipos de datos de SQL Server a tipos de datos de Java para las estructuras de datos y parámetros en [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

Actualmente se admiten los siguientes tipos de datos de SQL y de Java para los conjuntos de datos de entrada/salida y para los parámetros de entrada y salida.

| Tipo de datos de SQL        | Tipo de datos de Java | Comentario | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| Int | int      | | |
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
| date | java.sql.date  | | |
| NUMERIC | java.math.BigDecimal  | | |
| Decimal | java.math.BigDecimal  | | |
| money | java.math.BigDecimal  | | |
| SMALLMONEY | java.math.BigDecimal  | | |
| smalldatetime | java.sql.timestamp  | | |
| datetime | java.sql.timestamp  | | |
| datetime2 | java.sql.timestamp  | | |


## <a name="next-steps"></a>Pasos siguientes

+ [Cómo llamar a Java en SQL Server](../how-to/call-java-from-sql.md)
