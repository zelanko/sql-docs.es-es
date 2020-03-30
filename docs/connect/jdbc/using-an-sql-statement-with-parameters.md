---
title: Empleo de una instrucción SQL con parámetros | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3202b88f-ce13-44dd-982c-c6a3b0260378
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f7b8b3f8b387345d91451c726b7f74a5685913f6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026653"
---
# <a name="using-an-sql-statement-with-parameters"></a>Empleo de una instrucción SQL con parámetros

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para trabajar con los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una instrucción SQL que contiene parámetros IN, puede usar el método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) de la clase [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) para devolver [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), que contiene los datos solicitados. Para ello, primero debe crear un objeto SQLServerPreparedStatement mediante el método [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

Al generar la instrucción SQL, los parámetros IN se especifican mediante el carácter ? (signo de interrogación), que actúa como un marcador de posición para los valores de parámetros que se van a pasar a la instrucción SQL. Para especificar un valor de un parámetro, puede usar uno de los métodos del establecedor de la clase SQLServerPreparedStatement. El método de establecedor usado se determina mediante el tipo de datos del valor que desea pasar a la instrucción SQL.

Al pasar un valor al método de establecedor, debe especificar no sólo el valor real que se va a usar en la instrucción SQL, sino también la posición ordinal del parámetro en la instrucción SQL. Por ejemplo, si la instrucción SQL contiene un solo parámetro, su valor ordinal será 1. Si la instrucción contiene dos parámetros, el primer valor ordinal es 1 y el segundo 2.

En el siguiente ejemplo, se pasa una conexión abierta a la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] a la función, se genera una instrucción SQL preparada y se ejecuta con un solo valor de parámetro String y, luego, se leen los resultados del conjunto de resultados.

[!code[JDBC#UsingSQLWithParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_1_1.java)]

## <a name="see-also"></a>Consulte también

[Empleo de instrucciones con SQL](../../connect/jdbc/using-statements-with-sql.md)
