---
title: Requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], WSFC clusters
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], prerequisites and restrictions
- Availability Groups [SQL Server], Failover Cluster Instances
- Availability Groups [SQL Server], databases
- Availability Groups [SQL Server]
ms.assetid: edbab896-42bb-4d17-8d75-e92ca11f7abb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9a0f8896903c2a7f817efcfa8dcc238ce0532f90
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48151905"
---
# <a name="prerequisites-restrictions-and-recommendations-for-alwayson-availability-groups-sql-server"></a>Requisitos previos, restricciones y recomendaciones para Grupos de disponibilidad AlwaysOn (SQL Server)
  En este tema se describen las consideraciones para implementar [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], incluidos los requisitos previos, restricciones y recomendaciones para equipos host, los clústeres de conmutación por error de Windows Server (WSFC), las instancias del servidor y los grupos de disponibilidad. Para cada uno de estos componentes, se indican los criterios de seguridad y permisos necesarios, si existen.  
  
> [!IMPORTANT]  
>  Antes de implementar [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], le recomendamos encarecidamente que lea todas las secciones de este tema.  
  
 
  
##  <a name="DotNetHotfixes"></a> Revisiones de .net que admiten grupos de disponibilidad AlwaysOn  
 Según los componentes y características de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que use con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], puede que tenga que instalar las revisiones de .Net adicionales identificadas en la tabla siguiente. Las revisiones pueden instalarse en cualquier orden.  
  
||Característica dependiente|Revisión|Vínculo|  
|------|-----------------------|------------|----------|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]|La revisión para .Net 3.5 SP1 agrega compatibilidad con las características SQL Client para AlwaysOn de intención de lectura, solo lectura y conmutación por error de multisubred. La revisión tiene que instalarse en cada servidor de informes [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|KB 2654347: [Revisión para .Net 3.5 SP1 para agregar compatibilidad con las características AlwaysOn](http://go.microsoft.com/fwlink/?LinkId=242896)|  
  
##  <a name="SystemReqsForAOAG"></a> Requisitos del sistema de Windows y recomendaciones  
  
  
###  <a name="SystemRequirements"></a> Lista de comprobación: requisitos (sistema de Windows)  
 Para admitir la característica de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , asegúrese de que cada equipo que vaya a participar en uno o varios grupos de disponibilidad cumpla los requisitos básicos siguientes:  
  
||Requisito|Vínculo|  
|------|-----------------|----------|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Asegúrese de que el sistema no es un controlador de dominio.|No se admiten grupos de disponibilidad en los controladores de dominio.|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Asegúrese de que cada equipo esté ejecutando Windows Server 2008 x86 (no WOW64) o x64 o versiones posteriores.|WOW64 (Windows de 32 bits de Windows de 64 bits) no admite [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Asegúrese de que cada equipo es un nodo de un clúster de conmutación por error de Windows Server (WSFC).|[Clústeres de conmutación por error de Windows Server &#40;WSFC&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Asegúrese de que el clúster de WSFC contiene los nodos suficientes para admitir las configuraciones de grupo de disponibilidad.|Un nodo de WSFC solo puede hospedar una única réplica de disponibilidad para un grupo de disponibilidad dado. En un nodo determinado de WSFC, una o más instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueden hospedar las réplicas de disponibilidad de muchos grupos de disponibilidad.<br /><br /> Consulte a los administradores de bases de datos cuántos nodos de WSFC se requieren para admitir las réplicas de disponibilidad de los grupos de disponibilidad planeados.<br /><br /> [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Asegúrese de que todas las revisiones aplicables de Windows se hayan instalado en cada nodo del clúster de WSFC.|**\*\* Importante \* \***  un número de revisiones se requieren o recomiendan para los nodos de un WSFC de clúster en el que [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] se va a implementar. Para obtener más información, vea [Revisiones de Windows que admiten los grupos de disponibilidad AlwaysOn (Windows System)](#WinHotfixes), más adelante en esta sección.|  
  
> [!IMPORTANT]  
>  Asegúrese también de que el entorno esté configurado correctamente para conectarse a un grupo de disponibilidad. Para obtener más información, consulte [conectividad de cliente de AlwaysOn (SQL Server)](always-on-client-connectivity-sql-server.md).  
  
####  <a name="WinHotfixes"></a> Revisiones de Windows que admiten los grupos de disponibilidad AlwaysOn (Windows System)  
 Dependiendo de la topología de clúster, podrían aplicarse varias revisiones adicionales de Windows Server 2008 Service Pack 2 (SP2) o Windows Server 2008 R2 para admitir [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. En la tabla siguiente se identifican estas revisiones. Las revisiones pueden instalarse en cualquier orden.  
  
||Se aplica a Windows 2008 SP2|Se aplica a Windows 2008 R2 SP1|Incluido en Windows 2012|Para admitir…|Revisión|Vínculo|  
|------|---------------------------------|------------------------------------|------------------------------|-----------------|------------|----------|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|√|√|Sí|**Configuración de quórum óptimo de WSFC**|En cada nodo de WSFC, asegúrese de que esté instalada la revisión descrita en el artículo 2494036 de Knowledge Base.<br /><br /> Esta revisión admite quórum óptimo de configuración con los destinos no automáticos de conmutación por error. Esta funcionalidad mejora los clústeres de varios sitios que permite seleccionar a qué nodos se vota.|KB 2494036:  [Hay disponible una revisión que permite configurar un nodo del clúster que no tiene los votos de quórum en Windows Server 2008 y Windows Server 2008 R2](http://support.microsoft.com/kb/2494036)<br /><br /> Para obtener información sobre la votación del cuórum, vea [Configuración de los votos y modos de cuórum WSFC &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|√|√|Sí|**Uso más eficaz del ancho de banda de red**|En cada nodo WSFC, asegúrese de que esté instalada la revisión descrita en el artículo 2616514 de Knowledge Base.<br /><br /> Sin esta revisión, el servicio Cluster envía notificaciones innecesarias del Registro entre los nodos del clúster. Este comportamiento limita el ancho de banda de red, que es un problema grave para [!INCLUDE[ssHADRc](../../../includes/sshadrc-md.md)].|KB 2616514:  [El servicio de clúster envía notificaciones de cambio de claves del Registro innecesarias entre los nodos del clúster en Windows Server 2008 o en Windows Server 2008 R2](http://support.microsoft.com/kb/2616514)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")||√|No aplicable|**Prueba en los discos que no están disponibles para todos los nodos WSFC del almacenamiento VPD**|Si un nodo de WSFC ejecuta Windows Server 2008 R2 Service Pack 1 (SP1) y la prueba de almacenamiento Validar datos vitales de producto (VPD) de dispositivo SCSI produce errores una vez que se ejecuta incorrectamente en los discos que están en línea y no disponibles para todos los nodos del clúster de WSFC, instale de la revisión descrita en el artículo 2531907 de Knowledge Base.<br /><br /> Esta revisión elimina las advertencias o errores incorrectos en el informe de validación cuando los discos están en línea.|KB 2531907:  [La prueba Validar datos vitales de producto (VPD) de dispositivo SCSI produce un error después de instalar Windows Server 2008 R2 SP1](http://support.microsoft.com/kb/2531907)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")||√|Sí|**Rápida conmutación por error a las réplicas locales**|Si un nodo de WSFC ejecuta Windows Server 2008 R2 Service Pack 1 (SP1), asegúrese de que la revisión descrita en el artículo 2687741 de Knowledge Base esté instalada.<br /><br /> Esta revisión mejora el rendimiento de la conmutación por error de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] a las réplicas locales.|2687741 KB:  [Una revisión que mejora el rendimiento “del grupo de AlwaysOn disponibilidad de la función” en SQL Server 2012 está disponible en Windows Server 2008 R2](http://support.microsoft.com/KB/2687741)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|√|√|Sí|**Almacenamiento asimétrico, para las instancias de clúster de conmutación por error (FCI)**|Si las instancias de clúster de conmutación por error (FCI) van a estar habilitadas para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], instale la revisión 976097 de Windows Server 2008.<br /><br /> Esta revisión habilita el complemento Microsoft Management Console (MMC) de administración de clúster de conmutación por error para admitir los discos asimétricos de almacenamiento compartido que están disponibles en solo algunos de los nodos de WSFC.|KB 976097:  [Revisión para agregar compatibilidad con los almacenamientos asimétricos al complemento MMC de administración de clústeres de conmutación por error para un clúster de conmutación por error que ejecute Windows Server 2008 o Windows Server 2008 R2](http://support.microsoft.com/kb/976097)<br /><br /> [Guía de arquitectura de AlwaysOn: Generar una alta disponibilidad y la solución de recuperación ante desastres mediante instancias de clúster de conmutación por error y grupos de disponibilidad](http://technet.microsoft.com/library/jj215886.aspx)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|√|√|No aplicable|**Protocolo de seguridad de Internet (IPsec)**|Si un entorno usa conexiones IPsec, puede experimentar un retraso prolongado (aproximadamente de dos o tres minutos) cuando un equipo cliente restablece la conexión IPsec con un nombre de red virtual (en este contexto, para conectarse al agente de escucha del grupo de disponibilidad). Si usa conexiones IPsec, recomendamos que revise los escenarios específicos detallados en el artículo de Knowledge Base (KB 980915).|KB 980915:  [Se produce un retraso prolongado cuando se vuelve a conectar una conexión de IPsec desde un equipo que ejecuta Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 o Windows Server 2008 R2](http://support.microsoft.com/kb/980915)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|√|√|Sí|**IPv6**|Si usa IPv6, recomendamos que revise los escenarios específicos detallados en el artículo de Knowledge Base 2578103 o 2578113, en función de su sistema operativo Windows Server.<br /><br /> Si la topología de Windows Server usa IP versión 6 (IPv6), el servicio de clúster WSFC requiere en torno a 30 segundos para la conmutación por error de la dirección IP IPv6. Esto hace que los clientes esperen aproximadamente 30 segundos para volver a conectarse a la dirección IP IPv6.|KB 2578103 (Windows Server 2008):  [El servicio de clúster tarda en torno a 30 segundos en la conmutación por error de las direcciones IP IPv6 en Windows Server 2008](http://support.microsoft.com/kb/2578103)<br /><br /> KB 2578113 (Windows Server 2008 R2):  **Windows Server 2008 R2:** [El servicio de clúster tarda en torno a 30 segundos en la conmutación por error de las direcciones IP IPv6 en Windows Server 2008 R2](http://support.microsoft.com/kb/2578113)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|√|√|Sí|**Ningún enrutador entre clúster y aplicación de servidor**|Si no hay ningún enrutador entre el clúster de conmutación por error y el servidor de aplicaciones, el servicio de Cluster Server realiza con lentitud la conmutación por error de los recursos relacionados con la red. Esto retrasa las conexiones de cliente después de producirse la conmutación por error del grupo de disponibilidad. Si no hay un enrutador, se recomienda revisar los escenarios concretos detallados en el artículo de Knowledge Base 2582281 e instalar la revisión, si es aplicable a su entorno.|KB 2582281:  [Reducir la operación de conmutación por error si no existe un enrutador entre el clúster y un servidor de aplicaciones](http://support.microsoft.com/kb/2582281)|  
  
###  <a name="ComputerRecommendations"></a> Recomendaciones para equipos que hospedan réplicas de disponibilidad (sistema de Windows)  
  
-   **Sistemas comparables:**  en un grupo de disponibilidad determinado, todas las réplicas de disponibilidad deben ejecutarse en sistemas comparables que puedan controlar cargas de trabajo idénticas.  
  
-   **Adaptadores de red dedicados:**  para obtener el mejor rendimiento, use un adaptador de red (tarjeta de interfaz de red) dedicado para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].  
  
-   **Espacio en disco suficiente:**  todos los equipos en los que una instancia del servidor hospeda una réplica de disponibilidad deben poseer suficiente espacio en disco para todas las bases de datos del grupo de disponibilidad. Tenga en cuenta que según crecen las bases de datos principales, las correspondientes bases de datos secundarias aumentan la misma cantidad.  
  
###  <a name="PermissionsWindows"></a> Permisos (sistema de Windows)  
 Para administrar un clúster de WSFC, el usuario debe ser administrador del sistema en cada nodo de clúster.  
  
 Para obtener más información sobre la cuenta para la administración del clúster, vea [Apéndice A: requisitos para un clúster de conmutación por error](http://technet.microsoft.com/library/dd197454\(WS.10\).aspx).  
  
###  <a name="RelatedTasksWindows"></a> Tareas relacionadas (sistema de Windows)  
  
|Tarea|Vínculo|  
|----------|----------|  
|Establecer el valor de HostRecordTTL.|[Cambiar el valor de HostRecordTTL (con Windows PowerShell)](#ChangeHostRecordTTLps)|  
  
####  <a name="ChangeHostRecordTTLps"></a> Cambiar el valor de HostRecordTTL (con Windows PowerShell)  
  
1.  Abra la ventana de PowerShell mediante **Ejecutar como administrador**.  
  
2.  Importe el módulo FailoverClusters.  
  
3.  Utilice la `Get-ClusterResource` cmdlet para encontrar el recurso de nombre de red y, después, usar `Set-ClusterParameter` cmdlet para establecer el `HostRecordTTL` valor, como se indica a continuación:  
  
     Get-ClusterResource “*\<nombreRecursoRed>*” | Set-ClusterParameter HostRecordTTL *\<tiempoEnSegundos>*  
  
     En el ejemplo siguiente de PowerShell se establece el HostRecordTTL en 300 segundos para un recurso de nombre de red denominado “`SQL Network Name (SQL35)`”.  
  
    ```  
    Import-Module FailoverClusters  
  
    $nameResource = "SQL Network Name (SQL35)"  
    Get-ClusterResource $nameResource | Set-ClusterParameter ClusterParameter HostRecordTTL 300  
    ```  
  
    > [!TIP]  
    >  Cada vez que abre una nueva ventana de PowerShell, deberá importar el `FailoverClusters` módulo.  
  
##### <a name="related-content-powershell"></a>Contenido relacionado (PowerShell)  
  
-   [Clustering and High-Availability (Clústeres y alta disponibilidad)](http://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (blog del equipo de Agrupacion de clústeres de conmutación por error y equilibrio de carga de red)  
  
-   [Introducción a Windows PowerShell en un clúster de conmutación por error](http://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [Comandos de recursos de clúster y cmdlets equivalentes de Windows PowerShell](http://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
###  <a name="RelatedContentWS"></a> Contenido relacionado (sistema Windows)  
  
-   [Configurar los valores de DNS en un clúster de conmutación por error de varios sitios](http://technet.microsoft.com/library/dd197562\(WS.10\).aspx)  
  
-   [Registro DNS con el recurso de nombre de red](http://blogs.msdn.com/b/clustering/archive/2009/07/17/9836756.aspx)  
  
-   [Windows 2008 R2 conmutación por error de agrupación en clústeres multisitio](http://www.microsoft.com/windowsserver2008/en/us/failover-clustering-multisite.aspx)  
  
##  <a name="ServerInstance"></a> Requisitos previos y restricciones de las instancias de SQL Server  
 Cada grupo de disponibilidad requiere un conjunto de asociados de conmutación por error, conocido como *réplicas de disponibilidad*, que se hospedan en instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Una instancia del servidor determinada puede ser una *instancia independiente* o una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]*instancia de clúster de conmutación por error* (FCI).  
  
 
  
###  <a name="PrerequisitesSI"></a> Lista de comprobación: requisitos previos (instancia del servidor)  
  
||Requisito previo|Vínculos|  
|-|------------------|-----------|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|El equipo host debe ser en un nodo de clúster de conmutación por error de Windows Server (WSFC). Las instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedan las réplicas de disponibilidad de un grupo de disponibilidad dado deben residir en nodos independientes de un único clúster de WSFC. La única excepción es que mientras se migra a otro clúster de WSFC, un grupo de disponibilidad puede ocupar temporalmente dos clústeres.|[Clústeres de conmutación por error de Windows Server &#40;WSFC&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)<br /><br /> [Agrupación en clústeres de conmutación por error y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Si desea que un grupo de disponibilidad trabaje con Kerberos:<br /><br /> Todas las instancias de servidor que hospedan una réplica de disponibilidad para el grupo de disponibilidad deben usar la misma cuenta de servicio de SQL Server.<br /><br /> El administrador de dominio debe registrar manualmente un nombre principal de servicio (SPN) con Active Directory en la cuenta del servicio SQL Server para el nombre de red virtual (VNN) del agente de escucha del grupo de disponibilidad. Si el SPN se registra en una cuenta distinta de la cuenta del servicio SQL Server, la autenticación no se realizará correctamente.<br /><br /> **\*\* Importante \*\*** Si cambia la cuenta del servicio SQL Server, el administrador de dominio deberá volver a registrar manualmente el SPN.|[Registrar un nombre principal de servicio para las conexiones con Kerberos](../../configure-windows/register-a-service-principal-name-for-kerberos-connections.md)<br /><br /> **Breve explicación:**<br /><br /> Kerberos y los SPN exigen la autenticación mutua. El SPN se asigna a la cuenta de Windows que inicia los servicios SQL Server. Si el SPN no se registra correctamente o provoca un error, el nivel de seguridad de Windows no podrá determinar la cuenta asociada al SPN y no podrá utilizarse la autenticación Kerberos.<br /><br /> Nota: NTLM no tiene este requisito.|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Si va a usar una instancia de clúster de conmutación por error (FCI) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para hospedar una réplica de disponibilidad, asegúrese de que comprende las restricciones de FCI y de que se cumplen los requisitos de FCI.|[Requisitos previos y requisitos para usar una instancia de clúster de conmutación por error (FCI) de SQL Server para hospedar una réplica de disponibilidad](#FciArLimitations) (más adelante en este tema)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Cada instancia del servidor se debe estar ejecutando en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]Enterprise Edition.|[Características compatibles con las ediciones de SQL Server 2014](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Todas las instancias del servidor que hospedan réplicas de disponibilidad para un grupo de disponibilidad deben usar la misma intercalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|[Configurar o cambiar la intercalación del servidor](../../../relational-databases/collations/set-or-change-the-server-collation.md)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Habilite la característica de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en cada instancia de servidor que hospeda una réplica de disponibilidad para cualquier grupo de disponibilidad. En un equipo determinado, puede habilitar tantas instancias de servidor de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] como admita la instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|[Habilitar y deshabilitar grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)<br /><br /> **\*\* Importante \*\*** Si elimina y vuelve a crear un clúster de WSFC, debe deshabilitar y volver a habilitar la característica [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en cada instancia del servidor habilitada para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en el clúster de WSFC original.|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Cada instancia del servidor requiere un extremo de creación de reflejo de la base de datos. Observe que todas las réplicas de disponibilidad, asociados de creación de reflejo de la base de datos y testigos de la instancia del servidor comparten este extremo.<br /><br /> Si una instancia de servidor seleccionada para hospedar una réplica de disponibilidad se ejecuta bajo una cuenta de usuario de dominio y no tiene todavía un punto de conexión de creación de reflejo de la base de datos, el [Asistente para nuevo grupo de disponibilidad](use-the-availability-group-wizard-sql-server-management-studio.md) (o el [asistente Agregar réplica a grupo de disponibilidad](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)) puede crear el punto de conexión y conceder el permiso CONNECT a la cuenta de servicio de la instancia de servidor. Sin embargo, si el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se ejecuta como una cuenta integrada (como sistema local, servicio local o servicio de red), o una cuenta que no es de dominio, debe usar certificados para la autenticación de extremos y el asistente no podrá crear un extremo de creación de reflejo de la base de datos en la instancia de servidor. En este caso, se recomienda crear los extremos de creación de reflejo de la base de datos manualmente antes de iniciar el asistente.<br /><br /> **\*\* Nota de seguridad \*\*** La seguridad de transporte para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] es la misma que para la creación de reflejo de la base de datos.|[El punto de conexión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)<br /><br /> [Seguridad de transporte para la creación de reflejo de base de datos y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-mirroring/transport-security-database-mirroring-always-on-availability.md)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Si va a agregar cualquier base de datos que usa FILESTREAM a un grupo de disponibilidad, asegúrese de que FILESTREAM está habilitado en cada instancia de servidor que hospedará una réplica de disponibilidad para el grupo de disponibilidad.|[Enable and Configure FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Si las bases de datos independientes se agregará a un grupo de disponibilidad, asegúrese de que el `contained database authentication` servidor opción está establecida en `1` en cada instancia del servidor que hospedará una réplica de disponibilidad del grupo de disponibilidad.|[contained database authentication (opción de configuración del servidor)](../../configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [Opciones de configuración de servidor &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)|  
  
###  <a name="ThreadUsage"></a> Uso de subprocesos por parte de los grupos de disponibilidad  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] tiene los siguientes requisitos para los subprocesos de trabajo:  
  
-   En una instancia inactiva de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] usa 0 subprocesos.  
  
-   El número máximo de subprocesos usados por los grupos de disponibilidad es el valor configurado para el número máximo de subprocesos de servidor ('`max worker threads`') menos 40.  
  
-   Las réplicas de disponibilidad hospedadas en una instancia de servidor dada comparten un único grupo de subprocesos.  
  
     Los subprocesos se comparten a petición, de la manera siguiente:  
  
    -   Normalmente, hay entre 3 y 10 subprocesos compartidos, pero este número puede aumentar según la carga de réplica principal.  
  
    -   Si un subproceso determinado está inactivo durante un tiempo, se libera de nuevo en el grupo de subprocesos general de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Normalmente, un subproceso inactivo se libera después de unos 15 segundos de inactividad. Sin embargo, dependiendo de la última actividad, un subproceso inactivo se puede conservar más tiempo.  
  
-   Además, los grupos de disponibilidad usan subprocesos no compartidos, de la manera siguiente:  
  
    -   Cada réplica principal usa 1 subproceso de captura de registro para cada base de datos principal. Además, usa 1 subproceso de envío de registro para cada base de datos secundaria. Los subprocesos de envío de registro se liberan después de unos 15 segundos de inactividad.  
  
    -   Cada réplica secundaria usa 1 subproceso de rehacer para cada base de datos secundaria. Los subprocesos de rehacer se liberan después de unos 15 segundos de inactividad.  
  
    -   Una copia de seguridad en una réplica secundaria contiene un subproceso en la réplica principal mientras dura la operación de copia de seguridad.  
  
 Para más información, vea [Series de aprendizaje de AlwaysON - HADRON: uso del grupo de trabajo para las bases de datos compatibles con HADRON](http://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx) (un blog de los ingenieros de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de CSS).  
  
###  <a name="PermissionsSI"></a> Permisos (instancia del servidor)  
  
|Tarea|Permisos necesarios|  
|----------|--------------------------|  
|Crear el extremo de creación de reflejo de la base de datos|Requiere permiso CREATE ENDPOINT o pertenecer al rol fijo de servidor **sysadmin** .  También requiere el permiso CONTROL ON ENDPOINT. Para obtener más información, vea [GRANT &#40;permisos de punto de conexión de Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql).|  
|Habilitar [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]|Requiere la pertenencia al grupo **Administrador** en el equipo local y control total del clúster de WSFC.|  
  
###  <a name="RelatedTasksSI"></a> Tareas relacionadas (instancia del servidor)  
  
|Tarea|Tema|  
|----------|-----------|  
|Determinar si existe un extremo de creación de reflejo de la base de datos|[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)|  
|Crear el extremo de creación de reflejo de la base de datos (si aún no existe)|[Crear un punto de conexión de creación de reflejo de la base de datos para la autenticación de Windows &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)<br /><br /> [Usar certificados para un punto de conexión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)<br /><br /> [Crear una base de datos de extremo de reflejo para grupos de disponibilidad AlwaysOn &#40;PowerShell de SQL Server&#41;](database-mirroring-always-on-availability-groups-powershell.md)|  
|Habilitar los grupos de disponibilidad de AlwaysOn|[Habilitar y deshabilitar grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)|  
  
###  <a name="RelatedContentSI"></a> Contenido relacionado (instancia del servidor)  
  
-   [AlwaysON - HADRON Learning Series: Bases de datos de uso del grupo de trabajo de HADRON habilitadas](http://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
##  <a name="NetworkConnect"></a> Recomendaciones de conectividad de red  
 Se recomienda que utilice los mismos vínculos de red para las comunicaciones entre los miembros del clúster de WSFC y las comunicaciones entre las réplicas de disponibilidad.  El uso de vínculos de red independientes puede provocar comportamientos inesperados si alguno de los vínculos da error (incluso de forma intermitente).  
  
 Por ejemplo, para que un grupo de disponibilidad admita la conmutación por error automática, la réplica secundaria que sea el asociado de conmutación por error automática debe tener el estado SYNCHRONIZED. Si el vínculo de red a esta réplica secundaria da error (incluso de forma intermitente), la réplica entra en el estado UNSYNCHRONIZED y no puede iniciarse para volver a sincronizar hasta que se restaure el vínculo. Si el clúster WSFC solicita una conmutación por error automática mientras la réplica secundaria está desincronizada, la conmutación por error automática no aparecerá.  
  
##  <a name="ClientConnSupport"></a> Compatibilidad con conectividad de cliente  
 Para obtener información acerca de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] admiten conectividad de cliente, vea [conectividad de cliente de AlwaysOn (SQL Server)](always-on-client-connectivity-sql-server.md).  
  
##  <a name="FciArLimitations"></a> Requisitos previos y restricciones para usar una instancia de clúster de conmutación por error (FCI) de SQL Server para hospedar una réplica de disponibilidad  
 
  
###  <a name="RestrictionsFCI"></a> Restricciones (FCI)  
  
> [!NOTE]  
>  A partir de [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], las instancias del clúster de conmutación por error de AlwaysOn admiten los volúmenes compartidos en clúster (CSV) en [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] y [!INCLUDE[win8srv](../../../includes/win8srv-md.md)]. Para obtener más información sobre CSV, vea [Descripción de Volúmenes compartidos de clúster en un clúster de conmutación por error](http://technet.microsoft.com/library/dd759255.aspx).  
  
-   **Los nodos de clúster de una FCI solo pueden hospedar una réplica para un grupo de disponibilidad determinado**  : Si agrega una réplica de disponibilidad en una FCI, los nodos de clúster de WSFC que sean posibles propietarios de FCI no pueden hospedar otra réplica para el mismo grupo de disponibilidad.  
  
     Además, todas las demás réplicas deben hospedarse en una instancia de SQL Server 2012 que resida en otro nodo de WSFC en el mismo clúster de WSFC. La única excepción es que mientras se migra a otro clúster de WSFC, un grupo de disponibilidad puede ocupar temporalmente dos clústeres.  
  
-   **Las FCI no admiten la conmutación automática por error por grupos de disponibilidad**  : Las FCI no admiten la conmutación automática por error por grupos de disponibilidad; por tanto, todas las réplicas de disponibilidad hospedadas por una FCI solo se pueden configurar para la conmutación por error manual.  
  
-   **Cambiar el nombre de red de FCI:**  si necesita cambiar el nombre de red de una FCI que hospede una réplica de disponibilidad, tendrá que quitar la réplica del grupo de disponibilidad y, después, agregar la réplica de nuevo al grupo de disponibilidad. No puede quitar la réplica principal, de modo que si cambia el nombre de una FCI que hospeda la réplica principal, debe conmutar por error a una réplica secundaria, después quitar la réplica principal anterior y volver a agregarla. Observe que cambiar el nombre de una FCI puede modificar la dirección URL del extremo de creación de reflejo de la base de datos. Al agregar la réplica asegúrese de especificar la dirección URL del extremo actual.  
  
###  <a name="PrerequisitesFCI"></a> Lista de comprobación: requisitos previos (FCI)  
  
||Requisito previo|Vínculo|  
|-|------------------|----------|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Antes de usar una FCI para hospedar una réplica de disponibilidad, asegúrese de que el administrador del sistema haya instalado la revisión de Windows Server 2008 descrita en el artículo 976097 de Knowledge Base. Esta revisión habilita el complemento Microsoft Management Console (MMC) de administración de clúster de conmutación por error para admitir los discos asimétricos de almacenamiento compartido que están disponibles en solo algunos de los nodos de WSFC.|KB 976097:  [Revisión para agregar compatibilidad con los almacenamientos asimétricos al complemento MMC de administración de clústeres de conmutación por error para un clúster de conmutación por error que ejecute Windows Server 2008 o Windows Server 2008 R2](http://support.microsoft.com/kb/976097)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Asegúrese de que cada instancia de clúster de conmutación por error (FCI) de SQL Server posee el almacenamiento compartido necesario según la instalación estándar de la instancia de clúster de conmutación por error de SQL Server.||  
  
###  <a name="RelatedTasksFCIs"></a> Tareas relacionadas (FCI)  
  
|Tarea|Tema|  
|----------|-----------|  
|Instalar un clúster de conmutación por error de SQL Server|[Crear un nuevo clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|Actualización en contexto del clúster de conmutación por error existente de SQL Server|[Actualizar una instancia de clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)|  
|Mantener el clúster de conmutación por error existente de SQL Server|[Agregar o quitar nodos en un clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
  
###  <a name="RelatedContentFCIs"></a> Contenido relacionado (FCI)  
  
-   [Agrupación en clústeres de conmutación por error y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)  
  
-   [Guía de arquitectura de AlwaysOn: Generar una alta disponibilidad y la solución de recuperación ante desastres mediante instancias de clúster de conmutación por error y grupos de disponibilidad](http://technet.microsoft.com/library/jj215886.aspx)  
  
##  <a name="PrerequisitesForAGs"></a> Requisitos previos y restricciones de los grupos de disponibilidad  

  
###  <a name="RestrictionsAG"></a> Restricciones (grupos de disponibilidad)  
  
-   **Las réplicas de disponibilidad se deben hospedar en nodos diferentes de un clúster de WSFC**  : Para un grupo de disponibilidad determinado, las réplicas de disponibilidad deben hospedarse en instancias de servidor que se ejecutan en nodos diferentes del mismo clúster de WSFC. La única excepción es que mientras se migra a otro clúster de WSFC, un grupo de disponibilidad puede ocupar temporalmente dos clústeres.  
  
    > [!NOTE]  
    >  Cada una de las diferentes máquinas virtuales de un mismo equipo físico puede hospedar una réplica de disponibilidad para el mismo grupo de disponibilidad, porque cada máquina virtual actúa como un equipo independiente.  
  
-   **Nombre único de grupo de disponibilidad:**  cada nombre de grupo de disponibilidad debe ser único en el clúster de WSFC. La longitud máxima del nombre de un grupo de disponibilidad es 128 caracteres.  
  
-   **Réplicas de disponibilidad**  : Cada grupo de disponibilidad admite una réplica principal y hasta ocho réplicas secundarias. Todas las réplicas pueden ejecutarse en el modo de confirmación asincrónica o hasta tres de ellas pueden ejecutarse en el modo de confirmación sincrónica (una réplica principal con dos réplicas secundarias sincrónicas).  
  
-   **Número máximo de grupos de disponibilidad y bases de datos de disponibilidad por equipo:** el número real de bases de datos y grupos de disponibilidad que puede colocar en un equipo (virtual o físico) depende del hardware y de la carga de trabajo, pero no existe ningún límite forzoso. Microsoft ha probado exhaustivamente con 10 grupos de disponibilidad y 100 bases de datos por equipo físico. Los signos de sistemas sobrecargados pueden incluir, pero no limitarse a los siguientes: agotamiento de subprocesos de trabajo, tiempos de respuesta lentos para vistas del sistema y DMV de AlwaysOn o volcados del sistema del distribuidor detenidos. Asegúrese de comprobar minuciosamente el entorno con una carga de trabajo similar a la que usará en producción para asegurarse de que puede controlar la capacidad de carga de trabajo máxima con sus contratos de nivel de servicio de aplicación. Cuando evalúe los contratos de nivel de servicio, no olvide tener en cuenta la carga en condiciones de error además de los tiempos de respuesta esperados.  
  
-   **No use el Administrador de clústeres de conmutación por error para manipular grupos de disponibilidad:**  
  
     Por ejemplo:  
  
    -   No cambie ninguna propiedad del grupo de disponibilidad, como los posibles propietarios.  
  
    -   No use el Administrador de clústeres de conmutación por error para conmutar grupos de disponibilidad. Debe usar [!INCLUDE[tsql](../../../includes/tsql-md.md)] o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
###  <a name="RequirementsAG"></a> Requisitos previos (grupos de disponibilidad)  
 Al crear o establecer de nuevo una configuración de grupo de disponibilidad, asegúrese de que se adhiere a los siguientes requisitos.  
  
||Requisito previo|Descripción|  
|-|------------------|-----------------|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Si va a usar una instancia de clúster de conmutación por error (FCI) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para hospedar una réplica de disponibilidad, asegúrese de que comprende las restricciones de FCI y de que se cumplen los requisitos de FCI.|[Requisitos previos y restricciones del uso de una instancia de clúster de conmutación por error (FCI) de SQL Server para hospedar una réplica de disponibilidad](#FciArLimitations) (más adelante en este tema)|  
  
###  <a name="SecurityAG"></a> Seguridad (grupos de disponibilidad)  
  
-   La seguridad se hereda del clúster de conmutación por error de Windows Server (WSFC). WSFC proporciona dos niveles de seguridad del usuario con una granularidad de todas las API del clúster de WSFC:  
  
    -   Acceso de solo lectura  
  
    -   Control total  
  
         [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] necesita el control total, y habilitar [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona control total del clúster de WSFC (a través del SID de servicio).  
  
         No puede agregar o quitar directamente la seguridad de una instancia del servidor en el Administrador de clústeres de conmutación por error de WSFC. Para administrar las sesiones de seguridad de WSFC, use el administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o el equivalente de WMI de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debe tener permisos de acceso al Registro, al clúster, y así sucesivamente.  
  
-   Se recomienda utilizar cifrado para las conexiones entre las instancias del servidor que hospedan las réplicas de disponibilidad de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .  
  
#### <a name="permissions-availability-groups"></a>Permisos (grupos de disponibilidad)  
  
|Tarea|Permisos necesarios|  
|----------|--------------------------|  
|Crear un grupo de disponibilidad|Se requiere la pertenencia al rol fijo de servidor **sysadmin** y el permiso de servidor CREATE AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.|  
|Modificar un grupo de disponibilidad|Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.<br /><br /> Además, combinar una base de datos con un grupo de disponibilidad requiere ser miembro del rol fijo de base de datos **db_owner** .|  
|Quitar o eliminar un grupo de disponibilidad|Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER. Para quitar un grupo de disponibilidad que no se encuentre hospedado en la ubicación de réplica local, se necesita el permiso CONTROL SERVER o el permiso CONTROL en ese grupo de disponibilidad.|  
  
###  <a name="RelatedTasksAGs"></a> Tareas relacionadas (grupos de disponibilidad)  
  
|Tarea|Tema|  
|----------|-----------|  
|Crear un grupo de disponibilidad|[Usar el grupo de disponibilidad (Asistente para nuevo grupo de disponibilidad)](use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [Crear un grupo de disponibilidad (Transact-SQL)](create-an-availability-group-transact-sql.md)<br /><br /> [Crear un grupo de disponibilidad (SQL Server PowerShell)](../../../powershell/sql-server-powershell.md)<br /><br /> [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)|  
|Modificar el número de réplicas de disponibilidad|[Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [Combinar una réplica secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [Quitar una réplica secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
|Crear un agente de escucha del grupo de disponibilidad|[Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)|  
|Quitar un grupo de disponibilidad|[Quitar un grupo de disponibilidad &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)|  
  
##  <a name="PrerequisitesForDbs"></a> Requisitos previos y restricciones de las bases de datos de disponibilidad  
 Para poder agregar una base de datos a un grupo de disponibilidad, la base de datos debe cumplir los requisitos previos y restricciones siguientes.  
  
 
  
###  <a name="RequirementsDb"></a> Lista de comprobación: requisitos (bases de datos de disponibilidad)  
 Para poder agregarse a un grupo de disponibilidad, una base de datos debe:  
  
||Requisitos|Vínculo|  
|-|------------------|----------|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Ser una base de datos de usuario. Las bases de datos del sistema no pueden pertenecer a un grupo de disponibilidad.||  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Residir en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] donde esté creando el grupo de disponibilidad y ser accesible a la instancia del servidor.||  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Ser una base de datos de lectura y escritura. Las bases de datos de solo lectura no se pueden agregar a un grupo de disponibilidad.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**is_read_only** = 0)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Ser una base de datos multiusuario.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**user_access** = 0)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|No utilizar AUTO_CLOSE.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**is_auto_close_on** = 0)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Utilice el modelo de recuperación completa (también conocido como modo de recuperación completa).|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**recovery_model** = 1)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Posea al menos una copia de seguridad completa de la base de datos.<br /><br /> Nota: Después de establecer una base de datos en modo de recuperación completa, se requiere una copia de seguridad completa para iniciar la cadena de registros de recuperación completa.|[Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|No pertenecer a ningún grupo de disponibilidad existente|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**group_database_id** = NULL)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|No estar configurada para la creación de reflejo de la base de datos.|[sys.database_mirroring](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql) (si la base de datos no participa en la creación de reflejo, todas las columnas con el prefijo “mirroring_” son NULL).|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Para poder agregar una base de datos que usa FILESTREAM a un grupo de disponibilidad, asegúrese de que FILESTREAM está habilitado en cada instancia del servidor que hospeda o que hospedará una réplica de disponibilidad para el grupo de disponibilidad.|[Habilitar y configurar FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Antes de agregar una base de datos independiente a un grupo de disponibilidad, asegúrese de que el `contained database authentication` servidor opción está establecida en `1` en cada servidor que hospeda la instancia o que hospedará una réplica de disponibilidad del grupo de disponibilidad.|[contained database authentication (opción de configuración del servidor)](../../configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [Opciones de configuración de servidor &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)|  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] funciona con cualquier nivel de compatibilidad con bases de datos.  
  
###  <a name="RestrictionsDb"></a> Restricciones (bases de datos de disponibilidad)  
  
-   Si la ruta de acceso de archivo (incluida la letra de unidad) de una base de datos secundaria es diferente de la ruta de acceso de la base de datos principal correspondiente, se aplican las restricciones siguientes:  
  
    -   **[!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]/[!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]:**  La opción **Completa** no es compatible (en el tema[Página Seleccionar sincronización de datos iniciales](select-initial-data-synchronization-page-always-on-availability-group-wizards.md) ).  
  
    -   **RESTORE WITH MOVE:**  para crear las bases de datos secundarias, se debe aplicar RESTORE WITH MOVE a los archivos de base de datos en cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda una réplica secundaria.  
  
    -   **Impacto en las operaciones de agregar archivos:**  una operación posterior de agregar archivos a la réplica principal podría producir un error en las bases de datos secundarias. Este error puede causar la suspensión de las bases de datos secundarias. Esto, a su vez, hace que las réplicas secundarias entren en el estado NOT SYNCHRONIZING.  
  
        > [!NOTE]  
        >  Para más información sobre cómo responder a una operación de adición de archivos errónea, vea [Solucionar problemas relativos a una operación de agregar archivos con error &#40;grupos de disponibilidad AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md).  
  
-   No se puede quitar una base de datos que pertenezca actualmente a un grupo de disponibilidad.  
  
###  <a name="TDEdbs"></a> Seguimiento de las bases de datos protegidas por TDE  
 Si usa cifrado de datos transparente (TDE), la clave de certificado o asimétrica para crear y descifrar otras claves debe ser la misma en todas las instancias de servidor que hospedan una réplica de disponibilidad para el grupo de disponibilidad. Para obtener más información, vea [Mover una base de datos protegida por TDE a otra instancia de SQL Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md).  
  
###  <a name="PermissionsDbs"></a> Permisos (bases de datos de disponibilidad)  
 Requiere el permiso ALTER en la base de datos.  
  
###  <a name="RelatedTasksADb"></a> Tareas relacionadas (bases de datos de disponibilidad)  
  
|Tarea|Tema|  
|----------|-----------|  
|Preparar una base de datos secundaria (manualmente)|[Preparar manualmente una base de datos secundaria para un grupo de disponibilidad &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)|  
|Combinar una base de datos secundaria con un grupo de disponibilidad (manualmente)|[Combinar una base de datos secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)|  
|Modificar el número de bases de datos de disponibilidad|[Agregar una base de datos a un grupo de disponibilidad &#40;SQL Server&#41;](availability-group-add-a-database.md)<br /><br /> [Quitar una base de datos secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)<br /><br /> [Quitar una base de datos principal de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)|  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Guía de soluciones de Microsoft SQL Server AlwaysOn para alta disponibilidad y recuperación ante desastres](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Blog del equipo de AlwaysOn SQL Server: Oficial AlwaysOn Team Blog de SQL Server](http://blogs.msdn.com/b/sqlalwayson/)  
  
-   [AlwaysON - HADRON Learning Series: Bases de datos de uso del grupo de trabajo de HADRON habilitadas](http://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Agrupación en clústeres de conmutación por error y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Conectividad de cliente de AlwaysOn (SQL Server)](always-on-client-connectivity-sql-server.md)  
  
  
