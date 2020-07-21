---
title: Empleo de una instrucción SQL para modificar objetos de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f49ea499-df3c-4e85-9fc7-450fb99622a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de8e357328c151e3762f324dcbeba2525df53530
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026563"
---
# <a name="using-an-sql-statement-to-modify-database-objects"></a>Empleo de una instrucción SQL para modificar objetos de base de datos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para modificar objetos de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante una instrucción SQL, puede usar el método [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). El método executeUpdate pasa la instrucción SQL a la base de datos para su procesamiento y luego devuelve un valor de 0 porque no se ha visto afectada ninguna fila.

Para ello, primero debe crear un objeto SQLServerStatement mediante el método [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

> [!NOTE]  
> Las instrucciones SQL que modifican objetos dentro de una base de datos, se llaman instrucciones de lenguaje de definición de datos (DDL). Estas incluyen instrucciones como `CREATE TABLE`, `DROP TABLE`, `CREATE INDEX`, y `DROP INDEX`. Para obtener más información sobre los tipos de instrucciones DDL compatibles con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

En el siguiente ejemplo, se pasa a la función una conexión abierta a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)], se construye una instrucción SQL que crea el elemento TestTable simple en la base de datos y luego se ejecuta la instrucción y se muestra el valor devuelto.

[!code[JDBC#UsingSQLToModifyDBObjects1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_0_1.java)]

## <a name="see-also"></a>Consulte también

[Empleo de instrucciones con SQL](../../connect/jdbc/using-statements-with-sql.md)
