---
title: Procedimientos para deshabilitar los conjuntos de resultados activos múltiples (MARS)
description: Obtenga información sobre cómo deshabilitar la compatibilidad con los conjuntos de resultados activos múltiples al usar los controladores de Microsoft para PHP en SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple active result sets, disabling
- MARS, disabling
ms.assetid: 1912ad05-d0a4-40ff-8888-0d85bb36a807
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 11ca08618f0b8d7675e8ec74ec259d4225d44aba
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/15/2020
ms.locfileid: "92080624"
---
# <a name="how-to-disable-multiple-active-resultsets-mars"></a>Procedimientos: Desactivación de los conjuntos de resultados activos múltiples (MARS)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Si necesita conectarse a un origen de datos de SQL Server que no habilite conjuntos de resultados activos múltiples (MARS), puede utilizar la opción de conexión MultipleActiveResultSets para deshabilitar o habilitar MARS.  
  
## <a name="procedure"></a>Procedimiento  
  
#### <a name="to-disable-mars-support"></a>Pasos para deshabilitar la compatibilidad con MARS  
  
-   Utilice la opción de conexión siguiente:  
  
    ```  
    'MultipleActiveResultSets'=>false  
    ```  
  
    Si la aplicación trata de ejecutar una consulta en una conexión que tiene un conjunto de resultados activo pendiente, el segundo intento de consulta devolverá la información de error siguiente:  
  
    La conexión no puede procesar esta operación porque no hay una instrucción con resultados pendientes.  Para que la conexión esté disponible en otras consultas, capture todos los resultados, o bien cancele o libere la instrucción. Para obtener más información sobre la opción de conexión MultipleActiveResultSets, consulte [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="sqlsrv-example"></a>Ejemplo de SQLSRV  
En el ejemplo siguiente se muestra cómo deshabilitar la compatibilidad con MARS utilizando el controlador SQLSRV de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", 'MultipleActiveResultSets'=> false);  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="pdo_sqlsrv-example"></a>Ejemplo de PDO_SQLSRV  
En el ejemplo siguiente se muestra cómo deshabilitar la compatibilidad con MARS con el controlador PDO_SQLSRV de [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
```  
<?php  
// Connect to the local server using Windows Authentication and AdventureWorks database  
$serverName = "(local)";   
$database = "AdventureWorks";  
  
try {  
   $conn = new PDO(" sqlsrv:server=$serverName ; Database=$database ; MultipleActiveResultSets=false ", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );   
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
$conn = null;   
?>  
```  
  
## <a name="see-also"></a>Consulte también  
[Conexión al servidor](../../connect/php/connecting-to-the-server.md)  
  
