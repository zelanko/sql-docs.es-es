---
title: Usar un procedimiento almacenado con parámetros de entrada | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8f491b70-7d1b-42bd-964f-9a8b86af5eaa
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c408fc703a3f6d9831cae226ce858b1a20a80c7
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278776"
---
# <a name="using-a-stored-procedure-with-input-parameters"></a>Usar un procedimiento almacenado con parámetros de entrada
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Un procedimiento almacenado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] al que se puede llamar es aquel que contiene uno o más parámetros IN, parámetros que se pueden usar para pasar datos al procedimiento almacenado. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona la clase [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), que puede usar para llamar a este procedimiento almacenado y para procesar los datos que devuelve.  
  
 Si usa el controlador JDBC para llamar a un procedimiento almacenado con los parámetros IN, debe usar la secuencia de escape `call` de SQL junto con el método [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). La sintaxis de la secuencia de escape `call` con los parámetros IN es la siguiente:  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Para obtener más información acerca de las secuencias de escape SQL, consulte [usando secuencias de Escape SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Al crear la secuencia de escape `call`, especifique los parámetros IN mediante el carácter ? (signo de interrogación). Este carácter actúa como un marcador de posición para los valores de parámetros pasados al procedimiento almacenado. Para especificar un valor para un parámetro, puede usar uno de los métodos de establecedor de la clase SQLServerPreparedStatement. El método del establecedor que puede usar se determina mediante el tipo del parámetro IN.  
  
 Cuando pasa un valor al método establecedor, debe especificar no solo el valor real que se usará en el parámetro, sino el lugar ordinal que ocupa el parámetro en el procedimiento almacenado. Por ejemplo, si el procedimiento almacenado contiene un solo parámetro IN, su valor ordinal será 1. Si el procedimiento almacenado contiene dos parámetros, el primer valor ordinal es 1 y el segundo 2.  
  
 Como ejemplo de cómo llamar a un procedimiento que contiene un parámetro IN, use el procedimiento almacenado uspGetEmployeeManagers de la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Este procedimiento almacenado acepta un solo parámetro de entrada llamado EmployeeID (Id. del empleado), que es un valor entero, y devuelve una lista recursiva de empleados y sus jefes según el EmployeeID especificado. El código Java para llamar a este procedimiento almacenado es el siguiente:  
  
```java
public static void executeSprocInParams(Connection con) throws SQLException {  
    try(PreparedStatement pstmt = con.prepareStatement("{call dbo.uspGetEmployeeManagers(?)}"); ) {  

        pstmt.setInt(1, 50);  
        ResultSet rs = pstmt.executeQuery();  

        while (rs.next()) {  
            System.out.println("EMPLOYEE:");  
            System.out.println(rs.getString("LastName") + ", " + rs.getString("FirstName"));  
            System.out.println("MANAGER:");  
            System.out.println(rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));  
            System.out.println();  
        }  
    }
}
```  
  
## <a name="see-also"></a>Ver también  
 [Usar instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
