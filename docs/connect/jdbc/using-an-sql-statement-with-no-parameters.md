---
title: Empleo de una instrucción SQL sin parámetros | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4b0728bd-059b-4b71-895c-999335bc7427
author: MightyPen
ms.author: genemi
ms.openlocfilehash: da4342b8640e89a0183a3f80889dd27ecfb1a76e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026543"
---
# <a name="using-an-sql-statement-with-no-parameters"></a>Empleo de una instrucción SQL sin parámetros

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para trabajar con los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una instrucción SQL que no contenga parámetros, puede usar el método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) para devolver un elemento [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) que contenga los datos solicitados. Para ello, primero debe crear un objeto SQLServerStatement mediante el método [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

En el siguiente ejemplo, se pasa una conexión abierta a la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] a la función, se genera y ejecuta una instrucción SQL y luego se leen los resultados del conjunto de resultados.

[!code[JDBC#UsingSQLWithNoParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_0_1.java)]

Para obtener más información sobre cómo usar conjuntos de resultados, consulte [Administrar conjuntos de resultados con el controlador JDBC](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md).

## <a name="see-also"></a>Consulte también

[Empleo de instrucciones con SQL](../../connect/jdbc/using-statements-with-sql.md)
