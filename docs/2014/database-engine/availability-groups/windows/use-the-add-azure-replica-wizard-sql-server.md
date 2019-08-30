---
title: Usar el Asistente para agregar réplica de Azure (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.addreplicawizard.azurereplica.f1
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85f5dc758a6f9243fc553f597687552fdb22a481
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154406"
---
# <a name="use-the-add-azure-replica-wizard-sql-server"></a>Usar el Asistente para agregar réplica de Azure (SQL Server)
  Use el Asistente para agregar una réplica de Azure para ayudarle a crear una nueva máquina virtual de Azure en ti híbrida y configurarla como una réplica secundaria para un grupo de disponibilidad AlwaysOn nuevo o existente.  
  
-   **Antes de empezar:**  
  
     [Requisitos previos](#Prerequisites)  
  
     [Seguridad](#Security)  
  
-   **Para agregar una réplica, mediante:**  [Asistente para agregar réplica de Azure (SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
 Si nunca ha agregado ninguna réplica de disponibilidad a un grupo de disponibilidad, vea las secciones "instancias del servidor" y "grupos y réplicas de disponibilidad" en [requisitos previos, restricciones y recomendaciones &#40;para grupos de disponibilidad AlwaysOn SQL Servidor&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Debe estar conectado a la instancia del servidor que hospeda la réplica principal actual.  
  
-   Debe tener un entorno de ti híbrido en el que la subred local tenga una VPN de sitio a sitio con Azure. Para obtener más información, vea [Configurar una VPN de sitio a sitio en el Portal de administración](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create).  
  
-   Es preciso que el grupo de disponibilidad cuente con réplicas locales disponibles.  
  
-   Los clientes del agente de escucha del grupo de disponibilidad deben tener conectividad a Internet si desean mantener la conectividad con el agente de escucha cuando el grupo de disponibilidad se conmuta por error a una réplica de Azure.  
  
-   **Requisitos previos para usar la sincronización de datos inicial completa** Deberá especificar un recurso compartido de red para que el asistente cree copias de seguridad y pueda tener acceso a estas. Para la réplica principal, la cuenta usada para iniciar el [!INCLUDE[ssDE](../../../includes/ssde-md.md)] debe tener permisos del sistema de archivos de lectura y escritura en un recurso compartido de red. Para las réplicas secundarias, la cuenta debe tener permiso de lectura en el recurso compartido de red.  
  
     Si no puede utilizar el asistente para realizar la sincronización de datos inicial completa, debe preparar las bases de datos secundarias manualmente. Puede hacerlo antes o después de ejecutar el asistente. Para obtener más información, vea [Preparar manualmente una base de datos secundaria para un grupo de disponibilidad &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Consulte [Security](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md#Security)  
  
##  <a name="SSMSProcedure"></a> Usar el Asistente para agregar réplica de Azure (SQL Server Management Studio)  
 El Asistente para agregar réplica de Azure se puede iniciar desde [Especificar la página de réplicas](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md). Hay dos formas de llegar a esta opción:  
  
-   [Usar el Asistente para grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar el Asistente para agregar una réplica al grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 Una vez que haya iniciado el Asistente para agregar réplica de Azure, siga los pasos a continuación:  
  
1.  En primer lugar, descargue un certificado de administración para su suscripción de Azure. Haga clic en **Descargar** para abrir la página de inicio de sesión.  
  
2.  En la página de inicio de sesión, inicie sesión en su suscripción de Azure. Una vez que haya iniciado sesión, el asistente instala un certificado de administración en el equipo local. Este certificado de administración se cargará automáticamente cuando vuelva a usar este asistente. Si ha descargado varios certificados de administración, puede hacer clic en el botón **...** para seleccionar el que desea usar.  
  
3.  A continuación, haga clic en **Conectar**para conectarse a su suscripción. Una vez que esté conectado, las listas desplegables se rellenan con los parámetros de Azure, como **Virtual Network** y **Virtual Network subred**.  
  
4.  Especifique la configuración de la máquina virtual de Azure que hospedará la nueva réplica secundaria:  
  
     Image  
     El nombre de la imagen de SQL Server que se va a usar para la máquina virtual de Azure  
  
     Tamaño de VM  
     El tamaño de la máquina virtual de Azure  
  
     Nombre de VM  
     El nombre DNS de la máquina virtual de Azure  
  
     Nombre de usuario de VM  
     El nombre de usuario del administrador predeterminado para la máquina virtual de Azure  
  
     Contraseña del administrador de la máquina virtual (y confirmar contraseña)  
     La contraseña del administrador predeterminado para la máquina virtual de Azure.  
  
     Virtual Network  
     La red virtual en la que se va a colocar la máquina virtual de Azure  
  
     Subred de la red virtual  
     La subred de la red virtual en la que se va a colocar la máquina virtual de Azure  
  
     Dominio  
     El dominio Active Directory (AD) para unirse a la máquina virtual de Azure  
  
     Nombre de usuario del dominio  
     El nombre de usuario de AD que se usa para unir la máquina virtual de Azure al dominio.  
  
     Contraseña  
     La contraseña que se usa para unir la máquina virtual de Azure al dominio.  
  
5.  Haga clic en **Aceptar** para confirmar los valores de configuración y salir del Asistente para agregar réplica de Azure.  
  
6.  Continúe con el resto de los pasos de configuración para [Especificar la página de réplicas](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) , tal como hace para las réplicas nuevas.  
  
     Cuando haya terminado con el Asistente para grupo de disponibilidad o el Asistente para agregar una réplica al grupo de disponibilidad, el proceso de configuración realizará todas las operaciones en Azure para crear la nueva máquina virtual, unirla al dominio de AD, agregarla al clúster de Windows, habilitar AlwaysOn alto Disponibilidad y agregue la nueva réplica al grupo de disponibilidad.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Información general de &#40;grupos de disponibilidad AlwaysOn SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Requisitos previos, restricciones y recomendaciones para Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
