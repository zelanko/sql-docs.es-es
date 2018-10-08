---
title: 'Cómo: conectarse a un puerto específico | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, specifying a port
ms.assetid: 65a154d1-375c-439b-a653-7815c9d70ff3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4d19077a4a0b676875a9b82acf529cc8720f31f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680028"
---
# <a name="how-to-connect-on-a-specified-port"></a>Cómo conectarse a un puerto específico
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se describe cómo conectarse a SQL Server en un puerto específico con los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
### <a name="to-connect-on-a-specified-port"></a>Pasos para conectarse a un puerto específico  
  
1.  Compruebe el puerto en que el servidor está configurado para aceptar conexiones. Para obtener información sobre cómo configurar un servidor para que acepte conexiones en un puerto específico, vea [Configurar un servidor para que escuche en un puerto TCP específico (Administrador de configuración de SQL Server)](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
2.  Agregue el puerto deseado al parámetro *$serverName* de la función [sqlsrv_connect](../../connect/php/sqlsrv-connect.md). Separe el nombre del servidor y el puerto con una coma. Por ejemplo, las siguientes líneas de código utilizan el controlador SQLSRV para demostrar cómo conectarse a un servidor denominado *myServer* en el puerto 1521:  
  
    ```  
    $serverName = "myServer, 1521";  
    sqlsrv_connect( $serverName );  
    ```  
  
    Las siguientes líneas de código usan el controlador PDO_SQLSRV para mostrar cómo conectarse a un servidor denominado *myServer* en el puerto 1521:  
  
    ```  
    $serverName = "(local), 1521";  
    $database = "AdventureWorks";  
    $conn = new PDO( "sqlsrv:server=$serverName;Database=$database", "", "");  
    ```  
  
## <a name="see-also"></a>Ver también  
[Conexión al servidor](../../connect/php/connecting-to-the-server.md)

[Programación de guía para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Introducción a los controladores de Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referencia del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
