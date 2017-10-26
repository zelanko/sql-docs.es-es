---
title: "Mediante un procedimiento almacenado con parámetros de salida | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1c006f27-7e99-43d5-974c-7b782659290c
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8e5c3b945652c04cbbe75563d853703b5676b43f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-stored-procedure-with-output-parameters"></a>Usar un procedimiento almacenado con parámetros de salida
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedimiento almacenado que se puede llamar es aquella que devuelve uno o varios parámetros, que son parámetros que utiliza el procedimiento almacenado para devolver datos de salida devuelto a la aplicación que realiza la llamada. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona el [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) (clase), que puede usar para llamar a este tipo de procedimiento almacenado y procesar los datos que devuelve.  
  
 Cuando se llama a este tipo de procedimiento almacenado con el controlador JDBC, debe utilizar el `call` secuencia de escape SQL junto con la [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) método de la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) clase. La sintaxis de la `call` secuencia de escape con los parámetros de salida es la siguiente:  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Para obtener más información acerca de las secuencias de escape SQL, consulte [usar secuencias de Escape de SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 ¿Al construir el `call` secuencia de escape, especifique los parámetros OUT con el? (signo de interrogación). Este carácter actúa como un marcador de posición para los valores de parámetros devueltos por el procedimiento almacenado. Para especificar un valor para un parámetro OUT, debe especificar el tipo de datos de cada parámetro mediante el [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) método de la clase SQLServerCallableStatement antes de ejecutar el procedimiento almacenado.  
  
 El valor que especifique para el parámetro OUT en el método registerOutParameter debe ser uno de los tipos de datos JDBC incluidos en java.sql.Types, que a su vez se asigna a uno de nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos. Para obtener más información acerca de JDBC y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos, consulte [descripción de los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md).  
  
 Cuando se pasa un valor para el método registerOutParameter para un parámetro OUT, debe especificar no solo los tipos de datos que se utilizará para el parámetro, pero también posición ordinal del parámetro o el nombre del parámetro en el procedimiento almacenado. Por ejemplo, si el procedimiento almacenado contiene un solo parámetro OUT, su valor ordinal es 1 y, si el procedimiento almacenado contiene dos parámetros, el primer valor ordinal es 1 y el segundo 2.  
  
> [!NOTE]  
>  El controlador JDBC no admite el uso de CURSOR, SQLVARIANT, tabla y marca de tiempo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos como parámetros de salida.  
  
 Por ejemplo, cree el siguiente procedimiento almacenado en el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo:  
  
```  
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
  
 En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función y el [ejecutar](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) método se usa para llamar al procedimiento almacenado GetImmediateManager:  
  
```  
public static void executeStoredProcedure(Connection con) {  
   try {  
      CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");  
      cstmt.setInt(1, 5);  
      cstmt.registerOutParameter(2, java.sql.Types.INTEGER);  
      cstmt.execute();  
      System.out.println("MANAGER ID: " + cstmt.getInt(2));  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
 Este ejemplo utiliza las posiciones ordinales para identificar los parámetros. También puede identificar un parámetro utilizando su nombre en lugar de su posición ordinal. En el ejemplo de código siguiente se modifica el ejemplo anterior para demostrar cómo utilizar los parámetros con nombre en una aplicación Java. Observe que los nombres de parámetros se corresponden con los nombres de parámetros en la definición del procedimiento almacenado:  
  
```  
public static void executeStoredProcedure(Connection con) {  
   try {  
      CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");  
      cstmt.setInt("employeeID", 5);  
      cstmt.registerOutParameter("managerID", java.sql.Types.INTEGER);  
      cstmt.execute();  
      System.out.println("MANAGER ID: " + cstmt.getInt("managerID"));  
      cstmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
```  
  
 }  
  
> [!NOTE]  
>  Estos ejemplos utilizan el método execute de la clase SQLServerCallableStatement para ejecutar el procedimiento almacenado. Se usa dicho método porque el procedimiento almacenado no ha devuelto ningún conjunto de resultados. Si lo hiciera, el [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) se usaría el método.  
  
 Los procedimientos almacenados también pueden devolver recuentos de actualizaciones y múltiples conjuntos de resultados. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] sigue la especificación de JDBC 3.0, que indica que se deben recuperar varios conjuntos de resultados y recuentos de actualizaciones antes de que se recuperen los parámetros OUT. Es decir, la aplicación debe recuperar todos los objetos de conjunto de resultados y recuentos de actualizaciones antes de recuperar los parámetros OUT mediante los métodos de CallableStatement.getter. En caso contrario, los objetos de conjunto de resultados y recuentos de actualizaciones que no se han recuperado se perderán cuando se recuperen los parámetros OUT. Para obtener más información sobre recuentos de actualizaciones y conjuntos de resultados, vea [mediante un procedimiento almacenado con un recuento de actualización](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) y [utilizando varios conjuntos de resultados](../../connect/jdbc/using-multiple-result-sets.md).  
  
## <a name="see-also"></a>Vea también  
 [Usar instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  

