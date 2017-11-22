---
title: sqlsrv_close | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: sqlsrv_close
apitype: NA
helpviewer_keywords:
- sqlsrv_close
- API Reference, sqlsrv_close
ms.assetid: 6ac6209c-a134-4f8f-b88b-8eefaa1cbc7f
caps.latest.revision: "25"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7e86837cabb40eda586ac7147e5559084d651d6d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="sqlsrvclose"></a>sqlsrv_close
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Cierra la conexión especificada y libera los recursos asociados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_close( resource $conn )  
```  
  
#### <a name="parameters"></a>Parámetros  
*$conn*: la conexión que se va a cerrar.  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve el valor booleano **True** , salvo que se llame a la función con un parámetro no válido. En este caso, se devolverá **False** .  
  
> [!NOTE]  
> **Null** es un parámetro válido para esta función. Esto permite que se llame varias veces a la función en un script. Por ejemplo, si cierra una conexión en una condición de error y se vuelve a cerrar al final de la secuencia de comandos, la segunda llamada a **sqlsrv_close** devolverá **true** porque la primera llamada a **sqlsrv_ cerrar** (en la condición de error) establece el recurso de conexión **null**.  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se cierra una conexión. En el ejemplo se da por hecho que SQL Server está instalado en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
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
  
//-----------------------------------------------  
// Perform operations with connection here.  
//-----------------------------------------------  
  
/* Close the connection. */  
sqlsrv_close( $conn);  
echo "Connection closed.\n";  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  
  
