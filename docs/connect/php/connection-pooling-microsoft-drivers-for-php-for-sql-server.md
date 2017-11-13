---
title: "Agrupación de conexiones (controladores de Microsoft para PHP para SQL Server) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection pooling support
ms.assetid: 4d9a83d4-08de-43a1-975c-0a94005edc94
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e536bbaee8f9dd934f24504e8c1226c9db7db9de
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>Agrupación de conexiones (controladores de Microsoft para PHP para SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

A continuación, se muestran consideraciones importantes que hay tener cuenta sobre la agrupación de conexiones en los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]:  
  
-   Los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] utilizan la agrupación de conexiones ODBC.  
  
-   De forma predeterminada, la agrupación de conexiones está habilitada en Windows. En Linux y Mac OS X, las conexiones se agrupan solo si la agrupación de conexiones está habilitada para ODBC. Cuando se habilita la agrupación de conexiones y se conecta a un servidor, el controlador intenta usar una conexión agrupada antes de crear uno nuevo. Si no encuentra una conexión equivalente en el grupo, se crea una nueva conexión y se agrega al grupo. El controlador determina si las conexiones son equivalentes según una comparación de las cadenas de conexión.  
  
-   Cuando se utiliza una conexión del grupo, se restablece el estado de conexión.  
  
-   Al cerrar la conexión, la conexión vuelve al grupo.  
  
Para obtener más información sobre la agrupación de conexiones, consulte [Driver Manager Connection Pooling](http://go.microsoft.com/fwlink/?linkid=119622)(Agrupación de conexiones del Administrador de controladores).  
  
## <a name="enablingdisabling-connection-pooling"></a>Agrupación de conexiones de habilitar/deshabilitar
### <a name="windows"></a>Windows
También puede forzar el controlador para crear una nueva conexión (en lugar de buscar una conexión equivalente en la agrupación de conexiones) estableciendo el valor de la *ConnectionPooling* atributo en la cadena de conexión para **false**  (o 0).  
  
Si el *ConnectionPooling* se omite el atributo de la cadena de conexión o si se establece en **true** (o 1), el controlador solo creará una nueva conexión si no existe una conexión equivalente en el grupo de conexiones.  
  
Para obtener información sobre otros atributos de conexión, consulte [Connection Options](../../connect/php/connection-options.md).  
### <a name="linux-and-mac-os-x"></a>Linux y Mac OS X
*ConnectionPooling* atributo no puede utilizarse para habilitar o deshabilitar la agrupación de conexiones. 

Agrupación de conexiones puede habilitarse o deshabilitarse mediante la edición de archivo de configuración de odbcinst.ini. Debe volver a cargar el controlador para que los cambios surtan efecto.

Establecer `Pooling` a `Yes` y positivo `CPTimeout`valor de odbcinst.ini habilita la agrupación de conexiones. 
```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
CPTimeout=<int value>
```
Establecer `Pooling` a `No` en odbcinst.ini obliga al controlador para crear una nueva conexión.
```
[ODBC]
Pooling=No
```
  
## <a name="see-also"></a>Vea también  
[Cómo conectarse mediante la autenticación de Windows](../../connect/php/how-to-connect-using-windows-authentication.md)  
[Cómo conectarse mediante la autenticación de SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
  

