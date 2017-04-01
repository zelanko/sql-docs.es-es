---
title: "Elecci&#243;n de un m&#233;todo de actualizaci&#243;n del motor de base de datos | Microsoft Docs"
ms.custom: ""
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5e57a427-2e88-4ef6-b142-4ccad97bcecc
caps.latest.revision: 23
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 23
---
# Elecci&#243;n de un m&#233;todo de actualizaci&#243;n del motor de base de datos
  Existen varios enfoques que se deben considerar a la hora de planear la actualización del [!INCLUDE[ssDE](../../includes/ssde-md.md)] de una versión previa de SQL Server a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con el objetivo de minimizar el tiempo de inactividad y los riesgos. Puede realizar una actualización local, migrar a una nueva instalación o efectuar una actualización gradual. El siguiente diagrama le ayudará a elegir uno de estos enfoques. Además, más adelante en este artículo se describen todos los enfoques presentes en el diagrama. Si quiere obtener ayuda para tomar las decisiones que se le presentan en el diagrama, consulte también [Plan and Test the Database Engine Upgrade Plan](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
 ![Database Engine Upgrade Method Decision Tree](../../database-engine/install-windows/media/database-engine-upgrade-method-decision-tree.png "Database Engine Upgrade Method Decision Tree")  
  
 **Descargar**  
  
-   Para descargar [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], vaya al  **[Centro de evaluación](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**.  
  
-   ¿Tiene una cuenta de Azure?  Si es así, vaya **[aquí](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016ctp2evaluationwindowsserver2012r2/?wt.mc_id=sqL16_vm)** para poner en marcha una máquina virtual con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ya instalado.  
  
> [!NOTE]  
>  También puede plantearse actualizar la base de datos SQL de Azure o virtualizar su entorno de SQL Server como parte de su plan de actualización. Estos temas se quedan fuera del ámbito de este artículo, pero puede ampliar la información al respecto en estos vínculos: [Introducción a la nube híbrida de SQL Server 2016](../Topic/Introduction%20to%20SQL%20Server%202016%20Hybrid%20Cloud.md), [Introducción a SQL Server en máquinas virtuales de Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/), [Base de datos SQL](https://azure.microsoft.com/en-us/services/sql-database/) y [Selección de una opción de SQL Server en Azure](https://azure.microsoft.com/documentation/articles/data-management-azure-sql-database-and-sql-server-iaas/).  
  
##  <a name="UpgradeInPlace"></a> Actualización local  
 Con este enfoque, el programa de instalación de SQL Server actualiza la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente reemplazando la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente por una de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y, después, actualiza cada una de las bases de datos de usuario y del sistema.  El enfoque de actualización local es el más sencillo, conlleva la menor cantidad de tiempo de inactividad, tarda más en tiempo en revertirse (si esto fuera necesario) y no se admite en todos los casos. Para obtener más información sobre los escenarios de actualización local que se admiten y los que no, vea [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
 Este enfoque se suele usar en los escenarios siguientes:  
  
-   Un entorno de desarrollo sin una configuración de alta disponibilidad.  
  
-   Un entorno de producción no esencial que pueda tolerar el tiempo de inactividad y que ejecute hardware y software recientes. La cantidad de tiempo de inactividad depende del tamaño de la base de datos y la velocidad de su subsistema de E/S. Se necesitará un poco más de tiempo a la hora de actualizar SQL Server 2014 cuando se estén usando tablas con optimización para memoria. Para obtener más información, consulte [Plan and Test the Database Engine Upgrade Plan](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
> [!WARNING]  
>  Cuando se ejecuta el programa de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se detiene y reinicia como parte de la ejecución de las comprobaciones previas a la actualización.  
  
> [!CAUTION]  
>  Cuando actualice a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la instancia anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se sobrescribirá y ya no estará en el equipo. Antes de actualizar, realice una copia de seguridad de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de otros objetos asociados con la instancia anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 En el siguiente diagrama se ofrece una descripción general de los pasos necesarios para llevar a cabo una actualización local del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 ![Database Engine Upgrade Non-HA In-Place Upgrade](../../database-engine/install-windows/media/database-engine-upgrade-non-ha-in-place-upgrade.png "Database Engine Upgrade Non-HA In-Place Upgrade")  
  
 Para obtener información detallada, vea [Actualización a SQL Server 2016 mediante el Asistente para instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/upgrade-to-sql-server-2016-using-the-installation-wizard-setup.md).  
  
##  <a name="NewInstallationUpgrade"></a> Migración a una nueva instalación  
 Con este enfoque, conserva el entorno actual a la vez que crea un entorno de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nuevo, con frecuencia en nuevo hardware y con una nueva versión del sistema operativo. Después de instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en el nuevo entorno, debe realizar una serie de pasos a fin de prepararlo para poder migrar las bases de datos de usuario existentes desde el entorno antiguo al nuevo y minimizar el tiempo de inactividad. En estos pasos se incluye la migración de los siguientes elementos:  
  
-   **Objetos de sistema:** algunas aplicaciones dependen de información, entidades u objetos que se encuentran fuera del ámbito de una sola base de datos de usuario. Normalmente, una aplicación depende de las bases de datos maestra y msdb, así como la de usuario. Cualquier elemento almacenado fuera de la base de datos de usuario que sea necesario para el funcionamiento correcto de dicha base de datos debe estar disponible en la instancia de servidor de destino. Por ejemplo, los inicios de sesión de una aplicación se almacenan como metadatos en la base de datos maestra y se deben volver a crear en el servidor de destino. Si una aplicación o un plan de mantenimiento de bases de datos dependen de trabajos del Agente SQL Server, cuyos metadatos estén almacenados en la base de datos msdb, dichos trabajos se deben volver a crear en la instancia de servidor de destino. De forma similar, los metadatos de un desencadenador de servidor se almacenan en la base de datos maestra.  
    Si mueve la base de datos de una aplicación a otra instancia de servidor, debe volver a crear todos los metadatos de las entidades y objetos dependientes de las bases de datos maestra y msdb en la instancia de servidor de destino. Por ejemplo, si una aplicación de la base de datos usa desencadenadores de servidor, no basta con adjuntar o restaurar la base de datos en el nuevo sistema. La base de datos no funcionará según lo previsto a menos que se vuelvan a crear manualmente los metadatos para dichos desencadenadores en la base de datos maestra. Para obtener información detallada, vea [Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia del servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage metadata when making a database available on another server.md).  
  
-   **Paquetes de Integration Services almacenados en MSDB:** si almacena paquetes en MSDB, debe incluirlos en un script mediante [dtutil Utility](../../integration-services/dtutil-utility.md) o volver a implementarlos en el nuevo servidor. Antes de utilizar los paquetes en el nuevo servidor, debe actualizarlos a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, consulte [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
-   **Claves de cifrado de Reporting Services:** una parte importante de la configuración del servidor de informes es la creación de una copia de seguridad de la clave simétrica usada para cifrar información confidencial. La copia de seguridad de la clave se necesita para varias operaciones rutinarias y, además, permite volver a utilizar una base de datos del servidor de informes existente en una nueva instalación. Para obtener más información, vea [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../../reporting-services/install-windows/back-up-and-restore-reporting-services-encryption-keys.md) y [Actualizar y migrar Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
 Una vez el nuevo entorno de   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] cuente con los mismos objetos de sistema que el antiguo, deberá migrar las bases de datos de usuario desde el sistema existente a la instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con un método que minimice el tiempo de inactividad en dicho sistema. Podrá realizar la migración de la base de datos por medio de una copia de seguridad y una restauración, o bien redirigiendo LUN si se encuentra en un entorno de SAN. Los pasos de ambos métodos se escriben en los diagramas siguientes.  
  
> [!CAUTION]  
>  La cantidad de tiempo de inactividad depende del tamaño de la base de datos y la velocidad de su subsistema de E/S. Se necesitará un poco más de tiempo a la hora de actualizar SQL Server 2014 cuando se estén usando tablas con optimización para memoria. Para obtener más información, consulte [Plan and Test the Database Engine Upgrade Plan](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
 Después de migrar las bases de datos de usuario, dirija a los nuevos usuarios a la nueva instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante uno de los diversos métodos disponibles (por ejemplo, cambiar el nombre del servidor, usar una entrada DNS, modificar las cadenas de conexión, etc.).  El nuevo enfoque de instalación reduce los riesgos y el tiempo de inactividad (en comparación con una actualización local). Además, facilita que se actualice el hardware y el sistema operativo con la actualización a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Si ya dispone de una solución de alta disponibilidad o de algún otro entorno con varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vaya a [Actualización gradual](#RollingUpgrade). Si no cuenta con una solución de alta disponibilidad, puede plantearse configurar temporalmente la [creación de reflejo de la base de datos](http://msdn.microsoft.com/library/ms190941.aspx) a fin de minimizar el tiempo de inactividad y facilitar la actualización, o bien aprovechar esta oportunidad para configurar un [grupo de disponibilidad AlwaysOn](http://msdn.microsoft.com/library/hh510260.aspx) como solución de alta disponibilidad permanente.  
  
 Por ejemplo, puede utilizar este enfoque para actualizar los siguientes elementos:  
  
-   Una instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un sistema operativo no compatible.  
  
-   Una instalación x86 de SQL Server, ya que [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no admite este tipo de instalaciones.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en hardware nuevo o una nueva versión del sistema operativo.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] junto con una consolidación de servidores.  
  
-   SQL Server 2005, ya que [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no admite la actualización local de SQL Server 2005 a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, consulte [Are you upgrading from SQL Server 2005?](../../database-engine/install-windows/are-you-upgrading-from-sql-server-2005.md).  
  
 Los pasos necesarios realizar una actualización mediante una nueva instalación varían ligeramente en función de si usa almacenamiento conectado o SAN.  
  
-   **Entorno de almacenamiento conectado:** si tiene un entorno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el que se usa almacenamiento conectado, el siguiente diagrama y los vínculos incluidos le servirán de guía para seguir los pasos necesarios para realizar una actualización de [!INCLUDE[ssDE](../../includes/ssde-md.md)]mediante una nueva instalación.  
  
     ![New installation upgrade method using backup and restore for attached storage](../../database-engine/install-windows/media/new-installation-upgrade-method-using-backup-and-restore-for-attached-storage.png "New installation upgrade method using backup and restore for attached storage")  
  
-   **Entorno de almacenamiento SAN:**  si tiene un entorno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el que se usa almacenamiento SAN, el siguiente diagrama y los vínculos incluidos le servirán de guía para seguir los pasos necesarios para realizar una actualización de [!INCLUDE[ssDE](../../includes/ssde-md.md)]mediante una nueva instalación.  
  
     ![New installation upgrade method using detach and attach for SAN storage](../../database-engine/install-windows/media/new-installation-upgrade-method-using-detach-and-attach-for-san-storage.png "New installation upgrade method using detach and attach for SAN storage")  
  
##  <a name="RollingUpgrade"></a> Actualización gradual  
 Se requiere una actualización gradual en entornos de soluciones de SQL Server donde se deba actualizar varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un orden determinado para maximizar el tiempo de actividad, minimizar los riesgos y conservar determinada funcionalidad. Una actualización gradual consiste básicamente en la actualización de varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un orden determinado, ya sea mediante una actualización local en cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente o efectuando una actualización con una nueva instalación a fin de facilitar la actualización del hardware o el sistema operativo como parte del proyecto de actualización. Hay una serie de escenarios en los que deberá poner en práctica el enfoque de actualización gradual. Estos se documentan en los siguientes temas:  
  
-   Grupos de disponibilidad AlwaysOn: si quiere obtener instrucciones detalladas para realizar una actualización gradual en un entorno de este tipo, vea [Actualización de instancias de la réplica del grupo de disponibilidad AlwaysOn](../../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).  
  
-   Instancias de clústeres de conmutación por error: si quiere obtener instrucciones detalladas para realizar una actualización gradual en un entorno de este tipo, vea [Actualización de una instancia de clúster de conmutación por error de SQL Server](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md).  
  
-   Instancias reflejadas: si quiere obtener instrucciones detalladas para realizar una actualización gradual en un entorno de este tipo, vea [Actualización de instancias reflejadas](../../database-engine/database-mirroring/upgrading-mirrored-instances.md).  
  
-   Instancias de trasvase de registros: si quiere obtener instrucciones detalladas para realizar una actualización gradual en un entorno de este tipo, vea [Actualización del trasvase de registros a SQL Server 2016 &#40;Transact-SQL&#41;](../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md).  
  
-   Entorno de replicación: si quiere obtener instrucciones detalladas para realizar una actualización gradual en un entorno de este tipo, consulte [Upgrade Replicated Databases](../../database-engine/install-windows/upgrade-replicated-databases.md).  
  
-   Entorno de escalado horizontal de SQL Server Reporting Services: si quiere obtener instrucciones detalladas para realizar una actualización gradual en un entorno de este tipo, vea [Actualizar y migrar Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
## ¿Le ayudó este artículo? Le escuchamos  
 ¿Qué información está buscando? ¿La encontró? Escuchamos sus comentarios para mejorar el contenido. Envíe sus comentarios a [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Choose%20a%20Database%20Engine%20Upgrade%20Method%20page).  
  
## Vea también  
 [Planeación y prueba del plan de actualización del motor de base de datos](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)   
 [Completar la actualización motor de base de datos](../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
  