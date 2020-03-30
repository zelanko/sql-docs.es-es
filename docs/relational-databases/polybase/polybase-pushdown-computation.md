---
title: Cálculos de la aplicación en PolyBase | Microsoft Docs
dexcription: Enable pushdown computation to improve performance of queries on your Hadoop cluster. You can select a subset of rows/columns in an external table for pushdown.
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 20039429b5368dc560baba68061c4f42c73b95a1
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "80217130"
---
# <a name="pushdown-computations-in-polybase"></a>Cálculos de la aplicación en PolyBase

## <a name="dmv"></a>DMV

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El cálculo de la aplicación mejora el rendimiento de las consultas en el clúster de Hadoop.

## <a name="enable-pushdown"></a>Habilitar aplicación

En el siguiente artículo se tratan los pasos para habilitar la aplicación:

[Habilitar el cálculo de la aplicación en Hadoop](polybase-configure-hadoop.md#pushdown)

## <a name="select-a-subset-of-rows"></a>Seleccionar un subconjunto de filas

Use la aplicación del predicado para mejorar el rendimiento de una consulta que selecciona un subconjunto de filas de una tabla externa.

En este ejemplo, SQL Server 2016 inicia un trabajo de Map Reduce para recuperar las filas que coinciden con el predicado `customer.account_balance < 200000` en Hadoop. Como la consulta se puede completar correctamente sin examinar todas las filas de la tabla, solo las filas que cumplen los criterios del predicado se copian en SQL Server. Esto ahorra mucho tiempo y exige menos espacio de almacenamiento temporal cuando el número de saldos de cliente < 200000 es pequeño en comparación con el número de clientes con saldos de cuenta > = 200000.

```sql
SELECT * FROM customer WHERE customer.account_balance < 200000
SELECT * FROM SensorData WHERE Speed > 65;  
```

### <a name="select-a-subset-of-columns"></a>Seleccionar un subconjunto de columnas

Use la aplicación del predicado para mejorar el rendimiento de una consulta que selecciona un subconjunto de columnas de una tabla externa.

En esta consulta, SQL Server inicia un trabajo asignar/reducir para preprocesar el archivo de texto delimitado por Hadoop para que únicamente los datos de las dos columnas, customer.name y customer.zip_code, se copien en PDW de SQL Server.

```sql
SELECT customer.name, customer.zip_code FROM customer WHERE customer.account_balance < 200000
```

### <a name="pushdown-for-basic-expressions-and-operators"></a>Aplicación para operadores y expresiones básicas

SQL Server permite las siguientes expresiones básicas y operadores para la aplicación del predicado.

+ Operadores de comparación binarios (\<, >, =, !=, <>, >=, <=) para valores de hora, fecha y numéricos.

+ Operadores aritméticos (+, -, *, /, %).

+ Operadores lógicos (AND, OR).

+ Operadores unarios (NOT, IS NULL, IS NOT NULL).

Los operadores BETWEEN, NOT, IN y LIKE podrían aplicarse. El comportamiento real depende de cómo el optimizador de consultas vuelva a escribir las expresiones de operador como una serie de instrucciones que usan operadores relacionales básicos.

La consulta de este ejemplo tiene varios predicados que se pueden insertar en Hadoop. SQL Server puede insertar trabajos de Map Reduce en Hadoop para ejecutar el predicado `customer.account_balance <= 200000`. La expresión `BETWEEN 92656 and 92677` se compone también de operaciones binarias y lógicas que se pueden insertar en Hadoop. La operación lógica **AND** en `customer.account_balance and customer.zipcode` es una expresión final.

Dada esta combinación de predicados, los trabajos de Map Reduce pueden ejecutar todos la cláusula WHERE. Solo los datos que cumplen los criterios SELECT se vuelven a copiar en PDW de SQL Server.

```sql
SELECT * FROM customer WHERE customer.account_balance <= 200000 AND customer.zipcode BETWEEN 92656 AND 92677
```

## <a name="force-pushdown"></a>Forzar aplicación

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (FORCE EXTERNALPUSHDOWN);
```

## <a name="disable-pushdown"></a>Deshabilitar aplicación

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (DISABLE EXTERNALPUSHDOWN);
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre PolyBase, consulte [¿Qué es PolyBase?](polybase-guide.md)
