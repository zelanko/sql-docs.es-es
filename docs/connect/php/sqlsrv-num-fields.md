---
title: sqlsrv_num_fields | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_num_fields
apitype: NA
helpviewer_keywords:
- sqlsrv_num_fields
- API Reference, sqlsrv_num_fields
ms.assetid: 03ca1860-01ed-408c-862a-57a7355de4bf
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b7c42aa895d02420f50f8ab35b6d18453839eb18
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvnumfields"></a>sqlsrv_num_fields
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera el número de campos de un conjunto de resultados activo. Tenga en cuenta que se puede llamar a **sqlsrv_num_fields** en cualquier instrucción preparada, con independencia de que sea anterior o posterior a la ejecución.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_num_fields( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parámetros  
*$stmt*: la instrucción en el que está activo el conjunto de resultados de destino.  
  
## <a name="return-value"></a>Valor devuelto  
Establece un valor entero que representa el número de campos del conjunto de resultados activo. Si se produce un error, se devuelve el valor booleano **False** .  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se ejecuta una consulta para recuperar todos los campos de las primeras tres filas en la tabla *HumanResources.Department* de la base de datos de Adventureworks. La función **sqlsrv_num_fields** determina el número de campos del conjunto de resultados. Gracias a esto, los datos pueden mostrarse repitiéndose a través de los campos de cada fila devuelta.  
  
En el ejemplo se da por hecho que SQL Server y la base de datos de [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) están instalados en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Define and execute the query. */  
$tsql = "SELECT TOP (3) * FROM HumanResources.Department";  
$stmt = sqlsrv_query($conn, $tsql);  
if( $stmt === false)  
{  
     echo "Error in executing query.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve the number of fields. */  
$numFields = sqlsrv_num_fields( $stmt );  
  
/* Iterate through each row of the result set. */  
while( sqlsrv_fetch( $stmt ))  
{  
     /* Iterate through the fields of each row. */  
     for($i = 0; $i < $numFields; $i++)  
     {  
          echo sqlsrv_get_field($stmt, $i,   
                   SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR))." ";  
     }  
     echo "\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt );  
sqlsrv_close( $conn );  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)  
[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  
  

