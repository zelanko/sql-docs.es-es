---
title: Empleo de un procedimiento almacenado con un recuento de actualización| Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 64cf4877-5995-4bfc-8865-b7618a5c8d01
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 851974955b9311efc149ecdff310bfbb1d8869fc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026935"
---
# <a name="using-a-stored-procedure-with-an-update-count"></a>Empleo de un procedimiento almacenado con un recuento de actualización

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para modificar datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un procedimiento almacenado, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). Con la clase SQLServerCallableStatement, puede llamar a los procedimientos almacenados que modifican los datos en la base de datos y devuelven un recuento del número de filas afectadas, lo que se denomina recuento de actualización.

Una vez configurada la llamada al procedimiento almacenado mediante la clase SQLServerCallableStatement, puede llamar al procedimiento almacenado con el método [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) o [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md). El método executeUpdate devuelve un valor **int** que contiene el número de filas afectadas por el procedimiento almacenado, mientras que el método execute no lo hace. Si usa el método execute y quiere obtener el recuento del número de filas afectadas, puede llamar al método [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) después de ejecutar el procedimiento almacenado.

> [!NOTE]  
> Si desea que el controlador JDBC devuelva todos los recuentos de actualizaciones, incluidos los recuentos de actualizaciones devueltos por todos los desencadenadores activados, establezca la propiedad de cadena de conexión lastUpdateCount en "false". Para obtener más información sobre la propiedad lastUpdateCount, consulte [Establecimiento de las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).

A modo de ejemplo, cree la tabla y el procedimiento almacenado siguientes e inserte también datos de ejemplo en la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:

```sql
CREATE TABLE TestTable
   (Col1 int IDENTITY,
    Col2 varchar(50),
    Col3 int);  

CREATE PROCEDURE UpdateTestTable  
   @Col2 varchar(50),  
   @Col3 int  
AS  
BEGIN  
   UPDATE TestTable  
   SET Col2 = @Col2, Col3 = @Col3  
END;  
INSERT INTO dbo.TestTable (Col2, Col3) VALUES ('b', 10);  
```

En el siguiente ejemplo, se pasa una conexión abierta a la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] a la función, se usa el método execute para llamar al procedimiento almacenado UpdateTestTable y luego se usa el método getUpdateCount para devolver un recuento de las filas afectadas por el procedimiento almacenado.

[!code[JDBC#UsingSprocWithUpdateCount1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_0_1.java)]

## <a name="see-also"></a>Consulte también

[Empleo de instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md)
