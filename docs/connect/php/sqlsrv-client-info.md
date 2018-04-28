---
title: sqlsrv_client_info | Documentos de Microsoft
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
ms.topic: article
apiname:
- sqlsrv_client_info
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_client_info
- sqlsrv_client_info
ms.assetid: 3e2d3679-436a-45d8-8bdc-7c633b65a720
caps.latest.revision: 47
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 17c204fd5f7d84056591ff79cfe59ecb908b1ce2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsrvclientinfo"></a>sqlsrv_client_info
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Devuelve información sobre la pila de conexión y cliente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_client_info( resource $conn)  
```  
  
#### <a name="parameters"></a>Parámetros  
*$conn*: el recurso de conexión mediante el cual está conectado el cliente.  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve una matriz asociativa con las claves descritas en la tabla siguiente, o bien **False** si el valor del recurso de conexión es Null.  
  
**Para PHP (versiones 3.2 y 3.1 de SQL Server)**:  
  
|Key|Description|  
|-------|---------------|  
|DriverDllName|MSODBCSQL11.DLL (ODBC Driver 11 for SQL Server)|  
|DriverODBCVer|Versión de ODBC (xx.yy)|  
|DriverVer|Versión de la DLL de ODBC Driver 11 for SQL Server:<br /><br />xx.yy.zzzz ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versión 3.2 o 3.1)|  
|ExtensionVer|Versión de php_sqlsrv.dll:<br /><br />3.2.xxxx.x (para [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versión 3.2)<br /><br />3.1.xxxx.x (para [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versión 3.1)|  
  
**Para PHP (versiones 3.0 y 2.0 de SQL Server)**:  
  
|Key|Description|  
|-------|---------------|  
|DriverDllName|SQLNCLI10. DLL ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versión 2.0)|  
|DriverODBCVer|Versión de ODBC (xx.yy)|  
|DriverVer|Versión de la DLL de SQL Server Native Client:<br /><br />10.50. xxx ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versión 2.0)|  
|ExtensionVer|Versión de php_sqlsrv.dll:<br /><br />2.0.xxxx.x ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] versión 2.0)|  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se crea información del cliente en la consola cuando se ejecuta dicho ejemplo en la línea de comandos. En el ejemplo se da por hecho que SQL Server está instalado en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$conn = sqlsrv_connect( $serverName);  
  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
if( $client_info = sqlsrv_client_info( $conn))  
{  
       foreach( $client_info as $key => $value)  
      {  
              echo $key.": ".$value."\n";  
      }  
}  
else  
{  
       echo "Client info error.\n";  
}  
  
/* Close connection resources. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  
  
