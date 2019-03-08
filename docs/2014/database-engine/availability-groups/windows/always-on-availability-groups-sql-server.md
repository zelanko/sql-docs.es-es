---
title: Grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- secondary replicas, see Availability Groups [SQL Server]
- availability [SQL Server]
- AlwaysOn [SQL Server], see Availability Groups [SQL Server]
- Availability Groups [SQL Server]
ms.assetid: aa427606-8422-4656-b205-c9e665ddc8c1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bedea60c8bc356ff18b687123799977d83f308c5
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2019
ms.locfileid: "57578755"
---
# <a name="always-on-availability-groups-sql-server"></a>Grupos de disponibilidad AlwaysOn (SQL Server)
  La característica [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] es una solución de alta disponibilidad y de recuperación ante desastres que proporciona una alternativa empresarial a la creación de reflejo de la base de datos. Incorporada en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] maximiza la disponibilidad de un conjunto de bases de datos de usuario para una empresa. Un *grupo de disponibilidad* admite un entorno de conmutación por error para un conjunto discreto de bases de datos de usuario, conocido como *bases de datos de disponibilidad*, que realizan la conmutación por error conjuntamente. Un grupo de disponibilidad admite un conjunto de bases de datos principales de lectura y escritura y de uno a ocho conjuntos de bases de datos secundarias correspondientes. Opcionalmente, las bases de datos secundarias pueden estar disponibles para el acceso de solo lectura o para algunas operaciones de copia de seguridad.  
  
 Un grupo de disponibilidad realiza la conmutación por error en el nivel de réplica de disponibilidad. Las conmutaciones por error no se deben a problemas de bases de datos como que una base de datos pase a ser sospechosa debido a la pérdida de un archivo de datos, la eliminación de una base de datos o los daños de un registro de transacciones.  
  
  
##  <a name="Benefits"></a> Ventajas  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] proporciona un amplio conjunto de opciones que mejoran la disponibilidad de las bases de datos y que permiten el uso de recursos mejorado. Los componentes clave son los siguientes:  
  
-   Admite hasta nueve réplicas de disponibilidad. Una *réplica de disponibilidad* es una instancia de un grupo de disponibilidad hospedado en una instancia específica de SQL Server y que mantiene una copia local de cada base de datos de disponibilidad perteneciente al grupo de disponibilidad. Cada grupo de disponibilidad admite una réplica principal y hasta ocho réplicas secundarias. Para obtener más información, vea [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  
    > [!IMPORTANT]  
    >  Cada réplica de disponibilidad debe residir en otro nodo de un único clúster de clústeres de conmutación por error de Windows Server (WSFC). Para obtener más información sobre los requisitos previos, restricciones y recomendaciones para grupos de disponibilidad, consulte [requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn; SQL Server. ](prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   Admite modos de disponibilidad alternativos como los siguientes:  
  
    -   *Modo de confirmación asincrónica*. Este modo de disponibilidad es una solución de recuperación de desastres que funciona bien cuando las réplicas de disponibilidad se distribuyen sobre distancias considerables.  
  
    -   *Modo de confirmación sincrónica*. Este modo de disponibilidad resalta alta disponibilidad y protección de datos del rendimiento, a costa de aumentar la latencia de las transacciones. Un grupo de disponibilidad determinado puede admitir hasta tres réplicas de disponibilidad de confirmación sincrónica, incluida la réplica principal actual.  
  
     Para obtener más información, consulte [modos de disponibilidad. Grupos de disponibilidad; Always On ](availability-modes-always-on-availability-groups.md).  
  
-   Admite varias formas de conmutación por error de un grupo de disponibilidad: conmutación automática por error, conmutación por error manual planeada (suele denominarse simplemente "conmutación por error manual") y conmutación por error manual forzada (suele denominarse simplemente "conmutación por error forzada"). Para obtener más información, consulte [conmutación por error y modos de conmutación por error. Grupos de disponibilidad; Always On ](failover-and-failover-modes-always-on-availability-groups.md).  
  
-   Permite configurar una réplica de disponibilidad determinada que admite una o dos de las funciones secundarias activas siguientes:  
  
    -   Tener acceso de conexión de solo lectura, que permite conexiones de solo lectura a la réplica para obtener acceso y leer sus bases de datos cuando se ejecuta como una réplica secundaria. Para más información, consulte [Secundarias activas: Réplicas secundarias legibles; Grupos de disponibilidad Always On](https://msdn.microsoft.com/library/ff878253.aspx)).  
  
    -   Realizar operaciones de copia de seguridad en sus bases de datos cuando se ejecuta como una réplica secundaria. Para más información, consulte [Secundarias activas: Copia de seguridad en réplicas secundarias](https://msdn.microsoft.com/library/ff878253.aspx)).  
  
     Con capacidades secundarias activas se mejora la eficiencia de los procesos de TI y se reducen los costos mediante la mejor utilización de los recursos del hardware secundario. Además, las aplicaciones de lectura de descarga y los trabajos de copia de seguridad de las réplicas secundarias ayudan a mejorar el rendimiento de la réplica primaria.  
  
-   Admite un agente de escucha del grupo de disponibilidad para cada grupo de disponibilidad. Un *agente de escucha del grupo de disponibilidad* es un nombre de servidor al que los clientes pueden conectarse para tener acceso a una base de datos en una réplica principal o secundaria de un grupo de disponibilidad AlwaysOn. Los agentes de escucha del grupo de disponibilidad dirigen las conexiones entrantes a la réplica principal o una réplica secundaria de solo lectura. El agente de escucha proporciona conmutación por error rápida de aplicaciones después de que se produzca la conmutación por error del grupo de disponibilidad. Para obtener más información, consulte [los agentes de escucha del grupo de disponibilidad, conectividad de cliente y conmutación por error de la aplicación; SQL Server. ](../../listeners-client-connectivity-application-failover.md).  
  
-   Admite una directiva flexible de conmutación por error para un mayor control sobre una conmutación por error del grupo de disponibilidad. Para obtener más información, consulte [conmutación por error y modos de conmutación por error. Grupos de disponibilidad; Always On ](failover-and-failover-modes-always-on-availability-groups.md).  
  
-   Admite la reparación automática de páginas para ofrecer protección frente al daño en las páginas. Para obtener más información, consulte [reparación de página automática &#40;para grupos de disponibilidad y la creación de reflejo de base de datos;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md).  
  
-   Admite el cifrado y compresión, que proporcionan un transporte seguro y de alto rendimiento.  
  
-   Proporciona un conjunto integrado de herramientas para simplificar la implementación y administración de los grupos de disponibilidad, como:  
  
    -   [!INCLUDE[tsql](../../../includes/tsql-md.md)] para crear y administrar grupos de disponibilidad. Para obtener más información, consulte [información general de instrucciones de Transact-SQL para el grupo de disponibilidad AlwaysOn; SQL Server. ](transact-sql-statements-for-always-on-availability-groups.md).  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] son las siguientes:  
  
        -   [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] crea y configura un grupo de disponibilidad. En algunos entornos, este asistente puede también preparar automáticamente las bases de datos secundarias e iniciar la sincronización de datos de cada una de ellas. Para obtener más información, consulte [utilice el cuadro de diálogo nuevo de grupo de disponibilidad; SQL Server Management Studio; ](use-the-new-availability-group-dialog-box-sql-server-management-studio.md).  
  
        -   [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] agrega una o más bases de datos principales a un grupo de disponibilidad. En algunos entornos, este asistente puede también preparar automáticamente las bases de datos secundarias e iniciar la sincronización de datos de cada una de ellas. Para obtener más información, vea [Usar el Asistente para agregar una base de datos al grupo de disponibilidad (SQL Server)](availability-group-add-database-to-group-wizard.md).  
  
        -   [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] agrega una o varias réplicas secundarias a un grupo de disponibilidad. En algunos entornos, este asistente puede también preparar automáticamente las bases de datos secundarias e iniciar la sincronización de datos de cada una de ellas. Para obtener más información, consulte [usar Agregar una réplica al Asistente para grupo de disponibilidad; SQL Server Management Studio; ](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md).  
  
        -   [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)] inicia una conmutación manual por error en un grupo de disponibilidad. Dependiendo de la configuración y el estado de la réplica secundaria que se especifique como destino de la conmutación por error, el asistente puede realizar una conmutación por error manual planeada o forzada. Para obtener más información, consulte [usar el error a través de asistente grupo de disponibilidad; SQL Server Management Studio; ](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md).  
  
    -   [!INCLUDE[ssAoDash](../../../includes/ssaodash-md.md)] supervisa los grupos de disponibilidad AlwaysOn, las réplicas de disponibilidad y las bases de datos de disponibilidad y evalúa los resultados de las directivas de AlwaysOn. Para obtener más información, consulte [utilice el panel de AlwaysOn SQL Server Management Studio; ](use-the-always-on-dashboard-sql-server-management-studio.md).  
  
    -   El panel Detalles del Explorador de objetos muestra información básica acerca de los grupos de disponibilidad existentes. Para obtener más información, consulte [usar los detalles del explorador de objetos al grupo de disponibilidad de Monitor; SQL Server Management Studio; ](use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Cmdlets de PowerShell. Para obtener más información, consulte [información general de los Cmdlets de PowerShell para grupos de disponibilidad AlwaysOn; SQL Server; ](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md).  
  
##  <a name="TermsAndDefinitions"></a> Términos y definiciones  
 grupo de disponibilidad  
 Contenedor para un conjunto de bases de datos, las *bases de datos de disponibilidad*, que conmutan por error juntas.  
  
 base de datos de disponibilidad  
 Base de datos que pertenece a un grupo de disponibilidad. Para cada base de datos de disponibilidad, el grupo de disponibilidad mantiene una sola copia de lectura y escritura (la *base de datos principal*) y de una a ocho copias de solo lectura (*bases de datos secundarias*).  
  
 base de datos principal  
 La copia de lectura y escritura de una base de datos de disponibilidad.  
  
 base de datos secundaria  
 Una copia de solo lectura de una base de datos de disponibilidad.  
  
 réplica de disponibilidad  
 Creación de instancia de un grupo de disponibilidad hospedado por una instancia específica de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y mantiene una copia local de cada base de datos de disponibilidad perteneciente al grupo de disponibilidad. Existen dos tipos de réplicas de disponibilidad: una sola *réplica principal* y de una a ocho *réplicas secundarias*.  
  
 réplica principal  
 La réplica de disponibilidad que hace que las bases de datos principales estén disponibles para las conexiones de lectura y escritura de clientes y, además, envía las entradas del registro de transacciones para cada base de datos principal a cada réplica secundaria.  
  
 réplica secundaria  
 Réplica de disponibilidad que mantiene una copia secundaria de cada base de datos de disponibilidad y actúa como posible destino de conmutación por error para el grupo de disponibilidad. Opcionalmente, una réplica secundaria puede admitir acceso de solo lectura a bases de datos secundarias y la creación de copias de seguridad de bases de datos secundarias.  
  
 agente de escucha de grupo de disponibilidad  
 Nombre del servidor al que los clientes pueden conectarse para tener acceso a una base de datos en una réplica principal o secundaria de un grupo de disponibilidad AlwaysOn. Los agentes de escucha del grupo de disponibilidad dirigen las conexiones entrantes a la réplica principal o una réplica secundaria de solo lectura.  
  
> [!NOTE]  
>  Para obtener más información, consulte [información general de grupos de disponibilidad AlwaysOn; SQL Server; ](overview-of-always-on-availability-groups-sql-server.md).  
  
##  <a name="Interoperability"></a> Interoperabilidad y coexistencia con otras características del motor de base de datos  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] se puede utilizar con las siguientes características o componentes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   [Acerca de la captura de datos modificados; SQL Server.](../../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
-   [Seguimiento de cambios; SQL Server;](../../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
-   [Bases de datos independientes](../../../relational-databases/databases/contained-databases.md)  
  
-   [Clave de cifrado de la base de datos](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
-   [Instantáneas de base de datos](database-snapshots-with-always-on-availability-groups-sql-server.md)  
  
-   [FILESTREAM](../../../relational-databases/blob/filestream-sql-server.md)  
  
-   [FileTable](../../../relational-databases/blob/filetables-sql-server.md)  
  
-   [Trasvase de registros](../../log-shipping/about-log-shipping-sql-server.md)  
  
-   [Almacén remoto de blobs (RBS)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
-   [Replicación](../../install-windows/install-sql-server-replication.md)  
  
-   [Service Broker](../../configure-windows/sql-server-service-broker.md)  
  
-   [Agente SQL Server](../../../ssms/agent/sql-server-agent.md)  
  
-   [Reporting Services](reporting-services-with-always-on-availability-groups-sql-server.md)  
  
> [!WARNING]  
>  Para más información sobre las restricciones y limitaciones para usar otras características con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vea [Grupos de disponibilidad Always On: Interoperabilidad; SQL Server. ](always-on-availability-groups-interoperability-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Introducción a AlwaysOn en grupos de disponibilidad; SQL Server.](getting-started-with-always-on-availability-groups-sql-server.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   **Blogs:**  
  
     [Blogs del equipo de Always On de SQL Server: El blog del equipo de AlwaysOn oficial SQL Server](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs de los ingenieros de SQL Server de CSS](https://blogs.msdn.com/b/psssql/)  
  
-   **Vídeos:**  
  
     [Microsoft SQL Server Code-Named "Denali", Serie Always On, parte 1: Introducción a la solución de alta disponibilidad de próxima generación](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Code-Named "Denali", Serie Always On, parte 2: Creación de una solución esencial de alta disponibilidad utilizando AlwaysOn](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Notas del producto:**  
  
     [Guía de soluciones AlwaysOn de Microsoft SQL Server para lograr alta disponibilidad y recuperación ante desastres](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
  
  
## <a name="see-also"></a>Vea también  
 [Información general de AlwaysOn de grupos de disponibilidad; SQL Server.](overview-of-always-on-availability-groups-sql-server.md)   
 [Requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Configuración de una instancia de servidor para grupos de disponibilidad; Always On SQL Server.](always-on-availability-groups-sql-server.md)   
 [Creación y configuración de grupos de disponibilidad; SQL Server.](creation-and-configuration-of-availability-groups-sql-server.md)   
 [Administración de un grupo de disponibilidad; SQL Server.](administration-of-an-availability-group-sql-server.md)   
 [Supervisión de los grupos de disponibilidad &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [Información general sobre instrucciones Transact-SQL para grupos de disponibilidad; Always On SQL Server.](transact-sql-statements-for-always-on-availability-groups.md)   
 [Introducción a los PowerShell Cmdlets para grupos de disponibilidad AlwaysOn; SQL Server.](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
  
