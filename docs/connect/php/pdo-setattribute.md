---
title: 'PDO:: setAttribute | Documentos de Microsoft'
ms.custom: 
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 56f9ee96-e1d2-46cc-b137-38f06a251863
caps.latest.revision: "24"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 07659d23732d78958ea8db6258a9fe836ca0b883
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="pdosetattribute"></a>PDO::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Establece un atributo PDO predefinido o un controlador personalizado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
bool PDO::setAttribute ( $attribute, $value );  
```  
  
#### <a name="parameters"></a>Parámetros  
*$attribute*: el atributo que se establecerá. Consulte la sección Comentarios para obtener la lista de atributos admitidos.  
  
*$value*: el valor (tipo mixto).  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve True si la operación se realiza correctamente; de lo contrario, False.  
  
## <a name="remarks"></a>Comentarios  
  
|Attribute|Procesado mediante|Valores admitidos|Description|  
|-------------|----------------|--------------------|---------------|  
|PDO::ATTR_CASE|PDO|PDO::CASE_LOWER<br /><br />PDO::CASE_NATURAL<br /><br />PDO::CASE_UPPER|Especifica la mayúsculas en los nombres de columna.<br /><br />PDO::CASE_LOWER aplica minúsculas a los nombres de columna.<br /><br />PDO::CASE_NATURAL (el valor predeterminado) muestra los nombres de columna con el mismo uso de mayúsculas y minúsculas que aparece en la base de datos.<br /><br />PDO::CASE_UPPER aplica mayúsculas a los nombres de columna.<br /><br />Este atributo también puede establecerse utilizando PDO::setAttribute.|  
|PDO::ATTR_DEFAULT_FETCH_MODE|PDO|Consulte la documentación de PDO.|Consulte la documentación de PDO.|  
|PDO::ATTR_ERRMODE|PDO|PDO::ERRMODE_SILENT<br /><br />PDO::ERRMODE_WARNING<br /><br />PDO::ERRMODE_EXCEPTION|Especifica cómo el controlador detecta errores.<br /><br />PDO::ERRMODE_SILENT (el valor predeterminado) establece la información y los códigos de los errores.<br /><br />PDO::ERRMODE_WARNING genera una advertencia E_WARNING.<br /><br />PDO::ERRMODE_EXCEPTION genera una excepción.<br /><br />Este atributo también puede establecerse utilizando PDO::setAttribute.|  
|PDO::ATTR_ORACLE_NULLS|PDO|Consulte la documentación de PDO.|Especifica cómo se deben devolver los valores Null.<br /><br />PDO::NULL_NATURAL no realiza ninguna conversión.<br /><br />PDO::NULL_EMPTY_STRING convierte el valor de una cadena vacía en Null.<br /><br />PDO::NULL_TO_STRING convierte el valor de una cadena vacía en Null.|  
|PDO::ATTR_STATEMENT_CLASS|PDO|Consulte la documentación de PDO.|Establece que la clase de la instrucción proporcionada por el usuario se obtenga de PDOStatement.<br /><br />Se requiere `array(string classname, array(mixed constructor_args))`.<br /><br />Para obtener más información, consulte la documentación de la API.|  
|PDO::ATTR_STRINGIFY_FETCHES|PDO|true o false|Convierte los valores numéricos en cadenas al recuperar los datos.|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|1 para el límite de memoria PHP.|Configura el tamaño del búfer que contiene el conjunto de resultados.<br /><br />El valor predeterminado es 10240 KB (10 MB).<br /><br />Para obtener más información acerca de las consultas que crean un cursor de cliente, consulte [tipos de Cursor &#40; Controlador PDO_SQLSRV &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true<br /><br />false|Especifica la ejecución de la consulta directa o preparada. Para obtener más información, vea [Direct Statement Execution and Prepared Statement Execution in the PDO_SQLSRV Driver (Ejecución de la instrucción preparada o directa en el controlador PDO_SQLSRV)](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_ENCODING|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|PDO::SQLSRV_ENCODING_UTF8<br /><br />PDO::SQLSRV_ENCODING_SYSTEM.|Establece el juego de caracteres que utiliza el controlador para comunicarse con el servidor.<br /><br />No se admite PDO::SQLSRV_ENCODING_BINARY.<br /><br />El valor predeterminado es PDO::SQLSRV_ENCODING_UTF8.|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true o false|Controla capturas numéricos de las columnas con tipos SQL numéricos (bit, integer, smallint, tinyint, float o real).<br /><br />Cuando marca de la opción de conexión ATTR_STRINGIFY_FETCHES está activada, el valor devuelto es una cadena aunque SQLSRV_ATTR_FETCHES_NUMERIC_TYPE está activado.<br /><br />Cuando el tipo devuelto de PDO en la columna de enlace es PDO_PARAM_INT, el valor devuelto de una columna de tipo entero es un tipo int aunque SQLSRV_ATTR_FETCHES_NUMERIC_TYPE está desactivada.|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|integer|Establece el tiempo de espera de consulta en segundos.<br /><br />El valor predeterminado es 0, lo que significa que el controlador esperará indefinidamente para obtener los resultados.<br /><br />No se permiten números negativos.|  
|PDO::SQLSRV_CLIENT_BUFFER_MAX_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|integer|Establece el tamaño del búfer de consulta.<br /><br />El valor predeterminado es 0, que indica el tamaño de búfer ilimitado.<br /><br />No se permiten números negativos.<br /><br />Para obtener más información acerca de las consultas que crean un cursor de cliente, consulte [tipos de Cursor &#40; Controlador PDO_SQLSRV &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
  
PDO procesa algunos de los atributos predefinidos y requiere que el controlador procese otros. Todos los atributos personalizados y opciones de conexión se procesan mediante el controlador. Un atributo no admitido, la opción de conexión o el valor no admitido se notifica según la configuración de PDO:: attr_errmode.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
En este ejemplo se muestra cómo establecer el atributo PDO::ATTR_ERRMODE.  
  
```  
<?php  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
  
   $attributes1 = array( "ERRMODE" );  
   foreach ( $attributes1 as $val ) {  
      echo "PDO::ATTR_$val: ";  
      var_dump ($conn->getAttribute( constant( "PDO::ATTR_$val" ) ));  
   }  
  
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
  
   $attributes1 = array( "ERRMODE" );  
   foreach ( $attributes1 as $val ) {  
      echo "PDO::ATTR_$val: ";  
      var_dump ($conn->getAttribute( constant( "PDO::ATTR_$val" ) ));  
   }  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Clase PDO](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  
