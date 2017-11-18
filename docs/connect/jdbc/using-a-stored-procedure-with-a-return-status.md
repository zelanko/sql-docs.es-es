---
title: Mediante un procedimiento almacenado con un estado de retorno | Documentos de Microsoft
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
ms.assetid: 4b126e95-8458-41d6-af37-fc6662859f19
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8247f7f81e70aafac8d109abe7f8303c8e13f487
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-stored-procedure-with-a-return-status"></a>Usar un procedimiento almacenado con un estado de devolución
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedimiento almacenado que se puede llamar es aquella que devuelve un estado o un parámetro de resultado. Se usa normalmente para indicar el funcionamiento correcto o incorrecto del procedimiento almacenado. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona el [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) (clase), que puede usar para llamar a este tipo de procedimiento almacenado y procesar los datos que devuelve.  
  
 Cuando se llama a este tipo de procedimiento almacenado con el controlador JDBC, tendrá que usar el `call` secuencia de escape SQL junto con la [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) método de la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) (clase) . La sintaxis de la `call` secuencia de escape con un parámetro de estado devuelto es el siguiente:  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Para obtener más información acerca de las secuencias de escape SQL, consulte [usar secuencias de Escape de SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 ¿Al construir el `call` secuencia de escape, especifique el parámetro de estado devuelto con el? (signo de interrogación). Este carácter actúa como un marcador de posición para el valor del parámetro que devolverá el procedimiento almacenado. Para especificar un valor para un parámetro de estado de retorno, debe especificar el tipo de datos del parámetro mediante el [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) método de la clase SQLServerCallableStatement, antes de ejecutar el procedimiento almacenado.  
  
> [!NOTE]  
>  Al usar el controlador JDBC con una base de datos de SQL Server, el valor que especifique para el parámetro de estado de retorno en el método registerOutParameter siempre será un entero, que se puede especificar utilizando el tipo de datos java.sql.Types.INTEGER.  
  
 Además, cuando se pasa un valor para el método registerOutParameter para un parámetro de estado de retorno, debe especificar no solo los tipos de datos que se utilizará para el parámetro, sino también la posición del parámetro ordinal en la llamada de procedimiento almacenado. En el caso del parámetro de estado de devolución, su posición ordinal siempre es 1 debido a que es siempre el primer parámetro de la llamada al procedimiento almacenado. Aunque la clase SQLServerCallableStatement proporciona compatibilidad para que utilizar el nombre del parámetro para indicar el parámetro concreto, puede usar solo el número de posición ordinal del parámetro para los parámetros de estado de retorno.  
  
 Por ejemplo, cree el siguiente procedimiento almacenado en el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo:  
  
```  
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
  
 En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función y el [ejecutar](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) método se usa para llamar al procedimiento almacenado CheckContactCity:  
  
 [!code[JDBC#UsingSprocWithReturnStatus1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_1_1.java)]  
  
## <a name="see-also"></a>Vea también  
 [Usar instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  

