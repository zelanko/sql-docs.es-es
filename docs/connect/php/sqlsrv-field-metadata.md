---
title: sqlsrv_field_metadata | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_field_metadata
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_field_metadata
- sqlsrv_field_metadata
ms.assetid: c02f6942-0484-4567-a78e-fe8aa2053536
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c030a6a3d2ba5caad755abfd92a5cf1adb01cc25
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47748513"
---
# <a name="sqlsrvfieldmetadata"></a>sqlsrv_field_metadata
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera los metadatos de los campos de una instrucción preparada. Para obtener información acerca de cómo preparar una instrucción, consulte [sqlsrv_query](../../connect/php/sqlsrv-query.md) o [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md). Tenga en cuenta que se puede llamar a **sqlsrv_field_metadata** en cualquier instrucción preparada, ya sea antes o después de la ejecución.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_field_metadata( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parámetros  
*$stmt*: un recurso de instrucción para el que se buscan metadatos de campo.  
  
## <a name="return-value"></a>Valor devuelto  
Una **matriz** de matrices o el valor **False**. La matriz consta de una matriz por cada campo del conjunto de resultados. Cada submatriz contiene las claves que se describen en la siguiente tabla. Si se produce un error en el proceso de recuperación de los metadatos de los campos, se devuelve el valor **False** .  
  
|Key|Descripción|  
|-------|---------------|  
|Nombre|Nombre de la columna a la que corresponde el campo.|  
|Tipo|Valor numérico que corresponde a un tipo SQL.|  
|Tamaño|Número de caracteres de los campos de tipo de carácter: char(n), varchar(n), nchar(n), nvarchar(n) y XML. Número de bytes de los campos de tipo binario: binary(n), varbinary(n) y UDT. En otros tipos de datos de SQL Server, se devuelve**NULL** .|  
|Precisión|La precisión de los tipos de precisión de variables: real, numeric, decimal, datetime2, datetimeoffset y time. En otros tipos de datos de SQL Server, se devuelve**NULL** .|  
|Escala|La escala de los tipos de escala de variables: numeric, decimal, datetime2, datetimeoffset y time. En otros tipos de datos de SQL Server, se devuelve**NULL** .|  
|Admisión de valores NULL|Un valor enumerado que indica si la columna acepta valores Null (**SQLSRV_NULLABLE_YES**), no los acepta (**SQLSRV_NULLABLE_NO**) o no se sabe si los acepta (**SQLSRV_NULLABLE_UNKNOWN**).|  
  
En la tabla siguiente se proporciona más información sobre las claves de cada submatriz (consulte la documentación de SQL Server para obtener más información sobre estos tipos):  
  
|Tipo de datos de SQL Server 2008|Tipo|Precisión mín./máx.|Escala mín./máx.|Tamaño|  
|-----------------------------|--------|----------------------|------------------|--------|  
|BIGINT|SQL_BIGINT (-5)|||8|  
|binary|SQL_BINARY (-2)|||0 < *n* < 8000 <sup>1</sup>|  
|bit|SQL_BIT (-7)||||  
|char|SQL_CHAR (1)|||0 < *n* < 8000 <sup>1</sup>|  
|Date|SQL_TYPE_DATE (91)|10/10|0/0||  
|DATETIME|SQL_TYPE_TIMESTAMP (93)|23/23|3/3||  
|datetime2|SQL_TYPE_TIMESTAMP (93)|19/27|0/7||  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET (-155)|26/34|0/7||  
|Decimal|SQL_DECIMAL (3)|1/38|0/valor de precisión||  
|FLOAT|SQL_FLOAT (6)|4/8|||  
|imagen|SQL_LONGVARBINARY (-4)|||2 GB|  
|INT|SQL_INTEGER (4)||||  
|money|SQL_DECIMAL (3)|19/19|4/4||  
|NCHAR|SQL_WCHAR (-8)|||0 < *n* < 4000 <sup>1</sup>|  
|ntext|SQL_WLONGVARCHAR (-10)|||1 GB|  
|NUMERIC|SQL_NUMERIC (2)|1/38|0/valor de precisión||  
|NVARCHAR|SQL_WVARCHAR (-9)|||0 < *n* < 4000 <sup>1</sup>|  
|REAL|SQL_REAL (7)|4/4|||  
|smalldatetime|SQL_TYPE_TIMESTAMP (93)|16/16|0/0||  
|SMALLINT|SQL_SMALLINT (5)|||2 bytes|  
|Smallmoney|SQL_DECIMAL (3)|10/10|4/4||  
|texto|SQL_LONGVARCHAR (-1)|||2 GB|  
|time|SQL_SS_TIME2 (-154)|8/16|0/7||  
|TIMESTAMP|SQL_BINARY (-2)|||8 bytes|  
|tinyint|SQL_TINYINT (-6)|||1 byte|  
|udt|SQL_SS_UDT (-151)|||variable|  
|UNIQUEIDENTIFIER|SQL_GUID (-11)|||16|  
|varbinary|SQL_VARBINARY (-3)|||0 < *n* < 8000 <sup>1</sup>|  
|varchar|SQL_VARCHAR (12)|||0 < *n* < 8000 <sup>1</sup>|  
|xml|SQL_SS_XML (-152)|||0|  
  
(1) Un valor de cero (0) indica que se permite el tamaño máximo.  
  
La clave que acepta valores Null puede ser yes o no.  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se crea un recurso de instrucción y, luego, se recuperan y muestran los metadatos de los campos. En el ejemplo se da por hecho que SQL Server y la base de datos [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) están instalados en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
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
  
/* Prepare the statement. */  
$tsql = "SELECT ReviewerName, Comments FROM Production.ProductReview";  
$stmt = sqlsrv_prepare( $conn, $tsql);  
  
/* Get and display field metadata. */  
foreach( sqlsrv_field_metadata( $stmt) as $fieldMetadata)  
{  
      foreach( $fieldMetadata as $name => $value)  
      {  
           echo "$name: $value\n";  
      }  
      echo "\n";  
}  
  
/* Note: sqlsrv_field_metadata can be called on any statement  
resource, pre- or post-execution. */  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Ver también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[Constantes &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  

[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  
  
