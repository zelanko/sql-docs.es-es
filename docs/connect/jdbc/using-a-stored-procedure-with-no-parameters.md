---
title: Usar un procedimiento almacenado sin parámetros | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e9470a6d-a758-4c56-96ec-7b37139e36a7
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7db021b9d3fdf875c2c6074159b56d8e6cb0fd14
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32851240"
---
# <a name="using-a-stored-procedure-with-no-parameters"></a>Usar un procedimiento almacenado sin parámetros
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El tipo más sencillo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedimiento almacenado que se puede llamar es aquel que no contiene ningún parámetro y devuelve un conjunto de resultados único. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona el [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) (clase), que puede usar para llamar a este tipo de procedimiento almacenado y procesar los datos que devuelve.  
  
 Al usar el controlador JDBC para llamar a un procedimiento almacenado sin parámetros, debe usar el `call` secuencia de escape SQL. La sintaxis de la `call` secuencia de escape sin parámetros es como sigue:  
  
 `{call procedure-name}`  
  
> [!NOTE]  
>  Para obtener más información acerca de las secuencias de escape SQL, consulte [usar secuencias de Escape de SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Por ejemplo, cree el siguiente procedimiento almacenado en el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo:  
  
```  
CREATE PROCEDURE GetContactFormalNames   
AS  
BEGIN  
   SELECT TOP 10 Title + ' ' + FirstName + ' ' + LastName AS FormalName   
   FROM Person.Contact  
END  
```  
  
 Este procedimiento almacenado devuelve un solo conjunto de resultados que contiene una columna de datos, compuesta por una combinación del título, el nombre y el apellido de las diez primeras consultas de la tabla Person.Contact.  
  
 En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función y el [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) método se usa para llamar al procedimiento almacenado GetContactFormalNames.  
  
```  
public static void executeSprocNoParams(Connection con) {  
   try {  
      Statement stmt = con.createStatement();  
      ResultSet rs = stmt.executeQuery("{call dbo.GetContactFormalNames}");  
  
      while (rs.next()) {  
         System.out.println(rs.getString("FormalName"));  
      }  
      rs.close();  
      stmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
