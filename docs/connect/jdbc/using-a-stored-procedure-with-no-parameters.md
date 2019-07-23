---
title: Uso de un procedimiento almacenado sin parámetros | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e9470a6d-a758-4c56-96ec-7b37139e36a7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3dade70a033ddf2a9e20ffc09930a27e26d9a579
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916506"
---
# <a name="using-a-stored-procedure-with-no-parameters"></a>Usar un procedimiento almacenado sin parámetros

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

El tipo más sencillo de procedimiento almacenado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al que puede llamar es el que no contiene parámetros y devuelve un solo conjunto de resultados. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona la clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), que puede usar para llamar a este tipo de procedimiento almacenado y procesar los datos que devuelve.

Si usa el controlador JDBC para llamar a un procedimiento almacenado sin parámetros, debe usar la secuencia de escape `call` de SQL. La sintaxis de la secuencia de escape `call` sin parámetros es la siguiente:

`{call procedure-name}`

> [!NOTE]  
> Para obtener más información sobre las secuencias de escape de SQL, vea [usar secuencias de escape de SQL](../../connect/jdbc/using-sql-escape-sequences.md).

Cree, a modo de ejemplo, el siguiente procedimiento almacenado en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:

```sql
CREATE PROCEDURE GetContactFormalNames
AS  
BEGIN  
   SELECT TOP 10 Title + ' ' + FirstName + ' ' + LastName AS FormalName
   FROM Person.Contact  
END  
```

Este procedimiento almacenado devuelve un solo conjunto de resultados que contiene una columna de datos, compuesta por una combinación del título, el nombre y el apellido de las diez primeras consultas de la tabla Person.Contact.

En el siguiente ejemplo, se pasa a la función una conexión abierta a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] y se usa el método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) para llamar al procedimiento almacenado GetContactFormalNames.

```java
public static void executeSprocNoParams(Connection con) throws SQLException {  
    try(Statement stmt = con.createStatement();) {  

        ResultSet rs = stmt.executeQuery("{call dbo.GetContactFormalNames}");  
        while (rs.next()) {  
            System.out.println(rs.getString("FormalName"));  
        }  
    }  
}
```

## <a name="see-also"></a>Consulte también

[Usar instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md)
