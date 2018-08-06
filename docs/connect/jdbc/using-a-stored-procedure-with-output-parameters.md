---
title: Usar un procedimiento almacenado con parámetros de salida | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1c006f27-7e99-43d5-974c-7b782659290c
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d040dd53d646a455e3623b2a0ee33406ea4574c5
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278626"
---
# <a name="using-a-stored-procedure-with-output-parameters"></a>Usar un procedimiento almacenado con parámetros de salida
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Un procedimiento almacenado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] al que se puede llamar es aquel que devuelve uno o más parámetros OUT, que son los parámetros que el procedimiento almacenado usa para devolver los datos a la aplicación que realiza la llamada. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), que se puede usar para llamar a este tipo de procedimiento almacenado y procesar los datos que devuelve.  
  
 Cuando se llama a este tipo de procedimiento almacenado con JDBC Driver, se debe usar la secuencia de escape `call` de SQL junto con el método [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). La sintaxis para la secuencia de escape `call` con parámetros OUT es la siguiente:  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Para obtener más información acerca de las secuencias de escape SQL, consulte [usando secuencias de Escape SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Al crear la secuencia de escape `call`, especifique los parámetros OUT mediante el carácter ? (signo de interrogación). Este carácter actúa como un marcador de posición para los valores de parámetros devueltos por el procedimiento almacenado. Para especificar un valor para un parámetro OUT, debe especificar el tipo de datos de cada parámetro mediante el método [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) de la clase SQLServerCallableStatement antes de ejecutar el procedimiento almacenado.  
  
 El valor especificado para el parámetro OUT en el método registerOutParameter debe ser uno de los tipos de datos JDBC incluidos en java.sql.Types, que se asigna a su vez a uno de los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nativos. Para obtener más información acerca de JDBC y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos, vea [describir los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md).  
  
 Cuando pasa un valor al método registerOutParameter para un parámetro OUT, debe especificar no solo el tipo de datos que se usará para el parámetro, sino también la posición ordinal del parámetro o el nombre del mismo en el procedimiento almacenado. Por ejemplo, si el procedimiento almacenado contiene un solo parámetro OUT, su valor ordinal es 1 y, si el procedimiento almacenado contiene dos parámetros, el primer valor ordinal es 1 y el segundo 2.  
  
> [!NOTE]  
>  JDBC Driver no admite el uso de los tipos de datos CURSOR, SQLVARIANT, TABLE y TIMESTAMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] como parámetros OUT.  
  
 Cree, a modo de ejemplo, el siguiente procedimiento almacenado en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:  
  
```sql
CREATE PROCEDURE GetImmediateManager  
   @employeeID INT,  
   @managerID INT OUTPUT  
AS  
BEGIN  
   SELECT @managerID = ManagerID   
   FROM HumanResources.Employee   
   WHERE EmployeeID = @employeeID  
END
```  
  
 Este procedimiento almacenado devuelve un solo parámetro OUT (managerID), que es un entero, en función del parámetro IN (employeeID) especificado, que también es un entero. El valor devuelto en el parámetro OUT es ManagerID en función de EmployeeID en la tabla HumanResources.Employee.  
  
 En el siguiente ejemplo, se pasa a la función una conexión abierta a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] y se usa el método [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) para llamar al procedimiento almacenado GetImmediateManager:  
  
```java
public static void executeStoredProcedure(Connection con) throws SQLException {  
    try(CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");) {  
        cstmt.setInt(1, 5);  
        cstmt.registerOutParameter(2, java.sql.Types.INTEGER);  
        cstmt.execute();  
        System.out.println("MANAGER ID: " + cstmt.getInt(2));  
    }  
} 
```  
  
 Este ejemplo utiliza las posiciones ordinales para identificar los parámetros. También puede identificar un parámetro utilizando su nombre en lugar de su posición ordinal. En el ejemplo de código siguiente se modifica el ejemplo anterior para demostrar cómo utilizar los parámetros con nombre en una aplicación Java. Observe que los nombres de parámetros se corresponden con los nombres de parámetros en la definición del procedimiento almacenado:  
  
```java
public static void executeStoredProcedure(Connection con) throws SQLException {  
    try(CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}"); ) {  
        cstmt.setInt("employeeID", 5);  
        cstmt.registerOutParameter("managerID", java.sql.Types.INTEGER);  
        cstmt.execute();  
        System.out.println("MANAGER ID: " + cstmt.getInt("managerID"));  
    }  
}
```  
  
> [!NOTE]  
>  Estos ejemplos utilizan el método execute de la clase SQLServerCallableStatement para ejecutar el procedimiento almacenado. Se usa dicho método porque el procedimiento almacenado no ha devuelto ningún conjunto de resultados. En caso contrario, se usaría el método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md).  
  
 Los procedimientos almacenados también pueden devolver recuentos de actualizaciones y múltiples conjuntos de resultados. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] sigue la especificación de JDBC 3.0, que indica que se deben recuperar varios conjuntos de resultados y recuentos de actualizaciones antes de que se recuperen los parámetros OUT. Es decir, la aplicación debe recuperar todos los objetos de conjunto de resultados y recuentos de actualizaciones antes de recuperar los parámetros OUT mediante los métodos CallableStatement.getter. De lo contrario, los objetos ResultSet y los recuentos de actualizaciones que aún no se hayan recuperado se perderán cuando se recuperen los parámetros OUT. Para obtener más información sobre recuentos de actualizaciones y conjuntos de resultados, vea [mediante un procedimiento almacenado con un recuento de actualización](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) y [utilizando varios conjuntos de resultados](../../connect/jdbc/using-multiple-result-sets.md).  
  
## <a name="see-also"></a>Ver también  
 [Usar instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
