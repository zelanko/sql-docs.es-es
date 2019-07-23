---
title: Usar un procedimiento almacenado con un estado de devolución | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4b126e95-8458-41d6-af37-fc6662859f19
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eb5654563a0894abd497dfb0053b3e5667bf433d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916515"
---
# <a name="using-a-stored-procedure-with-a-return-status"></a>Usar un procedimiento almacenado con un estado de devolución

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Un procedimiento almacenado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al que puede llamar es el que devuelve un parámetro de estado o resultado. Se usa normalmente para indicar el funcionamiento correcto o incorrecto del procedimiento almacenado. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), que puede usar para llamar a este tipo de procedimiento almacenado y procesar los datos que devuelve.

Al llamar a este tipo de procedimiento almacenado mediante el controlador JDBC, debe usar la secuencia de escape `call` de SQL junto con el método [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). La sintaxis de la secuencia de escape `call` con un parámetro de estado de devolución es la siguiente:

`{[?=]call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> Para obtener más información sobre las secuencias de escape de SQL, vea [usar secuencias de escape de SQL](../../connect/jdbc/using-sql-escape-sequences.md).

Al crear la secuencia de escape `call`, especifique el parámetro de estado de devolución mediante el carácter ? (signo de interrogación). Este carácter actúa como un marcador de posición para el valor del parámetro que devolverá el procedimiento almacenado. Para especificar un valor para un parámetro de estado de devolución, debe especificar el tipo de datos del parámetro mediante el método [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) de la clase SQLServerCallableStatement antes de ejecutar el procedimiento almacenado.

> [!NOTE]  
> Al usar el controlador JDBC con una base de datos de SQL Server, el valor especificado para el parámetro de estado de devolución del método registerOutParameter siempre es un entero, que se puede especificar mediante el tipo de datos java.sql.Types.INTEGER.

Además, al pasar un valor al método registerOutParameter para un parámetro de estado de devolución, debe especificar no solo el tipo de datos usado para el parámetro, sino también la posición ordinal del parámetro en la llamada al procedimiento almacenado. En el caso del parámetro de estado de devolución, su posición ordinal siempre es 1 debido a que es siempre el primer parámetro de la llamada al procedimiento almacenado. Aunque la clase SQLServerCallableStatement proporciona compatibilidad para usar el nombre del parámetro para indicar el parámetro concreto, puede usar el número de la posición ordinal de solo un parámetro para los parámetros de estado de devolución.

Cree, a modo de ejemplo, el siguiente procedimiento almacenado en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:

```sql
CREATE PROCEDURE CheckContactCity  
   (@cityName CHAR(50))  
AS  
BEGIN  
   IF ((SELECT COUNT(*)  
   FROM Person.Address  
   WHERE City = @cityName) > 1)  
   RETURN 1  
ELSE  
   RETURN 0  
END  
```

Este procedimiento almacenado devuelve un valor de estado de 1 ó 0 en función de si la ciudad especificada en el parámetro cityName se encuentra en la tabla Person.Address.

En el siguiente ejemplo, se pasa una conexión abierta a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] a la función y se usa el método [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) para llamar al procedimiento almacenado CheckContactCity:

[!code[JDBC#UsingSprocWithReturnStatus1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_1_1.java)]

## <a name="see-also"></a>Consulte también

[Usar instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md)
