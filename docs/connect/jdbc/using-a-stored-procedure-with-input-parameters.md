---
title: "Usar un procedimiento almacenado con parámetros de entrada | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8f491b70-7d1b-42bd-964f-9a8b86af5eaa
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 49f92bf52ddf9c06906f42b81945ec3d630c8be4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-stored-procedure-with-input-parameters"></a>Usar un procedimiento almacenado con parámetros de entrada
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedimiento almacenado que se puede llamar es aquel que contiene uno o más parámetros IN, que son los parámetros que pueden utilizarse para pasar datos al procedimiento almacenado. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona el [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) (clase), que puede usar para llamar a este tipo de procedimiento almacenado y procesar los datos que devuelve.  
  
 Al usar el controlador JDBC para llamar a un procedimiento almacenado con parámetros, debe usar el `call` secuencia de escape SQL junto con la [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) método de la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) clase. La sintaxis de la `call` secuencia de escape con parámetros es como sigue:  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Para obtener más información acerca de las secuencias de escape SQL, consulte [usar secuencias de Escape de SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 ¿Al construir el `call` secuencia de escape, especifique los parámetros IN mediante el? (signo de interrogación). Este carácter actúa como un marcador de posición para los valores de parámetros pasados al procedimiento almacenado. Para especificar un valor para un parámetro, puede usar uno de los métodos de establecedor de la clase SQLServerPreparedStatement. El método del establecedor que puede usar se determina mediante el tipo del parámetro IN.  
  
 Cuando pasa un valor al método establecedor, debe especificar no solo el valor real que se usará en el parámetro, sino el lugar ordinal que ocupa el parámetro en el procedimiento almacenado. Por ejemplo, si el procedimiento almacenado contiene un solo parámetro IN, su valor ordinal será 1. Si el procedimiento almacenado contiene dos parámetros, el primer valor ordinal es 1 y el segundo 2.  
  
 Como ejemplo de cómo llamar a un procedimiento almacenado que contiene un parámetro IN, use el procedimiento almacenado uspGetEmployeeManagers en la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo. Este procedimiento almacenado acepta un solo parámetro de entrada llamado EmployeeID (Id. del empleado), que es un valor entero, y devuelve una lista recursiva de empleados y sus jefes según el EmployeeID especificado. El código Java para llamar a este procedimiento almacenado es el siguiente:  
  
```  
public static void executeSprocInParams(Connection con) {  
   try {  
      PreparedStatement pstmt = con.prepareStatement("{call dbo.uspGetEmployeeManagers(?)}");  
      pstmt.setInt(1, 50);  
      ResultSet rs = pstmt.executeQuery();  
  
      while (rs.next()) {  
         System.out.println("EMPLOYEE:");  
         System.out.println(rs.getString("LastName") + ", " + rs.getString("FirstName"));  
         System.out.println("MANAGER:");  
         System.out.println(rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));  
         System.out.println();  
      }  
      rs.close();  
      pstmt.close();  
   }  
  
   catch (Exception e) {  
      e.printStackTrace();  
    }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  

