---
title: Tipos de datos PHP predeterminados
description: En este tema se enumeran todos los tipos de datos PHP predeterminados con sus tipos de datos de SQL Server correspondientes al usar el controlador SQLSRV de Microsoft para PHP en SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: b66c301d-3d20-45b8-a112-225d8f01c0bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1e1cf91baf80fd6298eaaca9c9e12a0b5858d9f
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680797"
---
# <a name="default-php-data-types"></a>Tipos de datos PHP predeterminados
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Cuando se recuperan datos del servidor, los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] los convierten a un tipo de datos PHP predeterminado si el usuario no ha especificado ninguno.  
  
Cuando se devuelven datos utilizando el controlador PDO_SQLSRV, el tipo de datos será int o String.  
  
En el resto del contenido de este tema, se describen los tipos de datos predeterminados que utilizan el controlador SQLSRV.  
  
En la tabla siguiente se muestra el tipo de datos de SQL Server (el tipo de datos que se recupera del servidor), el tipo de datos PHP predeterminado (el tipo de datos al que se efectúa la conversión) y la codificación predeterminada de secuencias y cadenas. Para obtener información más detallada acerca de cómo especificar los tipos de datos cuando se recuperan datos del servidor, consulte [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
|Tipo de datos de SQL Server|Tipo de datos PHP predeterminado|Codificación predeterminada|  
|-------------------|--------------------|--------------------|  
|bigint|String|Carácter de 8 bits<sup>1</sup>|  
|binary|Stream<sup>2</sup>|Binaria<sup>3</sup>|  
|bit|Entero|Carácter de 8 bits<sup>1</sup>|  
|char|String|Carácter de 8 bits<sup>1</sup>|  
|date<sup>4</sup>|Datetime|No aplicable|  
|datetime<sup>4</sup>|Datetime|No aplicable|  
|datetime2<sup>4</sup>|Datetime|No aplicable|  
|datetimeoffset<sup>4</sup>|Datetime|No aplicable|  
|Decimal|String|Carácter de 8 bits<sup>1</sup>|  
|FLOAT|Float|Carácter de 8 bits<sup>1</sup>|  
|geography|Stream|Binaria<sup>3</sup>|  
|geometry|Stream|Binaria<sup>3</sup>|  
|imagen<sup>5</sup>|Stream<sup>2</sup>|Binaria<sup>3</sup>|  
|int|Entero|Carácter de 8 bits<sup>1</sup>|  
|money|String|Carácter de 8 bits<sup>1</sup>|  
|NCHAR|String|Carácter de 8 bits<sup>1</sup>|  
|NUMERIC|String|Carácter de 8 bits<sup>1</sup>|  
|NVARCHAR|String|Carácter de 8 bits<sup>1</sup>|  
|nvarchar(MAX)|Stream<sup>2</sup>|Carácter de 8 bits<sup>1</sup>|  
|ntext<sup>6</sup>|Stream<sup>2</sup>|Carácter de 8 bits<sup>1</sup>|  
|real|Float|Carácter de 8 bits<sup>1</sup>|  
|smalldatetime|Datetime|Carácter de 8 bits<sup>1</sup>|  
|SMALLINT|Entero|Carácter de 8 bits<sup>1</sup>|  
|SMALLMONEY|String|Carácter de 8 bits<sup>1</sup>|  
|sql_variant<sup>7</sup>|String|Carácter de 8 bits<sup>1</sup>|  
|texto<sup>8</sup>|Stream<sup>2</sup>|Carácter de 8 bits<sup>1</sup>|  
|time<sup>4</sup>|Datetime|No aplicable|  
|timestamp|String|Carácter de 8 bits<sup>1</sup>|  
|TINYINT|Entero|Carácter de 8 bits<sup>1</sup>|  
|UDT|Stream<sup>2</sup>|Binaria<sup>3</sup>|  
|UNIQUEIDENTIFIER|Cadena<sup>9</sup>|Carácter de 8 bits<sup>1</sup>|  
|varbinary|Stream<sup>2</sup>|Binaria<sup>3</sup>|  
|varbinary(MAX)|Stream<sup>2</sup>|Binaria<sup>3</sup>|  
|varchar|String|Carácter de 8 bits<sup>1</sup>|  
|varchar(MAX)|Stream<sup>2</sup>|Carácter de 8 bits<sup>1</sup>|
|Xml|Stream<sup>2</sup>|Carácter de 8 bits<sup>1</sup>|  
  

1.  Los datos se devuelven en caracteres de 8 bits tal y como se especifica en la página de códigos de la configuración regional de Windows del sistema. Los caracteres multibyte, o aquellos que no tengan una correspondencia con esta página de códigos, se sustituyen por un carácter de signo de interrogación de cierre (?) de un solo byte.  
  
2.  Si [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md) o [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) se usan para recuperar datos con el tipo de datos de PHP predeterminado Flujo, los datos se devuelven como una cadena con la misma codificación que el flujo. Por ejemplo, si se recupera un tipo binario de SQL Server mediante **sqlsrv_fetch_array**, el tipo de valor predeterminado devuelto es una cadena binaria.  
  
3.  Los datos se devuelven del servidor como una secuencia de bytes sin procesar, sin que se realicen procesos de codificación o traducción.  

4.  Los tipos de datos de fecha y hora se pueden recuperar como cadenas. Para obtener más información, vea [Cómo recuperar el tipo de fecha y hora como cadenas con el controlador SQLSRV](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md).  

5.  Se trata de un tipo heredado que se asigna al tipo varbinary(max).

6. Se trata de un tipo heredado que se asigna al tipo nvarchar(max).

7.  sql_variant no se admite en parámetros de salida o bidireccionales.

8.  Se trata de un tipo heredado que se asigna al tipo varchar(max).  
  
9.  Los datos uniqueidentifier son GUID que se representan mediante la siguiente expresión regular:  
  
    [0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-f]{4}-[0-9a-fA-f]{4}-[0-9a-fA-F]{12}  
 
 
## <a name="other-new-sql-server-2008-data-types-and-features"></a>Otras características y tipos de datos de SQL Server 2008 nuevos  
En los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], no se admiten los tipos de datos de SQL Server 2008 nuevos y que no figuran en las columnas (por ejemplo, los parámetros con valores de tabla). En la siguiente tabla se resume la compatibilidad de PHP con las nuevas características de SQL Server 2008.  
  
|Característica|Compatibilidad de PHP|  
|-----------|---------------|  
|Parámetro con valores de tabla|No|  
|Columnas dispersas|Parcial|  
|Compresión de bits Null|Sí|  
|Tipos de datos CLR definidos por el usuario (UDT) de gran tamaño|Sí|  
|Nombre de entidad de seguridad de servicio|No|  
|MERGE|Sí|  
|FILESTREAM|Parcial|  
  
En el caso de que la compatibilidad del tipo en cuestión sea parcial, no se podrán realizar consultas mediante programación del tipo de datos de la columna.  
  
## <a name="see-also"></a>Consulte también  
[Constantes &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[Conversión de tipos de datos](../../connect/php/converting-data-types.md)

[Tipos de datos PHP](https://php.net/manual/en/language.types.php)

[Tipos de datos (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)  
  
