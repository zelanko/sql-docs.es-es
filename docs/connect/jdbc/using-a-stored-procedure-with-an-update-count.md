---
title: Usar un procedimiento almacenado con un recuento de actualizaciones | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 64cf4877-5995-4bfc-8865-b7618a5c8d01
caps.latest.revision: "26"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3d0d09c7db3e657630515d1c8b9601c1049babdd
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="using-a-stored-procedure-with-an-update-count"></a>Usar un procedimiento almacenado con un recuento de actualizaciones
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para modificar datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos mediante un procedimiento almacenado, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona el [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clase. Mediante el uso de la clase SQLServerCallableStatement, puede llamar a procedimientos almacenados que modifican los datos que se encuentra en la base de datos y devolver un recuento del número de filas afectadas, también se denomina el número de actualizaciones.  
  
 Una vez haya configurado la llamada al procedimiento almacenado mediante la clase SQLServerCallableStatement, puede, a continuación, llame al procedimiento almacenado mediante el uso del [ejecutar](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) o [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) método. El método executeUpdate devolverá un **int** valor que contiene el número de filas afectadas por el procedimiento almacenado, pero el método execute no lo hace. Si utiliza el método execute y desea obtener el recuento del número de filas afectadas, puede llamar a la [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) método después de ejecutar el procedimiento almacenado.  
  
> [!NOTE]  
>  Si desea que el controlador JDBC devuelva todos los recuentos de actualizaciones, incluidos los recuentos de actualizaciones devueltos por todos los desencadenadores activados, establezca la propiedad de cadena de conexión lastUpdateCount en "false". Para obtener más información acerca de la propiedad lastUpdateCount, consulte [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Por ejemplo, cree la siguiente tabla y un procedimiento almacenado y también insertar los datos de ejemplo en el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo:  
  
```  
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
  
 En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función, se usa el método execute para llamar al procedimiento almacenado UpdateTestTable y, a continuación, se utiliza el método getUpdateCount para devolver un recuento de las filas que están afectadas por el procedimiento almacenado.  
  
 [!code[JDBC#UsingSprocWithUpdateCount1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_0_1.java)]  
  
## <a name="see-also"></a>Vea también  
 [Usar instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
