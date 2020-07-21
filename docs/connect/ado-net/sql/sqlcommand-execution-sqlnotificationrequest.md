---
title: Ejecución de SqlCommand con SqlNotificationRequest
description: Muestra cómo configurar un objeto SqlCommand para que funcione con una notificación de consulta.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 1776f48f-9bea-41f6-83a4-c990c7a2c991
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 1ad2fd2f29c7218d1da0535ca089e2648d4b0cf0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80918684"
---
# <a name="sqlcommand-execution-with-a-sqlnotificationrequest"></a>Ejecución de SqlCommand con SqlNotificationRequest

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Se puede configurar un elemento <xref:Microsoft.Data.SqlClient.SqlCommand> para generar una notificación cuando los datos cambien después de que se hayan capturado desde el servidor, y el conjunto de resultados sería diferente si la consulta se ejecutara de nuevo. Esto resulta útil para los escenarios en los que desea usar colas de notificaciones personalizadas en el servidor o cuando no desea mantener objetos activos.

## <a name="creating-the-notification-request"></a>Creación de la solicitud de notificación

Puede usar un objeto <xref:Microsoft.Data.Sql.SqlNotificationRequest> para crear la solicitud de notificación enlazándolo a un objeto `SqlCommand`. Una vez creada la solicitud, ya no necesita el objeto `SqlNotificationRequest`. Puede consultar la cola para obtener las notificaciones y responder de forma adecuada. Las notificaciones pueden producirse incluso si la aplicación se cierra y se reinicia posteriormente.

Cuando se ejecuta el comando con la notificación asociada, los cambios en el conjunto de resultados original desencadenan el envío de un mensaje a la cola de SQL Server configurada en la solicitud de notificación.

El modo en el que se sondea la cola de SQL Server y se interpreta el mensaje es específico de la aplicación. La aplicación es responsable de sondear la cola y de reaccionar según el contenido del mensaje.

> [!NOTE]
> Al usar solicitudes de notificación de SQL Server con <xref:Microsoft.Data.SqlClient.SqlDependency>, cree su propio nombre de cola en lugar de usar el nombre de servicio predeterminado.

No hay nuevos elementos de seguridad del lado cliente para <xref:Microsoft.Data.Sql.SqlNotificationRequest>. Se trata principalmente de una característica de servidor, y el servidor ha creado privilegios especiales que los usuarios deben tener para solicitar una notificación.

### <a name="example"></a>Ejemplo

En el siguiente fragmento de código se muestra cómo crear un valor <xref:Microsoft.Data.Sql.SqlNotificationRequest> y asociarlo a <xref:Microsoft.Data.SqlClient.SqlCommand>.

```csharp
// Assume connection is an open SqlConnection.
// Create a new SqlCommand object.
SqlCommand command=new SqlCommand(
 "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection);

// Create a SqlNotificationRequest object.
SqlNotificationRequest notificationRequest=new SqlNotificationRequest();
notificationRequest.id="NotificationID";
notificationRequest.Service="mySSBQueue";

// Associate the notification request with the command.
command.Notification=notificationRequest;
// Execute the command.
command.ExecuteReader();
// Process the DataReader.
// You can use Transact-SQL syntax to periodically poll the
// SQL Server queue to see if you have a new message.
```

## <a name="next-steps"></a>Pasos siguientes
- [Notificaciones de consulta en SQL Server](query-notifications-sql-server.md)
