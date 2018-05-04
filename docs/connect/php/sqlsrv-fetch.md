---
title: sqlsrv_fetch | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_fetch
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch
- API Reference, sqlsrv_fetch
- retrieving data, as a single field
ms.assetid: a5a640a1-6e7d-452e-8b66-850a4dc2ce89
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b1e88274bb409cc7cc0863f99a0641559eaed1b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsrvfetch"></a>sqlsrv_fetch
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Hace que la siguiente fila de un conjunto de resultados esté disponible para la lectura. Use [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) para leer campos de la fila.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_fetch( resource $stmt[, row[, ]offset])  
```  
  
#### <a name="parameters"></a>Parámetros  
*$stmt*: un recurso de instrucción correspondiente a una instrucción ejecutada.  
  
> [!NOTE]  
> Se debe ejecutar una instrucción antes de poder recuperar resultados. Para obtener información sobre cómo ejecutar una instrucción, consulte [sqlsrv_query](../../connect/php/sqlsrv-query.md) y [sqlsrv_execute](../../connect/php/sqlsrv-execute.md).  
  
*fila* [opcional]: uno de los siguientes valores, especificar la fila que se va a obtener acceso a un conjunto de resultados que utilice un cursor desplazable:  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
Para obtener más información sobre estos valores, vea [Especificación de un tipo de cursor y selección de filas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).  
  
*desplazamiento* [opcional]: se utiliza con SQLSRV_SCROLL_ABSOLUTE y SQLSRV_SCROLL_RELATIVE para especificar la fila que se va a recuperar. El primer registro del conjunto de resultados es 0.  
  
## <a name="return-value"></a>Valor devuelto  
Si se ha recuperado correctamente la siguiente fila del conjunto de resultados, se devuelve el valor **True** . Si no hay más resultados en el conjunto de resultados, se devuelve el valor **Null** . Si se produce un error, se devuelve el valor **False** .  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se usa **sqlsrv_fetch** para recuperar una fila de datos que contiene una reseña del producto y el nombre del autor. Para recuperar datos del conjunto de resultados, [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) se utiliza. El ejemplo supone que SQL Server y el [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) base de datos se instalan en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up and execute the query. Note that both ReviewerName and  
Comments are of SQL Server type nvarchar. */  
$tsql = "SELECT ReviewerName, Comments   
         FROM Production.ProductReview  
         WHERE ProductReviewID=1";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in statement preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Make the first row of the result set available for reading. */  
if( sqlsrv_fetch( $stmt ) === false)  
{  
     echo "Error in retrieving row.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Note: Fields must be accessed in order.  
Get the first field of the row. Note that no return type is  
specified. Data will be returned as a string, the default for  
a field of type nvarchar.*/  
$name = sqlsrv_get_field( $stmt, 0);  
echo "$name: ";  
  
/*Get the second field of the row as a stream.  
Because the default return type for a nvarchar field is a  
string, the return type must be specified as a stream. */  
$stream = sqlsrv_get_field( $stmt, 1,   
                            SQLSRV_PHPTYPE_STREAM( SQLSRV_ENC_CHAR));  
while( !feof( $stream ))  
{   
    $str = fread( $stream, 10000);  
    echo $str;  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Recuperación de datos](../../connect/php/retrieving-data.md)  

[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  
  
