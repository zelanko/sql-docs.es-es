---
description: Cálculos de la aplicación en PolyBase
title: Cálculos de la aplicación en PolyBase | Microsoft Docs
dexcription: Enable pushdown computation to improve performance of queries on your Hadoop cluster. You can select a subset of rows/columns in an external table for pushdown.
ms.date: 11/17/2020
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016'
ms.openlocfilehash: 844ab3f2a13e2bd5a9e3ea26d41012a51e7329a4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97416631"
---
# <a name="pushdown-computations-in-polybase"></a>Cálculos de la aplicación en PolyBase

[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

El cálculo de aplicación mejora el rendimiento de las consultas en los orígenes de datos externos. A partir de SQL Server 2016, los cálculos de aplicación han estado disponibles para los orígenes de datos externos de Hadoop. SQL Server 2019 presenta cálculos de aplicación para otros tipos de orígenes de datos externos.

## <a name="enable-pushdown-computation"></a> Habilitar el cálculo de la aplicación

En los artículos siguientes se incluye información sobre la configuración del cálculo de aplicación para tipos específicos de orígenes de datos externos:

- [Habilitar el cálculo de la aplicación en Hadoop](polybase-configure-hadoop.md#pushdown)
- [Configurar PolyBase para acceder a datos externos en Oracle](polybase-configure-oracle.md)
- [Configurar PolyBase para obtener acceso a datos externos en Teradata](polybase-configure-teradata.md)
- [Configurar PolyBase para acceder a datos externos en MongoDB](polybase-configure-mongodb.md)
- [Configuración de PolyBase para acceder a datos externos con tipos genéricos de ODBC](polybase-configure-odbc-generic.md)
- [Configurar PolyBase para acceder a datos externos en SQL Server](polybase-configure-sql-server.md)

## <a name="select-a-subset-of-rows"></a>Seleccionar un subconjunto de filas

Use la aplicación del predicado para mejorar el rendimiento de una consulta que selecciona un subconjunto de filas de una tabla externa.

En este ejemplo, SQL Server 2016 inicia un trabajo de Map Reduce para recuperar las filas que coinciden con el predicado `customer.account_balance < 200000` en Hadoop. Como la consulta se puede completar correctamente sin examinar todas las filas de la tabla, solo las filas que cumplen los criterios del predicado se copian en SQL Server. Esto ahorra mucho tiempo y exige menos espacio de almacenamiento temporal cuando el número de saldos de cliente < 200000 es pequeño en comparación con el número de clientes con saldos de cuenta > = 200000.

```sql
SELECT * FROM customer WHERE customer.account_balance < 200000
SELECT * FROM SensorData WHERE Speed > 65;  
```

### <a name="select-a-subset-of-columns"></a>Seleccionar un subconjunto de columnas

Use la aplicación del predicado para mejorar el rendimiento de una consulta que selecciona un subconjunto de columnas de una tabla externa.

En esta consulta, SQL Server inicia un trabajo de asignación y reducción para preprocesar el archivo de texto delimitado por Hadoop, de tal modo que únicamente los datos de las dos columnas, customer.name y customer.zip_code, se copien en SQL Server.

```sql
SELECT customer.name, customer.zip_code
FROM customer
WHERE customer.account_balance < 200000
```

### <a name="pushdown-for-basic-expressions-and-operators"></a>Aplicación para operadores y expresiones básicas

SQL Server permite las siguientes expresiones básicas y operadores para la aplicación del predicado.

- Operadores de comparación binarios (`<`, `>`, `=`, `!=`, `<>`, `>=` y `<=`) para valores de hora, fecha y numéricos.
- Operadores aritméticos (`+`, `-`, `*`, `/` y `%`).
- Operadores lógicos (`AND` y `OR`).
- Operadores unarios (`NOT`, `IS NULL` y `IS NOT NULL`).

Los operadores `BETWEEN`, `NOT`, `IN` y `LIKE` se pueden insertar. El comportamiento real depende de cómo el optimizador de consultas vuelva a escribir las expresiones de operador como una serie de instrucciones que usan operadores relacionales básicos.

La consulta de este ejemplo tiene varios predicados que se pueden insertar en Hadoop. SQL Server puede insertar trabajos de Map Reduce en Hadoop para ejecutar el predicado `customer.account_balance <= 200000`. La expresión `BETWEEN 92656 AND 92677` se compone también de operaciones binarias y lógicas que se pueden insertar en Hadoop. La operación lógica **AND** en `customer.account_balance AND customer.zipcode` es una expresión final.

Dada esta combinación de predicados, los trabajos de Map Reduce pueden ejecutar todos la cláusula WHERE. Solo los datos que cumplen los criterios `SELECT` se vuelven a copiar en SQL Server.

```sql
SELECT * FROM customer 
WHERE customer.account_balance <= 200000 
    AND customer.zipcode BETWEEN 92656 AND 92677
```

## <a name="examples"></a>Ejemplos

### <a name="force-pushdown"></a>Forzar aplicación

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (FORCE EXTERNALPUSHDOWN);
```

### <a name="disable-pushdown"></a>Deshabilitar aplicación

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (DISABLE EXTERNALPUSHDOWN);
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre PolyBase, consulte [¿Qué es PolyBase?](polybase-guide.md)
