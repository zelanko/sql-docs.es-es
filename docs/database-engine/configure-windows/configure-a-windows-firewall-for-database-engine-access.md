---
title: Configurar Firewall de Windows para el acceso al motor de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], firewall systems
- firewall systems, [Database Engine]
- security [SQL Server], firewalls
ms.assetid: 0093b43c-c6b5-4574-9b30-3a0e91e1a1f9
caps.latest.revision: 57
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 32e7e4a33a31eaa5ad66bc33e369980425cd73e3
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40405351"
---
# <a name="configure-a-windows-firewall-for-database-engine-access"></a>Configurar Firewall de Windows para el acceso al motor de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > Para obtener contenido relacionado con las versiones anteriores de SQL Server, vea [Configurar Firewall de Windows para el acceso al motor de base de datos](configure-a-windows-firewall-for-database-engine-access.md).


  En este tema se describe cómo configurar un firewall de Windows para el acceso al motor de base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el Administrador de configuración de SQL Server. Los sistemas de firewall ayudan a evitar el acceso no autorizado a los recursos de los equipos. Para obtener acceso a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] a través de un firewall, debe configurar el firewall en el equipo en el que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que permita el acceso.  
  
 Para obtener más información sobre la configuración predeterminada de Firewall de Windows y una descripción de los puertos TCP que afectan a [!INCLUDE[ssDE](../../includes/ssde-md.md)], Analysis Services, Reporting Services e Integration Services, vea [Configurar Firewall de Windows para permitir el acceso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md). Existen varios sistemas de firewall. Para obtener información específica, vea la documentación del firewall.  
  
 Los pasos principales para permitir el acceso son:  
  
1.  Configure el [!INCLUDE[ssDE](../../includes/ssde-md.md)] para que use un puerto TCP/IP específico. La instancia predeterminada de [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa el puerto 1433, pero se puede cambiar. El puerto que usa [!INCLUDE[ssDE](../../includes/ssde-md.md)] aparece en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Las instancias de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], [!INCLUDE[ssEW](../../includes/ssew-md.md)] y las instancias con nombre de [!INCLUDE[ssDE](../../includes/ssde-md.md)] usan puertos dinámicos. Para configurar estas instancias de modo que usen un puerto específico, vea [Configurar un servidor para que escuche en un puerto TCP específico &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
2.  Configure el firewall para que permita el acceso a ese puerto a los usuarios o equipos autorizados.  
  
> [!NOTE]  
>  El servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite a los usuarios conectarse a instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que no están escuchando en el puerto 1433, sin conocer el número de puerto. Para utilizar el Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe abrir el puerto UDP 1434. Para promover el entorno más seguro, deje detenido el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y configure los clientes para que se conecten usando el número de puerto.  
  
> [!NOTE]  
>  De forma predeterminada, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows habilita el Firewall de Windows, que cierra el puerto 1433 para impedir que los equipos de Internet se conecten a una instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en su equipo. No se puede realizar conexiones con TCP/IP a la instancia predeterminada, a menos que se vuelva a abrir el puerto 1433. Los pasos básicos para configurar el Firewall de Windows se proporcionan en los procedimientos siguientes. Para obtener más información, consulte la documentación de Windows.  
  
 Como alternativa a la configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para escuchar en un puerto fijo y abrir el puerto, puede poner el ejecutable de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Sqlservr.exe) en la lista de excepciones a los programas bloqueados. Use este método cuando desee seguir utilizando puertos dinámicos. De este modo, solo se puede tener acceso a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para configurar un firewall de Windows para el acceso al motor de base de datos, utilizando:**  
  
     [Administrador de configuración de SQL Server](#SSMSProcedure)  
  
## <a name="before-you-begin"></a>Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
 El hecho de abrir puertos en el firewall puede dejar el servidor expuesto a ataques malintencionados. Asegúrese de que conoce los sistemas de firewall antes de abrir puertos. Para obtener más información, consulte [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
 Se aplica a Windows Vista, Windows 7 y Windows Server 2008  
  
 El siguiente procedimiento configura el Firewall de Windows mediante el complemento Microsoft Management Console (MMC) de Firewall de Windows con seguridad avanzada. El Firewall de Windows con seguridad avanzada solo configura el perfil actual. Para obtener más información sobre Firewall de Windows con seguridad avanzada, vea [Configurar Firewall de Windows para permitir el acceso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
#### <a name="to-open-a-port-in-the-windows-firewall-for-tcp-access"></a>Para abrir un puerto en el Firewall de Windows para el acceso TCP  
  
1.  En el menú **Inicio** , haga clic en **Ejecutar**, escriba **WF.msc**y, a continuación, haga clic en **Aceptar**.  
  
2.  En la opción **Firewall de Windows con seguridad avanzada**del panel izquierdo, haga clic con el botón derecho en **Reglas de entrada**y, luego, haga clic en **Nueva regla** en el panel de acciones.  
  
3.  En el cuadro de diálogo **Tipo de regla** , seleccione **Puerto**y, a continuación, haga clic en **Siguiente**.  
  
4.  En el cuadro de diálogo **Protocolo y puertos** , seleccione **TCP**. Seleccione **Puertos locales específicos**y escriba el número de puerto de la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)], por ejemplo, **1433** para la instancia predeterminada. Haga clic en **Siguiente**.  
  
5.  En el cuadro de diálogo **Acción** , seleccione **Permitir la conexión**y, a continuación, haga clic en **Siguiente**.  
  
6.  En el cuadro de diálogo **Perfil** , seleccione los perfiles que describan el entorno de conexión del equipo cuando desee conectarse a [!INCLUDE[ssDE](../../includes/ssde-md.md)]y, a continuación, haga clic en **Siguiente**.  
  
7.  En el cuadro de diálogo **Nombre** , escriba un nombre y una descripción para esta regla. Después, haga clic en **Finalizar**.  
  
#### <a name="to-open-access-to-sql-server-when-using-dynamic-ports"></a>Para abrir el acceso a SQL Server cuando se usen puertos dinámicos  
  
1.  En el menú **Inicio** , haga clic en **Ejecutar**, escriba **WF.msc**y, a continuación, haga clic en **Aceptar**.  
  
2.  En la opción **Firewall de Windows con seguridad avanzada**del panel izquierdo, haga clic con el botón derecho en **Reglas de entrada**y, luego, haga clic en **Nueva regla** en el panel de acciones.  
  
3.  En el cuadro de diálogo **Tipo de regla** , seleccione **Programa**y, a continuación, haga clic en **Siguiente**.  
  
4.  En el cuadro de diálogo **Programa** , seleccione **Esta ruta de acceso del programa**. Haga clic en **Examinar**y navegue a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que desee obtener acceso a través del firewall y, a continuación, haga clic en **Abrir**. De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se encuentra en **C:\Archivos de programa\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Sqlservr.exe**. Haga clic en **Siguiente**.  
  
5.  En el cuadro de diálogo **Acción** , seleccione **Permitir la conexión**y, a continuación, haga clic en **Siguiente**.  
  
6.  En el cuadro de diálogo **Perfil** , seleccione los perfiles que describan el entorno de conexión del equipo cuando desee conectarse a [!INCLUDE[ssDE](../../includes/ssde-md.md)]y, a continuación, haga clic en **Siguiente**.  
  
7.  En el cuadro de diálogo **Nombre** , escriba un nombre y una descripción para esta regla. Después, haga clic en **Finalizar**.  
  
## <a name="see-also"></a>Ver también  
 [Configurar los valores de firewall (Base de datos SQL de Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)  
  
  
