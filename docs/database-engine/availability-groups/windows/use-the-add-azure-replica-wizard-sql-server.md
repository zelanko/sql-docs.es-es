---
title: "Usar el Asistente para agregar r&#233;plica de Azure (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.addreplicawizard.azurereplica.f1"
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
caps.latest.revision: 12
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 12
---
# Usar el Asistente para agregar r&#233;plica de Azure (SQL Server)
  Use el Asistente Agregar réplica de Microsoft Azure para que le ayude a crear una nueva máquina virtual de Windows Azure en tecnologías informáticas híbridas y configurarla como una réplica secundaria para un grupo de disponibilidad AlwaysON nuevo o existente.  
  
-   **Antes de empezar:**  
  
     [Requisitos previos](#Prerequisites)  
  
     [Seguridad](#Security)  
  
-   **Para agregar una réplica con:** [ Asistente Agregar réplica de Microsoft Azure (SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
 Si nunca ha agregado una réplica de disponibilidad a un grupo de disponibilidad, vea las secciones "Instancias del servidor" y "Grupos y réplicas de disponibilidad" en [Requisitos previos, restricciones y recomendaciones para Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs, restrictions, recommendations - always on availability.md).  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Debe estar conectado a la instancia del servidor que hospeda la réplica principal actual.  
  
-   Debe tener un entorno de tecnologías informáticas híbrido donde la subred local tenga una VPN de sitio a sitio con Windows Azure. Para obtener más información, vea [Configurar una VPN de sitio a sitio en el Portal de administración](https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-site-to-site-create).  
  
-   Es preciso que el grupo de disponibilidad cuente con réplicas locales disponibles.  
  
-   Los clientes del agente de escucha del grupo de disponibilidad deben disponer de conectividad a Internet si van a mantener la conectividad con el agente de escucha cuando el grupo de disponibilidad haya provocado una conmutación por error en una réplica de Windows Azure.  
  
-   **Requisitos previos para usar la sincronización de datos inicial completa** Deberá especificar un recurso compartido de red para que el asistente cree copias de seguridad y pueda tener acceso a estas. Para la réplica principal, la cuenta usada para iniciar el [!INCLUDE[ssDE](../../../includes/ssde-md.md)] debe tener permisos del sistema de archivos de lectura y escritura en un recurso compartido de red. Para las réplicas secundarias, la cuenta debe tener permiso de lectura en el recurso compartido de red.  
  
     Si no puede utilizar el asistente para realizar la sincronización de datos inicial completa, debe preparar las bases de datos secundarias manualmente. Puede hacerlo antes o después de ejecutar el asistente. Para obtener más información, vea [Preparar manualmente una base de datos secundaria para un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Consulte [Security](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md#Security)  
  
##  <a name="SSMSProcedure"></a> Usar el Asistente para agregar réplica de Azure (SQL Server Management Studio)  
 El Asistente para agregar réplica de Azure se puede iniciar desde [Especificar la página de réplicas](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md). Hay dos formas de llegar a esta opción:  
  
-   [Usar el Asistente para grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar el Asistente para agregar una réplica al grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 Una vez que haya iniciado el Asistente para agregar réplica de Azure, siga los pasos a continuación:  
  
1.  En primer lugar, descargue un certificado de administración para la suscripción de Windows Azure. Haga clic en **Descargar** para abrir la página de inicio de sesión.  
  
2.  Inicie sesión en Microsoft Azure con la cuenta de Microsoft o la cuenta corporativa. La cuenta corporativa o de Microsoft presenta el formato de una dirección de correo electrónico, como HYPERLINK "mailto:patc@contoso.com" patc@contoso.com. Para obtener más información sobre las credenciales de Azure, vea [Microsoft Account for Organizations FAQ](http://technet.microsoft.com/jj592903) (Preguntas frecuentes sobre Cuenta para organizaciones de Microsoft) y [Troubleshooting sign-in problems with your organizational account](https://support.microsoft.com/kb/2756852) (Solución de problemas de inicio de sesión con la cuenta corporativa).  
  
3.  A continuación, haga clic en **Conectar**para conectarse a su suscripción. Cuando lo haya hecho, las listas desplegables se rellenan con los parámetros de Windows Azure, como **Red virtual** y **Subred de la red virtual**.  
  
4.  Especifique los valores de configuración para la máquina virtual de Windows Azure que hospedará la nueva réplica secundaria:  
  
     Imagen  
     Nombre de la imagen de SQL Server que se va a usar para la máquina virtual de Windows Azure.  
  
     Tamaño de VM  
     Tamaño de la máquina virtual de Windows Azure  
  
     Nombre de VM  
     Nombre DNS de la máquina virtual de Windows Azure  
  
     Nombre de usuario de VM  
     Nombre de usuario del administrador predeterminado para la máquina virtual de Windows Azure  
  
     Contraseña del administrador de la máquina virtual (y confirmar contraseña)  
     Contraseña del administrador predeterminado para la máquina virtual de Windows Azure  
  
     Red virtual  
     Red virtual en la que estará la máquina virtual de Windows Azure  
  
     Subred de la red virtual  
     Subred de red virtual en la que estará la máquina virtual de Windows Azure  
  
     Dominio  
     Dominio de Active Directory (AD) para combinar la máquina virtual de Windows Azure  
  
     Nombre de usuario del dominio  
     Nombre de usuario de AD que se usa para combinar la máquina virtual de Windows Azure con el dominio  
  
     Contraseña  
     Contraseña que se usa para combinar la máquina virtual de Windows Azure con el dominio  
  
5.  Haga clic en **Aceptar** para confirmar los valores de configuración y salir del Asistente para agregar réplica de Azure.  
  
6.  Continúe con el resto de los pasos de configuración para [Especificar la página de réplicas](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) , tal como hace para las réplicas nuevas.  
  
     Una vez haya terminado con el Asistente para nuevo grupo de disponibilidad o el Asistente para agregar una réplica al grupo de disponibilidad, el proceso de configuración realizará todas las operaciones de Windows Azure para crear una máquina virtual nueva, combinarla con el dominio de AD, agregarla al clúster de Windows, habilitar alta disponibilidad de AlwaysOn y agregar una nueva réplica al grupo de disponibilidad.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## Vea también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Requisitos previos, restricciones y recomendaciones para Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs, restrictions, recommendations - always on availability.md)   
 [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  