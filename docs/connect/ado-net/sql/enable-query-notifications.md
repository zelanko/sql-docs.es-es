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
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 2648f8efbae6cc6665ea3ab984b27012a2a1ebc7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920427"
---
# <a name="enabling-query-notifications"></a>Habilitación de notificaciones de consultas

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Las aplicaciones que consumen notificaciones de consulta tienen un conjunto común de requisitos. El origen de datos se debe configurar correctamente para que admita notificaciones de consulta SQL y el usuario debe contar con los permisos adecuados en el cliente y el servidor.  
  
Para usar notificaciones de consulta, debe hacer lo siguiente:  
  
- Habilitar las notificaciones de consulta para la base de datos.  
  
- Asegurarse de que el identificador de usuario usado para conectarse a la base de datos tiene los permisos necesarios.  
  
- Usar un objeto <xref:Microsoft.Data.SqlClient.SqlCommand> para ejecutar una instrucción SELECT válida con un objeto de notificación asociado, ya sea <xref:Microsoft.Data.SqlClient.SqlDependency> o <xref:Microsoft.Data.Sql.SqlNotificationRequest>.  
  
- Proporcionar código para procesar la notificación si los datos que se supervisan cambian.  
  
## <a name="query-notifications-requirements"></a>Requisitos de las notificaciones de consultas  
Se admiten notificaciones de consultas solo para las instrucciones SELECT que cumplan un listado de requisitos específicos. En la tabla siguiente se proporcionan vínculos a la documentación de Service Broker y las notificaciones de consulta en Libros en pantalla de SQL Server.  
  
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
  
## <a name="enabling-query-notifications-to-run-sample-code"></a>Habilitación de las notificaciones de consulta para ejecutar código de ejemplo  
Para habilitar Service Broker en la base de datos **AdventureWorks** mediante SQL Server Management Studio, ejecute la siguiente instrucción de Transact-SQL:  
  
`ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
Para que los ejemplos de notificaciones de consulta se ejecuten correctamente, se deben ejecutar las siguientes instrucciones Transact-SQL en el servidor de base de datos.  
  
```sql
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a>Permisos de notificación de consulta  
Los usuarios que ejecutan comandos que solicitan una notificación deben tener el permiso de base de datos SUBSCRIBE QUERY NOTIFICATIONS en el servidor.  
  
El código del lado cliente que se ejecuta en una situación de confianza parcial requiere <xref:Microsoft.Data.SqlClient.SqlClientPermission>.  
  
El código siguiente crea un objeto <xref:Microsoft.Data.SqlClient.SqlClientPermission>, estableciendo <xref:System.Security.Permissions.PermissionState> en <xref:System.Security.Permissions.PermissionState.Unrestricted>. <xref:System.Security.CodeAccessPermission.Demand%2A> forzará a <xref:System.Security.SecurityException> en un entorno de ejecución si todos los autores de llamada situados en la parte superior de la pila de llamadas no disponen del permiso.  
  
[!code-csharp[DataWorks SqlClientPermission_Demand#1](~/../sqlclient/doc/samples/SqlClientPermission_Demand.cs#1)]
  
## <a name="choosing-a-notification-object"></a>Elección de un objeto de notificación  
La API de notificaciones de consulta proporciona dos objetos para procesar notificaciones: <xref:Microsoft.Data.SqlClient.SqlDependency> y <xref:Microsoft.Data.Sql.SqlNotificationRequest>.
  
### <a name="using-sqldependency"></a>Uso de SqlDependency  
Para usar <xref:Microsoft.Data.SqlClient.SqlDependency>, Service Broker debe estar habilitado en la base de datos de SQL Server que se vaya a usar y los usuarios deben tener permisos para recibir notificaciones. Los objetos de Service Broker, como la cola de notificación, están predefinidos.  
  
Además, <xref:Microsoft.Data.SqlClient.SqlDependency> inicia automáticamente un subproceso de trabajo para procesar las notificaciones que se publican en la cola; también analiza el mensaje de Service Broker y expone la información en forma de datos de argumento de evento. <xref:Microsoft.Data.SqlClient.SqlDependency> se debe inicializar llamando al método `Start` para establecer una dependencia en la base de datos. Se trata de un método estático al que es necesario llamar solo una vez durante la inicialización de la aplicación para cada conexión de base de datos necesaria. Se debe llamar al método `Stop` en la finalización de la aplicación para cada conexión de dependencia realizada.  
  
### <a name="using-sqlnotificationrequest"></a>Uso de SqlNotificationRequest  
Por el contrario, <xref:Microsoft.Data.Sql.SqlNotificationRequest> requiere que implemente toda la infraestructura de escucha. Además, se deben definir todos los objetos de Service Broker de compatibilidad, como la cola, el servicio y los tipos de mensajes admitidos por la cola. Este enfoque manual es útil si la aplicación requiere mensajes de notificación o comportamientos de notificación especiales, o si la aplicación forma parte de una aplicación Service Broker mayor.  
  
## <a name="next-steps"></a>Pasos siguientes
- [Notificaciones de consulta en SQL Server](query-notifications-sql-server.md)
