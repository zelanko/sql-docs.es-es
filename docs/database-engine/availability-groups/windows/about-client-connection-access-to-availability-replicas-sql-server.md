---
title: "Acerca del acceso de conexi&#243;n de cliente a r&#233;plicas de disponibilidad (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Grupos de disponibilidad [SQL Server], réplicas de disponibilidad"
  - "Grupos de disponibilidad [SQL Server], réplicas secundarias legibles"
  - "réplicas secundarias activas [SQL Server], acceso de solo lectura a"
  - "Grupos de disponibilidad [SQL Server], configurar"
  - "Grupos de disponibilidad [SQL Server], conectividad de cliente"
  - "Grupos de disponibilidad [SQL Server], réplicas secundarias activas"
ms.assetid: 29027e46-43e4-4b45-b650-c4cdeacdf552
caps.latest.revision: 16
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 15
---
# Acerca del acceso de conexi&#243;n de cliente a r&#233;plicas de disponibilidad (SQL Server)
  En un grupo de disponibilidad AlwaysOn, puede configurar una o varias réplicas de disponibilidad para permitir conexiones de solo lectura cuando se ejecutan en el rol secundario (es decir, cuando se ejecutan como réplica secundaria). También puede configurar cada réplica de disponibilidad para permitir o excluir conexiones de solo lectura cuando se ejecutan bajo el rol principal (es decir, cuando se ejecutan como réplica principal).  
  
 Para facilitar el acceso de cliente a las bases de datos principal o secundaria de un grupo de disponibilidad determinado, puede definir un agente de escucha del grupo de disponibilidad. De forma predeterminada, el agente de escucha del grupo de disponibilidad dirige las conexiones entrantes a la réplica principal. Sin embargo, puede configurar un grupo de disponibilidad de modo que se admita el enrutamiento de solo lectura, lo que permite a su agente de escucha del grupo de disponibilidad redirigir las solicitudes de conexión de las aplicaciones de intención de lectura a una réplica secundaria legible. Para obtener más información, vea [Configurar el enrutamiento de solo lectura para un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md).  
  
 Durante una conmutación por error, una réplica secundaria realiza la transición al rol principal y la réplica principal anterior realiza la transición al rol secundario. Durante el proceso de conmutación por error, se terminan todas las conexiones de cliente a la réplica principal y a las réplicas secundarias. Después de la conmutación por error, cuando un cliente se vuelve a conectar al agente de escucha del grupo de disponibilidad, el agente de escucha vuelve a conectar el cliente a la nueva réplica principal, excepto en el caso de una solicitud de conexión de intención de lectura. Si se configura el enrutamiento de solo lectura en el cliente, en las instancias de servidor que hospedan la nueva réplica principal y en al menos una réplica secundaria legible, las solicitudes de conexión de intención de lectura se vuelven a enrutar a una réplica secundaria que admita el tipo de acceso de conexión que el cliente necesita. Para asegurar una experiencia de cliente correcta después de una conmutación por error, es importante configurar el acceso de conexión de los roles principal y secundario de cada réplica de disponibilidad.  
  
> [!NOTE]  
>  Para obtener información sobre el agente de escucha de grupo de disponibilidad, que administra las solicitudes de conexión de cliente, vea [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners, client connectivity, application failover.md).  
  
 **En este tema:**  
  
-   [Tipos de acceso de conexión admitidos por el rol secundario](#ConnectAccessForSecondary)  
  
-   [Tipos de acceso de conexión admitidos por el rol principal](#ConnectAccessForPrimary)  
  
-   [Cómo la configuración de acceso de conexión afecta a la conectividad de cliente](#HowConnectionAccessAffectsConnectivity)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
-   [Contenido relacionado](#RelatedContent)  
  
##  <a name="ConnectAccessForSecondary"></a> Tipos de acceso de conexión admitidos por el rol secundario  
 El rol secundario admite tres alternativas para las conexiones de cliente, del siguiente modo:  
  
 Sin conexiones  
 No se permiten conexiones de usuario. Las bases de datos secundarias no están disponibles para acceso de lectura. este es el comportamiento predeterminado del rol secundario.  
  
 Solo conexiones de intención de lectura  
 Las bases de datos secundarias solo están disponibles para la conexión en que la propiedad de conexión **Application Intent** está establecida en **ReadOnly** (*conexiones de intención de lectura*).  
  
 Para obtener información acerca de esta conexión, vea [SQL Server Native Client Support for High Availability, Disaster Recovery](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
 Permitir cualquier conexión de solo lectura  
 Todas las bases de datos secundarias están disponibles para conexiones de acceso de lectura. Esta opción permite la conexión a los clientes de una versión anterior.  
  
 Para obtener más información, vea [Configurar el acceso de solo lectura en una réplica de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md).  
  
##  <a name="ConnectAccessForPrimary"></a> Tipos de acceso de conexión admitidos por el rol principal  
 El rol principal admite dos alternativas para las conexiones de cliente, del siguiente modo:  
  
 Todas las conexiones están permitidas  
 Se permiten conexiones de lectura/escritura y de solo lectura a las bases de datos principales. Este es el comportamiento predeterminado para el rol principal.  
  
 Permitir solo conexiones de lectura/escritura  
 Cuando la propiedad de conexión **Application Intent** se establece en **ReadWrite** o no se establece, se permite la conexión. No se permiten conexiones en que la palabra clave de cadena de conexión **Application Intent** se establece en **ReadOnly** . La acción de permitir conexiones de lectura/escritura puede impedir que los clientes conecten una carga de trabajo de intención de lectura a la réplica principal por error.  
  
 Para obtener información acerca de esta conexión, vea [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Para obtener más información, vea [Configurar el acceso de solo lectura en una réplica de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md).  
  
##  <a name="HowConnectionAccessAffectsConnectivity"></a> Cómo la configuración de acceso de conexión afecta a la conectividad de cliente  
 La configuración de acceso de conexión de una réplica determina si un intento de conexión se produce o no correctamente. La tabla siguiente resume si un intento de conexión determinado se produce o no correctamente para cada configuración de acceso de conexión.  
  
|Rol de réplica|Acceso de conexión admitido en la réplica|Intento de conexión|Resultado del intento de conexión|  
|------------------|--------------------------------------------|-----------------------|--------------------------------|  
|Secundario|Todos|Se ha especificado una intención de lectura, una intención de lectura/escritura o ninguna intención de conexión|Success|  
|Secundario|Ninguno (este es el comportamiento secundario predeterminado).|Se ha especificado una intención de lectura, una intención de lectura/escritura o ninguna intención de conexión|Failure|  
|Secundario|Solo intento de lectura|Intención de lectura|Success|  
|Secundario|Solo intento de lectura|Se ha especificado una intención de lectura/escritura o ninguna intención de conexión|Failure|  
|Principal|Todos (este es el comportamiento principal predeterminado).|Se ha especificado una intención de solo lectura, una intención de lectura/escritura o ninguna intención de conexión|Success|  
|Principal|Lectura-escritura|Solo intento de lectura|Failure|  
|Principal|Lectura-escritura|Se ha especificado una intención de lectura/escritura o ninguna intención de conexión|Success|  
  
 Para obtener información sobre cómo configurar un grupo de disponibilidad para aceptar conexiones de cliente a sus réplicas, vea [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners, client connectivity, application failover.md).  
  
### Ejemplo de configuración de acceso de conexión  
 Dependiendo de cómo estén configuradas diferentes réplicas de disponibilidad para acceso de conexión, la compatibilidad para las conexiones de cliente puede cambiar después de la conmutación por error de un grupo de disponibilidad. Por ejemplo, considere un grupo de disponibilidad para el que se realiza funcionalidad de informes en las réplicas secundarias de confirmación asincrónica remota. En todas las aplicaciones de solo lectura para las bases de datos de este grupo de disponibilidad se establece la propiedad de conexión **Application Intent** en **ReadOnly**, de modo que todas las conexiones de solo lectura son de intención de lectura.  
  
 Este grupo de disponibilidad de ejemplo posee dos réplicas de confirmación sincrónica en el centro de cálculo principal y dos réplicas de confirmación asincrónica en un sitio satélite. Para el rol principal, todas las réplicas se configuran para acceso de lectura/escritura, lo que evita las conexiones de intención de lectura a la réplica principal en todas las situaciones. El rol secundario de confirmación sincrónica utiliza la configuración de acceso de conexión predeterminada (“ninguna”), evitando las conexiones de cliente bajo el rol secundario.  En cambio, las réplicas de confirmación asincrónica se configuran para permitir conexiones de intención de lectura bajo el rol secundario. En la tabla siguiente se resume esta configuración de ejemplo:  
  
|Réplica|Modo de confirmación|Rol inicial|Acceso de conexión para el rol secundario|Acceso de conexión para el rol principal|  
|-------------|-----------------|------------------|------------------------------------------|----------------------------------------|  
|Réplica1|Sincrónica|Principal|Ninguno|Lectura-escritura|  
|Réplica2|Sincrónica|Secundario|Ninguno|Lectura-escritura|  
|Réplica3|Asincrónica|Secundario|Solo intención de lectura|Lectura-escritura|  
|Réplica4|Asincrónica|Secundario|Solo intento de lectura|Lectura-escritura|  
  
 Normalmente, en este escenario de ejemplo, las conmutaciones por error solo se producen entre las réplicas de confirmación sincrónica, e inmediatamente después de la conmutación por error, las aplicaciones de intención de lectura pueden volver a conectarse a una de las réplicas secundarias de confirmación asincrónica. Sin embargo, cuando se produce un desastre en el centro de cálculo principal se pierden las réplicas de confirmación sincrónica. El administrador de base de datos en el sitio satélite responde realizando una conmutación por error manual forzada a una réplica secundaria de confirmación asincrónica. Las bases de datos secundarias de la réplica secundaria restante son suspendidas por la conmutación por error forzada, haciendo que no estén disponibles para las cargas de trabajo de solo lectura. La nueva réplica principal, configurada para las conexiones de lectura/escritura, impide que la carga de trabajo de intención de lectura compita con la carga de trabajo de lectura/escritura. Esto significa que hasta que el administrador de base de datos reanude las bases de datos secundarias de la réplica secundaria de confirmación asincrónica restante, los clientes de intención de lectura no pueden conectarse a ninguna réplica de disponibilidad.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Configurar el acceso de solo lectura en una réplica de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar el enrutamiento de solo lectura para un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
-   [Ver las propiedades de una réplica de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
-   [Usar el cuadro de diálogo Nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Guía de soluciones AlwaysOn de Microsoft SQL Server para lograr alta disponibilidad y recuperación ante desastres](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Blog del equipo de AlwaysOn de SQL Server: blog oficial del equipo de AlwaysOn de SQL Server](http://blogs.msdn.com/b/sqlAlways%20On/)  
  
## Vea también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners, client connectivity, application failover.md)   
 [Estadísticas](../../../relational-databases/statistics/statistics.md)  
  
  