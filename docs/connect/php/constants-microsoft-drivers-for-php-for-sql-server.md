---
title: Constantes (controladores de Microsoft para PHP para SQL Server)
description: Obtenga información sobre las constantes definidas en los controladores SQLSRV y PDO_SQLSRV de Microsoft para PHP para SQL Server.
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- constants
ms.assetid: 9727c944-b645-48d6-9012-18dbde35ee3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 771a14e8705af72f57571503c2dba9012c2e9879
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435257"
---
# <a name="constants-microsoft-drivers-for-php-for-sql-server"></a>Constantes (controladores de Microsoft para PHP para SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se analizan las constantes definidas por los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="pdo_sqlsrv-driver-constants"></a>Constantes del controlador PDO_SQLSRV  
Las constantes incluidas en el [sitio web de PDO](https://php.net/manual/book.pdo.php) son válidas para los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
En las siguientes secciones, se describen las constantes específicas de Microsoft del controlador PDO_SQLSRV.  
  
### <a name="transaction-isolation-level-constants"></a>Constantes de nivel de aislamiento de transacción  
La clave **TransactionIsolation** , que se usa con [PDO::__construct](../../connect/php/pdo-construct.md), acepta una de las siguientes constantes:  
  
-   PDO::SQLSRV_TXN_READ_UNCOMMITTED  
  
-   PDO::SQLSRV_TXN_READ_COMMITTED  
  
-   PDO::SQLSRV_TXN_REPEATABLE_READ  
  
-   PDO::SQLSRV_TXN_SNAPSHOT  
  
-   PDO::SQLSRV_TXN_SERIALIZABLE  
  
Para obtener más información sobre la clave **TransactionIsolation** , consulte [Connection Options](../../connect/php/connection-options.md).  
  
### <a name="encoding-constants"></a>Constantes de codificación  
El atributo PDO::SQLSRV_ATTR_ENCODING puede transmitirse a [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), [PDO::setAttribute](../../connect/php/pdo-setattribute.md), [PDO::prepare](../../connect/php/pdo-prepare.md), [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) y [PDOStatement::bindParam](../../connect/php/pdostatement-bindparam.md).  
  
Los valores disponibles para transmitir a PDO::SQLSRV_ATTR_ENCODING son los siguientes:  
  
|Constante del controlador PDO_SQLSRV|Descripción|  
|-------------------------------|---------------|  
|PDO::SQLSRV_ENCODING_BINARY|Los datos son una secuencia de bytes sin procesar procedentes del servidor, sin que se realicen procesos de codificación o traducción.<br /><br />No válida para PDO::setAttribute.|  
|PDO::SQLSRV_ENCODING_SYSTEM|Los datos son caracteres de 8 bits tal y como se especifica en la página de códigos de la configuración regional de Windows establecida en el sistema. Los caracteres multibyte, o aquellos que no tengan una correspondencia con esta página de códigos, se sustituyen por un carácter de signo de interrogación de cierre (?) de un solo byte.|  
|PDO::SQLSRV_ENCODING_UTF8|Los datos presentan la codificación UTF-8. Esta es la codificación predeterminada.|  
|PDO::SQLSRV_ENCODING_DEFAULT|Utiliza PDO::SQLSRV_ENCODING_SYSTEM si se especifica durante la conexión.<br /><br />Utiliza la codificación de la conexión si se especifica en una instrucción prepare.|  
  
### <a name="query-timeout"></a>Tiempo de espera de la consulta  
El atributo PDO::SQLSRV_ATTR_QUERY_TIMEOUT es cualquier número entero no negativo que represente el período de tiempo de espera, en segundos. Cero (0) es el valor predeterminado y significa que no hay tiempo de espera.  
  
Puede especificar el atributo PDO::SQLSRV_ATTR_QUERY_TIMEOUT con [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), [PDO::setAttribute](../../connect/php/pdo-setattribute.md) y [PDO::prepare](../../connect/php/pdo-prepare.md).  
  
### <a name="direct-or-prepared-execution"></a>Ejecución directa o preparada  
Puede seleccionar la ejecución de la consulta directa o la ejecución de la instrucción preparada con el atributo PDO::SQLSRV_ATTR_DIRECT_QUERY. PDO::SQLSRV_ATTR_DIRECT_QUERY puede definirse con [PDO::prepare](../../connect/php/pdo-prepare.md) o [PDO::setAttribute](../../connect/php/pdo-setattribute.md). Para obtener más información sobre PDO::SQLSRV_ATTR_DIRECT_QUERY, vea [Direct Statement Execution and Prepared Statement Execution in the PDO_SQLSRV Driver](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md) (Ejecución de la instrucción preparada o directa en el controlador PDO_SQLSRV).  

### <a name="handling-numeric-fetches"></a>Control de capturas numéricas
El atributo PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE se puede usar para controlar las capturas numéricas de columnas con tipos SQL numéricos (bit, integer, smallint, tinyint, float y real). Cuando PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE está establecido en true, los resultados de una columna de enteros se representan como ints, mientras que los valores float y real de SQL se representan como valores flotantes. Este atributo se puede establecer con [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md). 

Puede modificar el comportamiento del formato decimal predeterminado con los atributos PDO::SQLSRV_ATTR_FORMAT_DECIMALS y PDO::SQLSRV_ATTR_DECIMAL_PLACES. El comportamiento de estos atributos es idéntico a las opciones correspondientes en el lado de SQLSRV (**FormatDecimals** y **DecimalPlaces**), salvo que no se admiten parámetros de salida para el formato. Estos atributos se pueden establecer en el nivel de conexión o de instrucción con [PDO::setAttribute](../../connect/php/pdo-setattribute.md) o [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), pero cualquier atributo de instrucción invalidará el atributo de conexión correspondiente. Para más información, vea [Aplicación de formato a cadenas decimales y valores de moneda (controlador PDO_SQLSRV)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).

### <a name="handling-date-and-time-fetches"></a>Control de las recuperaciones de fecha y hora

PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE especifica si se deben recuperar los tipos de fecha y hora como objetos [PHP DateTime](http://php.net/manual/en/class.datetime.php). Si el valor se deja como false, el comportamiento predeterminado es devolverlos como cadenas. Este atributo se puede establecer en el nivel de conexión o de instrucción con [PDO::setAttribute](../../connect/php/pdo-setattribute.md) o [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), pero el atributo de instrucción invalidará el atributo de conexión correspondiente. Para más información, vea: [Cómo: Recuperación de los tipos de fecha y hora como objetos de fecha y hora PHP mediante el controlador PDO_SQLSRV](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md).

## <a name="sqlsrv-driver-constants"></a>SQLSRV  
En las siguientes secciones se incluyen las constantes que utiliza el controlador SQLSRV.  
  
### <a name="err-constants"></a>Constantes de ERR  
En la siguiente tabla se indican las constantes que se utilizan para especificar si [sqlsrv_errors](../../connect/php/sqlsrv-errors.md) devuelve errores, advertencias o ambos.  
  
|Value|Descripción|  
|---------|---------------|  
|SQLSRV_ERR_ALL|Se devuelven los errores y las advertencias generados en la última llamada a una función de **sqlsrv** . Este es el valor predeterminado.|  
|SQLSRV_ERR_ERRORS|Se devuelven los errores generados en la última llamada a una función de **sqlsrv** .|  
|SQLSRV_ERR_WARNINGS|Se devuelven las advertencias generadas en la última llamada a una función de **sqlsrv** .|  
  
### <a name="fetch-constants"></a>Constantes de FETCH  
En la siguiente tabla se incluyen las constantes que se utilizan para especificar el tipo de la matriz devuelta por [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md).  
  
|Constante de SQLSRV|Descripción|  
|-------------------|---------------|  
|SQLSRV_FETCH_ASSOC|**sqlsrv_fetch_array** devuelve la siguiente fila de datos como una matriz asociativa.|  
|SQLSRV_FETCH_BOTH|**sqlsrv_fetch_array** devuelve la siguiente fila de datos como una matriz con claves tanto numéricas como asociativas. Este es el valor predeterminado.|  
|SQLSRV_FETCH_NUMERIC|**sqlsrv_fetch_array** devuelve la siguiente fila de datos como una matriz indexada numéricamente.|  
  
### <a name="logging-constants"></a>Constantes de registro  
En esta sección se incluyen las constantes que se usan para cambiar la configuración de registro con [sqlsrv_configure](../../connect/php/sqlsrv-configure.md). Para obtener más información sobre la actividad de registro, consulte [Logging Activity](../../connect/php/logging-activity.md).  
  
En la siguiente tabla se incluyen las constantes que se pueden utilizar como el valor de la configuración **LogSubsystems** :  
  
|Constante SQLSRV (equivalente entero entre paréntesis)|Descripción|  
|----------------------------------------------------------|---------------|  
|SQLSRV_LOG_SYSTEM_ALL (-1)|Activa el registro de todos los subsistemas.|  
|SQLSRV_LOG_SYSTEM_CONN (2)|Activa el registro de la actividad de conexión.|  
|SQLSRV_LOG_SYSTEM_INIT (1)|Activa el registro de la actividad de inicialización.|  
|SQLSRV_LOG_SYSTEM_OFF (0)|Desactiva el registro.|  
|SQLSRV_LOG_SYSTEM_STMT (4)|Activa el registro de la actividad de instrucción.|  
|SQLSRV_LOG_SYSTEM_UTIL (8)|Activa el registro de la actividad de funciones de error (como **handle_error** y **handle_warning**).|  
  
En la tabla siguiente se incluyen las constantes que se pueden utilizar como el valor de la configuración **LogSeverity** :  
  
|Constante SQLSRV (equivalente entero entre paréntesis)|Descripción|  
|----------------------------------------------------------|---------------|  
|SQLSRV_LOG_SEVERITY_ALL (-1)|Especifica que se registrarán errores, advertencias y avisos.|  
|SQLSRV_LOG_SEVERITY_ERROR (1)|Especifica que se registrarán los errores.|  
|SQLSRV_LOG_SEVERITY_NOTICE (4)|Especifica que se registrarán los avisos.|  
|SQLSRV_LOG_SEVERITY_WARNING (2)|Especifica que se registrarán las advertencias.|  
  
### <a name="nullable-constants"></a>Constantes que admiten valores NULL  
En la siguiente tabla se muestran las constantes que puede usar para determinar si una columna admite valores NULL o no, o si esta información no está disponible. Puede comparar el valor de la clave **Nullable** que devuelve [sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md) para determinar el estado de admisión de valores NULL de la columna.  
  
|Constante SQLSRV (equivalente entero entre paréntesis)|Descripción|  
|----------------------------------------------------------|---------------|  
|SQLSRV_NULLABLE_YES (0)|La columna admite valores NULL.|  
|SQLSRV_NULLABLE_NO (1)|La columna no admite valores NULL.|  
|SQLSRV_NULLABLE_UNKNOWN (2)|No se sabe si la columna admite valores NULL.|  
  
### <a name="param-constants"></a>Constantes de PARAM  
En la siguiente lista se enumeran las constantes para especificar la dirección del parámetro al llamar a [sqlsrv_query](../../connect/php/sqlsrv-query.md) o [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
|Constante de SQLSRV|Descripción|  
|-------------------|---------------|  
|SQLSRV_PARAM_IN|Indica un parámetro de entrada.|  
|SQLSRV_PARAM_INOUT|Indica un parámetro bidireccional.|  
|SQLSRV_PARAM_OUT|Indica un parámetro de salida.|  
  
### <a name="phptype-constants"></a>Constantes de PHPTYPE  
En la siguiente tabla se muestran las constantes que se utilizan para describir tipos de datos PHP. Para obtener información sobre los tipos de datos PHP, vea [Tipos de PHP](https://php.net/manual/en/language.types.php).  
  
|Constante de SQLSRV|Tipo de datos PHP|  
|-------------------|-----------------|  
|SQLSRV_PHPTYPE_INT|Entero|  
|SQLSRV_PHPTYPE_DATETIME|Datetime|  
|SQLSRV_PHPTYPE_FLOAT|Float|  
|SQLSRV_PHPTYPE_STREAM($encoding<sup>1</sup>)|Transmitir|  
|SQLSRV_PHPTYPE_STRING($encoding<sup>1</sup>)|String|  
  
1. **SQLSRV_PHPTYPE_STREAM** y **SQLSRV_PHPTYPE_STRING** aceptan un parámetro que especifique la codificación de la secuencia. En la siguiente tabla se indican las constantes de SQLSRV que constituyen parámetros aceptables y una descripción de la codificación correspondiente.  
  
|Constante de SQLSRV|Descripción|  
|-------------------|---------------|  
|SQLSRV_ENC_BINARY|Los datos se devuelven del servidor como una secuencia de bytes sin procesar, sin que se realicen procesos de codificación o traducción.|  
|SQLSRV_ENC_CHAR|Los datos se devuelven en caracteres de 8 bits tal y como se especifica en la página de códigos de la configuración regional de Windows establecida en el sistema. Los caracteres multibyte, o aquellos que no tengan una correspondencia con esta página de códigos, se sustituyen por un carácter de signo de interrogación de cierre (?) de un solo byte.<br /><br />Esta es la codificación predeterminada.|  
|"UTF-8"|Los datos se devuelven con la codificación UTF-8. Esta constante se agregó en la versión 1.1 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Para obtener más información sobre la compatibilidad con UTF-8, vea [Cómo enviar y recuperar datos UTF-8 gracias a la compatibilidad integrada con UTF-8](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md).|  
  
> [!NOTE]  
> Cuando use **SQLSRV_PHPTYPE_STREAM** o **SQLSRV_PHPTYPE_STRING**, debe especificar la codificación. Si no se proporciona ningún parámetro, se devolverá un error.  
  
Para obtener más información sobre estas constantes, vea [Cómo especificar tipos de datos PHP](../../connect/php/how-to-specify-php-data-types.md)y [Cómo recuperar datos de caracteres como una secuencia usando el controlador SQLSRV](../../connect/php/how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver.md).  
  
### <a name="sqltype-constants"></a>Constantes de SQLTYPE  
En la siguiente tabla se muestran las constantes que se utilizan para describir tipos de datos de SQL Server. Algunas constantes son de tipo función y pueden tomar parámetros que corresponden a la precisión, la escala y la longitud.  Al enlazar parámetros, se deben usar las constantes de tipo función. En el caso de las comparaciones de tipos, se requieren las constantes estándar (no similares a las funciones). Para obtener información sobre los tipos de datos de SQL Server, vea [Tipos de datos (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md). Para obtener información sobre la precisión, la escala y la longitud, vea [Precisión, escala y longitud (Transact-SQL)](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
|Constante de SQLSRV|Tipos de datos de SQL Server|  
|-------------------|------------------------|  
|SQLSRV_SQLTYPE_BIGINT|bigint|  
|SQLSRV_SQLTYPE_BINARY|binary|  
|SQLSRV_SQLTYPE_BIT|bit|  
|SQLSRV_SQLTYPE_CHAR|char<sup>5</sup>|  
|SQLSRV_SQLTYPE_CHAR($charCount)|char|  
|SQLSRV_SQLTYPE_DATE|date<sup>4</sup>|  
|SQLSRV_SQLTYPE_DATETIME|datetime|  
|SQLSRV_SQLTYPE_DATETIME2|datetime2<sup>4</sup>|  
|SQLSRV_SQLTYPE_DATETIMEOFFSET|datetimeoffset<sup>4</sup>|  
|SQLSRV_SQLTYPE_DECIMAL|decimal<sup>5</sup>|
|SQLSRV_SQLTYPE_DECIMAL($precision, $scale)|Decimal|  
|SQLSRV_SQLTYPE_FLOAT|FLOAT|  
|SQLSRV_SQLTYPE_IMAGE|image<sup>1</sup>|  
|SQLSRV_SQLTYPE_INT|int|  
|SQLSRV_SQLTYPE_MONEY|money| 
|SQLSRV_SQLTYPE_NCHAR|nchar<sup>5</sup>|   
|SQLSRV_SQLTYPE_NCHAR($charCount)|NCHAR|  
|SQLSRV_SQLTYPE_NUMERIC|numeric<sup>5</sup>|
|SQLSRV_SQLTYPE_NUMERIC($precision, $scale)|NUMERIC|  
|SQLSRV_SQLTYPE_NVARCHAR|nvarchar<sup>5</sup>|  
|SQLSRV_SQLTYPE_NVARCHAR($charCount)|NVARCHAR|  
|SQLSRV_SQLTYPE_NVARCHAR('max')|nvarchar(MAX)|  
|SQLSRV_SQLTYPE_NTEXT|ntext<sup>2</sup>|  
|SQLSRV_SQLTYPE_REAL|real|  
|SQLSRV_SQLTYPE_SMALLDATETIME|smalldatetime|  
|SQLSRV_SQLTYPE_SMALLINT|SMALLINT|  
|SQLSRV_SQLTYPE_SMALLMONEY|SMALLMONEY|  
|SQLSRV_SQLTYPE_TEXT|text<sup>3</sup>|  
|SQLSRV_SQLTYPE_TIME|time<sup>4</sup>|  
|SQLSRV_SQLTYPE_TIMESTAMP|timestamp|  
|SQLSRV_SQLTYPE_TINYINT|TINYINT|  
|SQLSRV_SQLTYPE_UNIQUEIDENTIFIER|UNIQUEIDENTIFIER|  
|SQLSRV_SQLTYPE_UDT|UDT|  
|SQLSRV_SQLTYPE_VARBINARY|varbinary<sup>5</sup>|  
|SQLSRV_SQLTYPE_VARBINARY($byteCount)|varbinary|  
|SQLSRV_SQLTYPE_VARBINARY('max')|varbinary(MAX)|  
|SQLSRV_SQLTYPE_VARCHAR|varchar<sup>5</sup>|  
|SQLSRV_SQLTYPE_VARCHAR($charCount)|varchar|  
|SQLSRV_SQLTYPE_VARCHAR('max')|varchar(MAX)|  
|SQLSRV_SQLTYPE_XML|Xml|  
  
1.  Se trata de un tipo heredado que se asigna al tipo varbinary(max).  
  
2.  Se trata de un tipo heredado que se asigna al tipo nvarchar más reciente.  
  
3.  Se trata de un tipo heredado que se asigna al tipo varchar más reciente.  
  
4.  La compatibilidad con este tipo se agregó en la versión 1.1 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

5.  Estas constantes se deben usar en las operaciones de comparación de tipos y no se deben reemplazar las constantes de tipo función con una sintaxis parecida. En el caso de los parámetros de enlace, debe usar las constantes de tipo función.

  
En la siguiente tabla se incluyen las constantes de SQLTYPE que aceptan parámetros y el intervalo de valores permitidos para cada parámetro.  
  
|SQLTYPE|Parámetro|Intervalo permitido para el parámetro|  
|-----------|-------------|---------------------------------|  
|SQLSRV_SQLTYPE_CHAR,<br /><br />SQLSRV_SQLTYPE_VARCHAR|charCount|1–8000|  
|SQLSRV_SQLTYPE_NCHAR,<br /><br />SQLSRV_SQLTYPE_NVARCHAR|charCount|1–4000|  
|SQLSRV_SQLTYPE_BINARY,<br /><br />SQLSRV_SQLTYPE_VARBINARY|byteCount|1–8000|  
|SQLSRV_SQLTYPE_DECIMAL,<br /><br />SQLSRV_SQLTYPE_NUMERIC|Precisión|1 - 38|  
|SQLSRV_SQLTYPE_DECIMAL,<br /><br />SQLSRV_SQLTYPE_NUMERIC|scale|1–precisión|  
  
### <a name="transaction-isolation-level-constants"></a>Constantes de nivel de aislamiento de transacción  
La clave **TransactionIsolation** , que se usa con [sqlsrv_connect](../../connect/php/sqlsrv-connect.md), acepta una de las siguientes constantes:  
  
-   SQLSRV_TXN_READ_UNCOMMITTED  
  
-   SQLSRV_TXN_READ_COMMITTED  
  
-   SQLSRV_TXN_REPEATABLE_READ  
  
-   SQLSRV_TXN_SNAPSHOT  
  
-   SQLSRV_TXN_SERIALIZABLE  
  
### <a name="cursor-and-scrolling-constants"></a>Constantes de cursor y desplazamiento  
Las siguientes constantes especifican el tipo de cursor que puede usar en un conjunto de resultados:  
  
-   SQLSRV_CURSOR_FORWARD  
  
-   SQLSRV_CURSOR_STATIC  
  
-   SQLSRV_CURSOR_DYNAMIC  
  
-   SQLSRV_CURSOR_KEYSET  
  
-   SQLSRV_CURSOR_CLIENT_BUFFERED  
  
Las siguientes constantes especifican qué fila se debe seleccionar en el conjunto de resultados:  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
Para obtener información sobre cómo usar estas constantes, consulte [Specifying a Cursor Type and Selecting Rows](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).  
  
## <a name="see-also"></a>Consulte también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  
