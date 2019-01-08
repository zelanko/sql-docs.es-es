---
title: 'Tipos de datos de Java admitidos en SQL Server 2019: SQL Server Machine Learning Services'
description: Asignar tipos de datos de Java para SQL Server para las estructuras de datos de entrada y salida y para los parámetros de entrada en el sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6921a40efc9af3ef94c0a53f8409891fee16127e
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432538"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java y SQL Server admiten los tipos de datos

En este artículo asigna los tipos de datos de SQL Server a tipos de datos de Java para estructuras de datos y los parámetros en [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

## <a name="data-types-for-data-sets"></a>Tipos de datos para conjuntos de datos

Actualmente se admiten los siguientes tipos de datos SQL y Java para conjuntos de datos de entrada y salida.

| Tipo de SQL        | Tipo de Java | | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| int | INT      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | Cadena (unicode)      | | |
| nvarchar (n) | Cadena (unicode)      | | |
| binary(n) | byte[]      | | |
| varbinary (n) | byte[]      | | |

## <a name="data-types-for-input-parameters"></a>Tipos de datos para los parámetros de entrada

Actualmente se admiten los siguientes tipos de datos SQL y Java para parámetros de entrada.

| Tipo de SQL        | Tipo de Java | | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| int | INT      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | Cadena (unicode)      | | |
| nvarchar (n) | Cadena (unicode)      | | |
| binary(n) | byte[]      | | |
| varbinary (n) | byte[]      | | |
| nvarchar(max) | Cadena (unicode)      | | |
| varbinary(max) | byte[]      | | |

## <a name="see-also"></a>Vea también

+ [Cómo llamar a Java en SQL Server](howto-call-java-from-sql.md)
+ [Ejemplo de Java en SQL Server](java-first-sample.md)
+ [Extensión del lenguaje Java en SQL Server](extension-java.md)