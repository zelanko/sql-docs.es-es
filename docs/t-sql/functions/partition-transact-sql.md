---
title: $PARTITION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- $partition_TSQL
- $partition
dev_langs:
- TSQL
helpviewer_keywords:
- $PARTITION function
- partitions [SQL Server], numbers
ms.assetid: abc865d0-57a8-49da-8821-29457c808d2a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 74287e364736b4a1d09711b20817a9a0b0c694c2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47839543"
---
# <a name="partition-transact-sql"></a>$PARTITION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el número de partición al que se asignaría un conjunto de valores de columnas de partición para cualquier función de partición especificada en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
[ database_name. ] $PARTITION.partition_function_name(expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Es el nombre de la base de datos que contiene la función de partición.  
  
 *partition_function_name*  
 Es el nombre de cualquier función de partición existente con la que se está aplicando un conjunto de valores de columnas de partición.  
  
 *expression*  
 Es una [expression](../../t-sql/language-elements/expressions-transact-sql.md) cuyo tipo de datos debe coincidir con el tipo de datos de su columna de partición correspondiente, o debe poder convertirse a dicho tipo de datos de forma implícita. *expression* también puede ser el nombre de una columna de partición que participa en ese momento en *partition_function_name*.  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="remarks"></a>Notas  
 $PARTITION devuelve un valor **int** entre 1 y el número de particiones de la función de partición.  
  
 $PARTITION devuelve el número de partición de cualquier valor válido, independientemente de si el valor existe en ese momento en una tabla o índice con particiones que utilice la función de partición.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-getting-the-partition-number-for-a-set-of-partitioning-column-values"></a>A. Obtener el número de partición de un conjunto de valores de columnas de partición  
 En el siguiente ejemplo se crea una función de partición `RangePF1` que realizará cuatro particiones en una tabla o un índice. $PARTITION se utiliza para determinar que el valor `10`, que representa la columna de partición de `RangePF1`, se colocaría en la partición 1 de la tabla.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE PARTITION FUNCTION RangePF1 ( int )  
AS RANGE FOR VALUES (10, 100, 1000) ;  
GO  
SELECT $PARTITION.RangePF1 (10) ;  
GO  
```  
  
### <a name="b-getting-the-number-of-rows-in-each-nonempty-partition-of-a-partitioned-table-or-index"></a>B. Obtener el número de filas de cada partición no vacía de una tabla o un índice con particiones  
 En el siguiente ejemplo se devuelve el número de filas de cada partición de la tabla `TransactionHistory` que contiene datos. La tabla `TransactionHistory` utiliza la función de partición `TransactionRangePF1`. Además, se crean particiones en la columna `TransactionDate`.  
  
 Para ejecutar este ejemplo, primero hay que ejecutar el script PartitionAW.sql en la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Para más información, vea [PartitioningScript](http://go.microsoft.com/fwlink/?LinkId=201015).  
  
```  
USE AdventureWorks2012;  
GO  
SELECT $PARTITION.TransactionRangePF1(TransactionDate) AS Partition,   
COUNT(*) AS [COUNT] FROM Production.TransactionHistory   
GROUP BY $PARTITION.TransactionRangePF1(TransactionDate)  
ORDER BY Partition ;  
GO  
```  
  
### <a name="c-returning-all-rows-from-one-partition-of-a-partitioned-table-or-index"></a>C. Devolver todas las filas de una partición de una tabla o un índice con particiones  
 En el siguiente ejemplo se devuelven todas las filas que se encuentran en la partición `5` de la tabla `TransactionHistory`.  
  
> [!NOTE]  
>  Para ejecutar este ejemplo, primero hay que ejecutar el script PartitionAW.sql en la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Para más información, vea [PartitioningScript](http://go.microsoft.com/fwlink/?LinkId=201015).  
  
```  
SELECT * FROM Production.TransactionHistory  
WHERE $PARTITION.TransactionRangePF1(TransactionDate) = 5 ;  
```  
  
## <a name="see-also"></a>Ver también  
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)  
  
  
