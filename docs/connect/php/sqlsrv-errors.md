---
title: sqlsrv_errors | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_errors
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_errors
- sqlsrv_errors
- errors and warnings
ms.assetid: d1fcffec-f34f-46de-9a0e-343f3b5dbae2
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e097a5b89d708b3a91296c49c0c615f8955b96cb
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35309054"
---
# <a name="sqlsrverrors"></a>sqlsrv_errors
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Devuelve extendidos información de error o advertencia de la última **sqlsrv** operación realizada.  
  
El **sqlsrv_errors** función puede devolver información de error o advertencia llamando a uno de los valores de parámetro especificados en la siguiente sección de parámetros.  
  
De forma predeterminada, las advertencias generadas en una llamada a cualquier función de **sqlsrv** se tratan como errores; si se produce una advertencia en una llamada a una función de **sqlsrv** , se devuelve el valor False. Sin embargo, las advertencias que se corresponden con los valores 01000, 01001, 01003 y 01S02 de SQLSTATE nunca se tratan como errores.  
  
La siguiente línea de código desactiva el comportamiento anterior; las advertencias generadas mediante una llamada a una función de **sqlsrv** no consiguen que dicha función devuelva el valor False:  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 0);  
```  
  
La siguiente línea de código restaura el comportamiento predeterminado; las advertencias (con las excepciones mencionadas anteriormente) se tratan como errores:  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 1);  
```  
  
Independientemente de la configuración, las advertencias solo se pueden recuperar mediante una llamada a **sqlsrv_errors** con cualquiera el **SQLSRV_ERR_ALL** o **SQLSRV_ERR_WARNINGS** valor del parámetro (consulte Sección parámetros más adelante para obtener más información).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_errors( [int $errorsAndOrWarnings] )  
```  
  
#### <a name="parameters"></a>Parámetros  
*$errorsAndOrWarnings*[opcional]: una constante predefinida. Este parámetro puede tomar uno de los valores que se muestran en la siguiente tabla:  
  
|Valor|Descripción|  
|---------|---------------|  
|SQLSRV_ERR_ALL|Se devuelven los errores y las advertencias generados en la última llamada a una función de **sqlsrv** .|  
|SQLSRV_ERR_ERRORS|Se devuelven los errores generados en la última llamada a una función de **sqlsrv** .|  
|SQLSRV_ERR_WARNINGS|Se devuelven las advertencias generadas en la última llamada a una función de **sqlsrv** .|  
  
Si no se especifica ningún valor de parámetro, se devuelven los errores y las advertencias generados mediante la última llamada a una función de **sqlsrv** .  
  
## <a name="return-value"></a>Valor devuelto  
Una **matriz** de matrices, o bien el valor **Null**. Cada **matriz** en el valor devuelto **matriz** contiene tres pares de clave-valor. En la siguiente tabla se muestra cada una de las claves con su descripción:  
  
|Key|Descripción|  
|-------|---------------|  
|SQLSTATE|En los errores que se originan desde el controlador ODBC, el valor de SQLSTATE que devuelve ODBC. Para obtener información acerca de los valores SQLSTATE para ODBC, vea [códigos de Error de ODBC](../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md).<br /><br />Para los errores que se originan desde los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], un valor de SQLSTATE de IMSSP.<br /><br />Para las advertencias que se originan desde los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], un valor de SQLSTATE de 01SSP.|  
|código|Para los errores que se originan desde SQL Server, el código de error de SQL Server nativo.<br /><br />Para los errores que se originan desde el controlador ODBC, el código de error que devuelve ODBC.<br /><br />Para los errores que se originan desde los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], el código de error de dichos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] . Para obtener más información, consulte [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md).|  
|message|Descripción del error.|  
  
También se pueden consultar los valores de matriz con las claves numéricas 0, 1 y 2. Si no se produce ningún error ni advertencia, se devuelve el valor **Null** .  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se muestran los errores que se producen durante la ejecución de una instrucción que no se realizó correctamente (La instrucción produce un error porque **InvalidColumName** no es un nombre de columna válido de la tabla especificada.) El ejemplo supone que SQL Server y el [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) base de datos se instalan en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
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
  
/* Set up a query to select an invalid column name. */  
$tsql = "SELECT InvalidColumnName FROM Sales.SalesOrderDetail";  
  
/* Attempt execution. */  
/* Execution will fail because of the invalid column name. */  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
      if( ($errors = sqlsrv_errors() ) != null)  
      {  
         foreach( $errors as $error)  
         {  
            echo "SQLSTATE: ".$error[ 'SQLSTATE']."\n";  
            echo "code: ".$error[ 'code']."\n";  
            echo "message: ".$error[ 'message']."\n";  
         }  
      }  
}  
  
/* Free connection resources */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  
  
