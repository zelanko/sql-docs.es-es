---
title: Notificaciones de consulta en SQL Server
description: Describe cómo las aplicaciones .NET pueden solicitar notificaciones de SQL Server cuando los datos han cambiado.
ms.date: 08/15/2019
ms.assetid: 0f0ba1a1-3180-4af8-87f7-c795dc8f8f55
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: b5f4500645b60a98dd97166e12bdf0899149b1c4
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725606"
---
# <a name="query-notifications-in-sql-server"></a>Notificaciones de consulta en SQL Server

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Las notificaciones de consulta, creadas a partir de la infraestructura de Service Broker, permiten notificar a las aplicaciones si los datos han cambiado. Esta característica resulta especialmente útil para las aplicaciones que proporcionan una caché de información de una base de datos, como una aplicación web, y necesitan recibir notificaciones si se modifican los datos de origen.  
  
Hay tres maneras de implementar notificaciones de consulta mediante ADO.NET:  
  
- La implementación de bajo nivel se proporciona mediante la clase `SqlNotificationRequest` que expone la funcionalidad del servidor, lo que permite ejecutar un comando con una solicitud de notificación.  
  
- La implementación de alto nivel se proporciona mediante la clase `SqlDependency`, que es una clase que proporciona una abstracción de alto nivel de la funcionalidad de notificación entre la aplicación de origen y SQL Server, lo que permite utilizar una dependencia para detectar los cambios en el servidor. En la mayoría de los casos, esta es la manera más sencilla y eficaz de aprovechar la capacidad de notificaciones de SQL Server por parte de aplicaciones cliente administradas que usan el proveedor de datos Microsoft SqlClient para SQL Server.  
  
- Además, las aplicaciones web creadas mediante ASP.NET 2.0 o posterior pueden usar las clases auxiliares `SqlCacheDependency`.  
  
Las notificaciones de consulta se usan para las aplicaciones que necesitan actualizar las visualizaciones o las almacena en caché en respuesta a los cambios en los datos subyacentes. Microsoft SQL Server permite que las aplicaciones .NET envíen un comando a SQL Server y soliciten una notificación si la ejecución del mismo comando fuera a producir conjuntos de resultados diferentes de los inicialmente recuperados. Las notificaciones generadas en el servidor se envían a través de colas para procesarse más adelante.  
  
Puede configurar notificaciones para las instrucciones SELECT y EXECUTE. Cuando se usa una instrucción EXECUTE, SQL Server registra una notificación para el comando ejecutado en lugar de la propia instrucción EXECUTE. El comando debe cumplir los requisitos y las limitaciones de una instrucción SELECT. Cuando un comando que registra una notificación contiene más de una instrucción, el motor de base de datos crea una notificación para cada instrucción del lote.  
  
Si está desarrollando una aplicación donde sean necesarias notificaciones de subsegundo confiables cuando los datos cambien, revise las secciones **Planear una estrategia eficaz de notificaciones de consulta** y **Alternativas a las notificaciones de consulta** del tema [Planear notificaciones](/previous-versions/sql/sql-server-2008-r2/ms187528(v=sql.105)) de los Libros en pantalla de SQL Server. Para obtener más información de las notificaciones de consulta y SQL Server Service Broker, vea los siguientes vínculos a los temas de Libros en pantalla de SQL Server.  
  
**Documentación de SQL Server**  
  
- [Usar notificaciones de consulta](/previous-versions/sql/sql-server-2008-r2/ms175110(v=sql.105))  
  
- [Crear una consulta de notificación](/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Desarrollo (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522889(v=sql.105))  
  
- [Centro de información del desarrollador de Service Broker](/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [Guía del desarrollador (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="in-this-section"></a>En esta sección  
[Habilitación de notificaciones de consultas](enable-query-notifications.md)  
Describe cómo usar las notificaciones de consulta, incluidos los requisitos para habilitarlas y usarlas.  
  
[SqlDependency en una aplicación ASP.NET](sqldependency-aspnet-app.md)  
Muestra cómo usar notificaciones de consulta desde una aplicación de ASP.NET.  
  
[Detección de cambios con SqlDependency](detect-changes-sqldependency.md)  
Muestra cómo detectar cuándo los resultados de la consulta serán distintos de los recibidos originalmente.  
  
[Ejecución de SqlCommand con SqlNotificationRequest](sqlcommand-execution-sqlnotificationrequest.md)  
Muestra cómo configurar un objeto <xref:Microsoft.Data.SqlClient.SqlCommand> para que funcione con una notificación de consulta.  
  
## <a name="reference"></a>Referencia  
<xref:Microsoft.Data.Sql.SqlNotificationRequest>  
Describe la clase <xref:Microsoft.Data.Sql.SqlNotificationRequest> y todos sus miembros.  
  
<xref:Microsoft.Data.SqlClient.SqlDependency>  
Describe la clase <xref:Microsoft.Data.SqlClient.SqlDependency> y todos sus miembros.  
  
<xref:System.Web.Caching.SqlCacheDependency>  
Describe la clase <xref:System.Web.Caching.SqlCacheDependency> y todos sus miembros.  
  
## <a name="next-steps"></a>Pasos siguientes
- [SQL Server y ADO.NET](index.md)