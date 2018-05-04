---
title: Usar una instrucción SQL para modificar datos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0d399da05226cb05506ad62cee3128a4a42aa0e6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-an-sql-statement-to-modify-data"></a>Usar una instrucción SQL para modificar datos
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para modificar los datos que se encuentran en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos mediante una instrucción SQL, se puede utilizar el [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) método de la [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) clase. El método executeUpdate pasará la instrucción SQL para la base de datos para su procesamiento y, a continuación, devuelven un valor que indica el número de filas afectadas.  
  
 Para ello, primero debe crear un objeto SQLServerStatement mediante el uso de la [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) método de la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) clase.  
  
 En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función, se genera una instrucción SQL que agrega nuevos datos a la tabla y, a continuación, se ejecuta la instrucción y se muestra el valor devuelto.  
  
 [!code[JDBC#UsingSQLToModifyData1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_1_1.java)]  
  
> [!NOTE]  
>  Si tiene que utilizar una instrucción SQL que contiene parámetros para modificar los datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos, debe usar el [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md) método de la [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) clase.  
>   
>  Si la columna en que intenta insertar datos contiene caracteres especiales (por ejemplo, espacios), debe proporcionar los valores que se van a insertar incluso si se trata de valores predeterminados. En caso contrario, la operación de inserción no funciona.  
>   
>  Si desea que el controlador JDBC devuelva todos los recuentos de actualizaciones, incluidos los recuentos de actualizaciones devueltos por todos los desencadenadores activados, establezca la propiedad de cadena de conexión lastUpdateCount en "false". Para obtener más información acerca de la propiedad lastUpdateCount, consulte [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Usar instrucciones con SQL](../../connect/jdbc/using-statements-with-sql.md)  
  
  
