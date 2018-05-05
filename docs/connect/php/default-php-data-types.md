---
title: Tipos de datos PHP predeterminados | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: b66c301d-3d20-45b8-a112-225d8f01c0bd
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8ae48b672aa4817f8451eeee788985b4b90694f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="default-php-data-types"></a>Tipos de datos PHP predeterminados
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Cuando se recuperan datos del servidor, los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] los convierten a un tipo de datos PHP predeterminado si el usuario no ha especificado ninguno.  
  
Cuando se devuelven datos utilizando el controlador PDO_SQLSRV, el tipo de datos será int o String.  
  
En el resto del contenido de este tema, se describen los tipos de datos predeterminados que utilizan el controlador SQLSRV.  
  
En la tabla siguiente se muestra el tipo de datos de SQL Server (el tipo de datos que se recupera del servidor), el tipo de datos PHP predeterminado (el tipo de datos al que se efectúa la conversión) y la codificación predeterminada de secuencias y cadenas. Para obtener información más detallada acerca de cómo especificar los tipos de datos cuando se recuperan datos del servidor, consulte [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
|Tipo de datos de SQL Server|Tipo de datos PHP predeterminado|Codificación predeterminada|  
|-------------------|--------------------|--------------------|  
|bigint|String|caracteres de 8 bits<sup>1</sup>|  
|binary|Stream<sup>2</sup>|Binaria<sup>3</sup>|  
|bit|Integer|caracteres de 8 bits<sup>1</sup>|  
|char|String|caracteres de 8 bits<sup>1</sup>|  
|date<sup>4</sup>|Fecha y hora|No aplicable|  
|fecha y hora<sup>4</sup>|Fecha y hora|No aplicable|  
|datetime2<sup>4</sup>|Fecha y hora|No aplicable|  
|datetimeoffset<sup>4</sup>|Fecha y hora|No aplicable|  
|decimal|String|caracteres de 8 bits<sup>1</sup>|  
|float|Float|caracteres de 8 bits<sup>1</sup>|  
|geography|Stream|Binaria<sup>3</sup>|  
|geometry|Stream|Binaria<sup>3</sup>|  
|imagen<sup>5</sup>|Stream<sup>2</sup>|Binaria<sup>3</sup>|  
|int|Integer|caracteres de 8 bits<sup>1</sup>|  
|money|String|caracteres de 8 bits<sup>1</sup>|  
|NCHAR|String|caracteres de 8 bits<sup>1</sup>|  
|numeric|String|caracteres de 8 bits<sup>1</sup>|  
|nvarchar|String|caracteres de 8 bits<sup>1</sup>|  
|nvarchar(MAX)|Stream<sup>2</sup>|caracteres de 8 bits<sup>1</sup>|  
|ntext<sup>6</sup>|Stream<sup>2</sup>|caracteres de 8 bits<sup>1</sup>|  
|real|Float|caracteres de 8 bits<sup>1</sup>|  
|smalldatetime|Fecha y hora|caracteres de 8 bits<sup>1</sup>|  
|smallint|Integer|caracteres de 8 bits<sup>1</sup>|  
|smallmoney|String|caracteres de 8 bits<sup>1</sup>|  
|sql_variant<sup>7</sup>|String|caracteres de 8 bits<sup>1</sup>|  
|texto<sup>8</sup>|Stream<sup>2</sup>|caracteres de 8 bits<sup>1</sup>|  
|time<sup>4</sup>|Fecha y hora|No aplicable|  
|TIMESTAMP|String|caracteres de 8 bits<sup>1</sup>|  
|tinyint|Integer|caracteres de 8 bits<sup>1</sup>|  
|UDT|Stream<sup>2</sup>|Binaria<sup>3</sup>|  
|uniqueidentifier|Cadena<sup>9</sup>|caracteres de 8 bits<sup>1</sup>|  
|varbinary|Stream<sup>2</sup>|Binaria<sup>3</sup>|  
|varbinary(MAX)|Stream<sup>2</sup>|Binaria<sup>3</sup>|  
|varchar|String|caracteres de 8 bits<sup>1</sup>|  
|varchar(MAX)|Stream<sup>2</sup>|caracteres de 8 bits<sup>1</sup>|
|xml|Stream<sup>2</sup>|caracteres de 8 bits<sup>1</sup>|  
  

1.  Los datos se devuelven en caracteres de 8 bits tal y como se especifica en la página de códigos de la configuración regional de Windows del sistema. Los caracteres de varios bytes o caracteres que no se asignen en esta página de códigos se sustituirán por un carácter de un solo byte de signo de interrogación (?).  
  
2.  Si [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md) o [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) es usa para recuperar los datos que tiene un tipo PHP predeterminado de secuencia, se devuelven los datos como una cadena con la misma codificación que la secuencia. Por ejemplo, si un binario de SQL Server se recupera tipo mediante el uso de **sqlsrv_fetch_array**, el valor devuelto predeterminado es de tipo de una cadena binaria.  
  
3.  Los datos se devuelven del servidor como una secuencia de bytes sin procesar, sin que se realicen procesos de codificación o traducción.  

4.  Los tipos de datos de fecha y hora se pueden recuperar como cadenas. Para obtener más información, vea [Cómo recuperar el tipo de fecha y hora como cadenas con el controlador SQLSRV](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md).  

5.  Se trata de un tipo heredado que se asigna al tipo varbinary(max).

6. Se trata de un tipo heredado que se asigna al tipo nvarchar(max).

7.  sql_variant no se admite en los parámetros de salida o bidireccional.

8.  Se trata de un tipo heredado que se asigna al tipo varchar(max).  
  
9.  Los datos uniqueidentifier son GUID que se representan mediante la siguiente expresión regular:  
  
    [0-9a-fA-F] {8}-[0-9a-fA-F]{4}-[0-9a-fA-f]{4}-[0-9a-fA-f]{4}-[0-9a-fA-F]{12}  
 
 
## <a name="other-new-sql-server-2008-data-types-and-features"></a>Otras características y tipos de datos de SQL Server 2008 nuevos  
No se admiten tipos de datos que son nuevas en SQL Server 2008 y que existen fuera de las columnas (por ejemplo, los parámetros con valores de tabla) en el [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. En la tabla siguiente se resume la compatibilidad PHP para las nuevas características de SQL Server 2008.  
  
|Característica|Compatibilidad de PHP|  
|-----------|---------------|  
|Parámetro con valores de tabla|no|  
|Columnas dispersas|Parcial|  
|Compresión de bits Null|Sí|  
|Tipos de datos CLR definidos por el usuario (UDT) de gran tamaño|Sí|  
|Nombre de entidad de seguridad de servicio|no|  
|MERGE|Sí|  
|FILESTREAM|Parcial|  
  
En el caso de que la compatibilidad del tipo en cuestión sea parcial, no se podrán realizar consultas mediante programación del tipo de datos de la columna.  
  
## <a name="see-also"></a>Vea también  
[Constantes &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[Converting Data Types](../../connect/php/converting-data-types.md)

[Tipos de PHP](http://php.net/manual/en/language.types.php)

[Tipos de datos (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)  
  
