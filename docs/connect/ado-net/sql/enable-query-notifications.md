---
title: Habilitación de notificaciones de consultas
description: Describe cómo usar las notificaciones de consulta, incluidos los requisitos para habilitarlas y usarlas.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 94b472a1fe040aa3a684d9f7b523ba09c82a651e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452235"
---
# <a name="enabling-query-notifications"></a>Habilitación de notificaciones de consultas

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Las aplicaciones que consumen notificaciones de consulta tienen un conjunto común de requisitos. El origen de datos se debe configurar correctamente para que admita notificaciones de consulta SQL y el usuario debe contar con los permisos adecuados en el cliente y el servidor.  
  
Para usar notificaciones de consulta, debe:  
  
- Habilite las notificaciones de consulta para la base de datos.  
  
- Asegúrese de que el ID. de usuario usado para conectarse a la base de datos tiene los permisos necesarios.  
  
- Use un objeto <xref:Microsoft.Data.SqlClient.SqlCommand> para ejecutar una instrucción SELECT válida con un objeto de notificación asociado, ya sea <xref:Microsoft.Data.SqlClient.SqlDependency> o <xref:Microsoft.Data.Sql.SqlNotificationRequest>.  
  
- Proporcione código para procesar la notificación si los datos que se supervisan cambian.  
  
## <a name="query-notifications-requirements"></a>Requisitos de notificaciones de consulta  
Las notificaciones de consulta solo se admiten para las instrucciones SELECT que cumplen una lista de requisitos específicos. En la tabla siguiente se proporcionan vínculos a la documentación de Service Broker y de las notificaciones de consulta en Libros en pantalla de SQL Server.  
  
**Documentación de SQL Server**  
  
- [Crear una consulta de notificación](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Consideraciones de seguridad de Service Broker](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166059(v=sql.90))  
  
- [Seguridad y protección (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522911(v=sql.105))  
  
- [Consideraciones de seguridad de Notification Services](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms172604(v=sql.90))  
  
- [Permisos de notificación de consulta](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms188311(v=sql.105))  
  
- [Consideraciones internacionales de Service Broker](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166028(v=sql.90))  
  
- [Consideraciones de diseño de soluciones (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522899(v=sql.105))  
  
- [Centro de información del desarrollador de Service Broker](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [Guía del desarrollador (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="enabling-query-notifications-to-run-sample-code"></a>Habilitar las notificaciones de consulta para ejecutar código de ejemplo  
Para habilitar Service Broker en la base de datos **AdventureWorks** mediante SQL Server Management Studio, ejecute la siguiente instrucción de Transact-SQL:  
  
`ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
Para que los ejemplos de notificaciones de consulta se ejecuten correctamente, se deben ejecutar las siguientes instrucciones Transact-SQL en el servidor de base de datos.  
  
```sql
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a>Permisos de notificaciones de consulta  
Los usuarios que ejecutan comandos que solicitan una notificación deben tener el permiso de base de datos SUBSCRIBE QUERY NOTIFICAtions en el servidor.  
  
El código del lado cliente que se ejecuta en una situación de confianza parcial requiere el <xref:Microsoft.Data.SqlClient.SqlClientPermission>.  
  
En el código siguiente se crea un objeto <xref:Microsoft.Data.SqlClient.SqlClientPermission>, estableciendo el <xref:System.Security.Permissions.PermissionState> en <xref:System.Security.Permissions.PermissionState.Unrestricted>. El <xref:System.Security.CodeAccessPermission.Demand%2A> forzará un <xref:System.Security.SecurityException> en tiempo de ejecución si no se ha concedido el permiso a todos los llamadores situados en la parte superior de la pila de llamadas.  
  
[!code-csharp[DataWorks SqlClientPermission_Demand#1](~/../sqlclient/doc/samples/SqlClientPermission_Demand.cs#1)]
  
## <a name="choosing-a-notification-object"></a>Elección de un objeto de notificación  
La API de notificaciones de consulta proporciona dos objetos para procesar notificaciones: <xref:Microsoft.Data.SqlClient.SqlDependency> y <xref:Microsoft.Data.Sql.SqlNotificationRequest>.
  
### <a name="using-sqldependency"></a>Usar SqlDependency  
Para usar <xref:Microsoft.Data.SqlClient.SqlDependency>, Service Broker debe estar habilitado en la base de datos de SQL Server que se vaya a usar y los usuarios deben tener permisos para recibir notificaciones. Service Broker objetos, como la cola de notificación, están predefinidos.  
  
Además, <xref:Microsoft.Data.SqlClient.SqlDependency> inicia automáticamente un subproceso de trabajo para procesar las notificaciones a medida que se envían a la cola; también analiza el mensaje de Service Broker, que expone la información como datos de argumento de evento. <xref:Microsoft.Data.SqlClient.SqlDependency> debe inicializarse llamando al método `Start` para establecer una dependencia con la base de datos. Se trata de un método estático al que es necesario llamar solo una vez durante la inicialización de la aplicación para cada conexión de base de datos necesaria. Se debe llamar al método `Stop` en la finalización de la aplicación para cada conexión de dependencia realizada.  
  
### <a name="using-sqlnotificationrequest"></a>Usar SqlNotificationRequest  
Por el contrario, <xref:Microsoft.Data.Sql.SqlNotificationRequest> requiere la implementación de toda la infraestructura de escucha. Además, se deben definir todos los objetos de Service Broker de compatibilidad, como la cola, el servicio y los tipos de mensajes admitidos por la cola. Este enfoque manual es útil si la aplicación requiere mensajes de notificación especiales o comportamientos de notificación, o si la aplicación forma parte de una aplicación Service Broker mayor.  
  
## <a name="next-steps"></a>Pasos siguientes
- [Notificaciones de consulta en SQL Server](query-notifications-sql-server.md)
