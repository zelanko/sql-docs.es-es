---
title: 'Procedimientos: Conexión a un puerto específico'
description: Obtenga información sobre cómo conectarse a una base de datos configurada en un puerto específico mediante los controladores SQLSRV y PDO_SQLSRV de Microsoft para PHP para SQL Server.
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b55f12bbfe4bbe255af2d62c2ed0c5ab3f968e98
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435238"
---
# <a name="how-to-connect-on-a-specified-port"></a>Procedimientos: Conexión a un puerto específico
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se describe cómo conectarse a SQL Server en un puerto específico con los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
### <a name="to-connect-on-a-specified-port"></a>Pasos para conectarse a un puerto específico  
  
1.  Compruebe el puerto en que el servidor está configurado para aceptar conexiones. Para información sobre cómo configurar un servidor para que acepte conexiones en un puerto especificado, consulte [Procedimiento: Configurar un servidor para que escuche en un puerto TCP específico (Administrador de configuración de SQL Server)](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)  
  
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
  
## <a name="see-also"></a>Consulte también  
[Conexión al servidor](../../connect/php/connecting-to-the-server.md)

[Guía de programación para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Introducción a los controladores de Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referencia del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
