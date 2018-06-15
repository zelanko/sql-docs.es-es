---
title: Mediante la agrupación de conexiones | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 699d4e8a-34bf-4c60-b0d5-4a10dad6084a
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c3b69e6cd19b493120a976c722db9d3efb01f57d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32851650"
---
# <a name="using-connection-pooling"></a>Usar agrupación de conexiones
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona compatibilidad para Java Platform, Enterprise Edition (Java EE) la agrupación de conexiones. El controlador JDBC implementa las interfaces necesarias de JDBC 3.0 para habilitar el controlador de modo que participe en la implementación de la agrupación de conexiones de los proveedores de software intermedio compatible con JDBC 3.0. El software intermedio, como los servidores de aplicaciones Java EE, suele ofrecer funciones de agrupación de conexiones compatibles. El controlador JDBC participa en las conexiones agrupadas de estos entornos.  
  
> [!NOTE]  
>  Aunque el controlador JDBC es compatible con la agrupación de conexiones de Java EE, no proporciona una implementación propia de la agrupación. El controlador se basa en los servidores de aplicación Java de otros fabricantes para administrar las conexiones.  
  
## <a name="remarks"></a>Comentarios  
 Las clases para la implementación de la agrupación de conexiones son las siguientes:  
  
|Clase|Implementaciones|Description|  
|-----------|----------------|-----------------|  
|com.Microsoft.SqlServer.JDBC. SQLServerXADataSource|javax.sql.ConnectionPoolDataSource y javax.sql.XADataSource|Se recomienda que realice la [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) necesita de clase para el servidor de Java EE, porque implementa todas las interfaces de la agrupación de JDBC 3.0 y XA.|  
|com.Microsoft.SqlServer.JDBC. SQLServerConnectionPoolDataSource|javax.sql.ConnectionPoolDataSource|Esta clase es un generador de conexiones que habilita el servidor de aplicaciones Java EE para rellenar su agrupación de conexiones con conexiones físicas. Si la configuración de su proveedor de Java EE requiere una clase que implementa javax.sql.ConnectionPoolDataSource, especifique el nombre de clase como [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md). Por lo general, se recomienda que realice la [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) clase en su lugar, porque implementa ambos agrupación y las interfaces XA y se ha comprobado en más configuraciones de servidor de Java EE.|  
  
 El código de aplicación de JDBC debe cerrar siempre las conexiones de forma explícita para obtener el máximo provecho de la agrupación. Si la aplicación cierra de forma explícita una conexión, la implementación de la agrupación puede volver a usar la conexión de inmediato. Si la conexión no está cerrada, las demás aplicaciones no pueden volver a usarla. Las aplicaciones pueden utilizar el `finally` construcción para asegurarse de que las conexiones agrupadas se cierran incluso si se produce una excepción.  
  
> [!NOTE]  
>  El controlador JDBC no llama al procedimiento almacenado sp_reset_connection al devolver la conexión al grupo. En su lugar, el controlador se basa en servidores de aplicaciones Java para devolver las conexiones a su estado original.  
  
## <a name="see-also"></a>Vea también  
 [Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
