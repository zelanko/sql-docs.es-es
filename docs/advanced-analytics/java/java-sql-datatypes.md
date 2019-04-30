---
title: Tipos de datos de Java admitidos en SQL Server 2019 - extensiones de lenguaje de SQL Server
description: Asignar tipos de datos de Java para SQL Server para las estructuras de datos de entrada y salida y para los parámetros de entrada en el sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 14a2bc5594b16610dfb8278ab82a9e7b8b22fea6
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473592"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java y SQL Server admiten los tipos de datos

En este artículo asigna los tipos de datos de SQL Server a tipos de datos de Java para estructuras de datos y los parámetros en [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

## <a name="data-types-for-data-sets"></a>Tipos de datos para conjuntos de datos

Actualmente se admiten los siguientes tipos de datos SQL y Java para conjuntos de datos de entrada y salida.


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

## <a name="next-steps"></a>Pasos siguientes

+ [Cómo llamar a Java en SQL Server](howto-call-java-from-sql.md)
+ [Ejemplo de Java en SQL Server](java-first-sample.md)
+ [Extensión del lenguaje Java en SQL Server](extension-java.md)
