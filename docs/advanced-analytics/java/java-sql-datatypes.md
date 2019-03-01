---
title: 'Tipos de datos de Java admitidos en SQL Server 2019: SQL Server Machine Learning Services'
description: Asignar tipos de datos de Java para SQL Server para las estructuras de datos de entrada y salida y para los parámetros de entrada en el sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4c0f691b8bb389c2da2001d19f0684b7f928f707
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017821"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java y SQL Server admiten los tipos de datos

En este artículo asigna los tipos de datos de SQL Server a tipos de datos de Java para estructuras de datos y los parámetros en [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

## <a name="data-types-for-data-sets"></a>Tipos de datos para conjuntos de datos

Actualmente se admiten los siguientes tipos de datos SQL y Java para conjuntos de datos de entrada y salida.

| Tipo de datos SQL        | Tipo de datos de Java | Comentario | |
| ------------- |-------------|-|
| bit      | boolean | |
| Tinyint      | short      | |
| Smallint | short      | |
| int | INT      | |
| Real | FLOAT      | |
| Bigint | long      | |
| FLOAT | double      | |
| nchar(n) | String      | |
| nvarchar(n) | String  | |
| binary(n) | byte[]      | |
| varbinary (n) | byte[]      | |
| nvarchar(max) | String | |
| varbinary(max) | byte[] | |
| UNIQUEIDENTIFIER | String | |
| char(n) | String | Solo se admiten cadenas de UTF8 |
| varchar(n) | String | Solo se admiten cadenas de UTF8 |
| ntext | String | Solo se admiten cadenas de UTF8 |

## <a name="data-types-for-input-parameters"></a>Tipos de datos para los parámetros de entrada

Actualmente se admiten los siguientes tipos de datos SQL y Java para parámetros de entrada.

| Tipo de datos SQL        | Tipo de datos de Java | Comentario | |
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
| varbinary (n) | byte[]      | | |
| nvarchar(max) | String      | | |
| varbinary(max) | byte[]      | | |
| UNIQUEIDENTIFIER | String | | |
| char(n) | String | Solo se admiten cadenas de UTF8 | |
| varchar(n) | String | Solo se admiten cadenas de UTF8 | |
| ntext | String | Solo se admiten cadenas de UTF8 | |

## <a name="see-also"></a>Vea también

+ [Cómo llamar a Java en SQL Server](howto-call-java-from-sql.md)
+ [Ejemplo de Java en SQL Server](java-first-sample.md)
+ [Extensión del lenguaje Java en SQL Server](extension-java.md)