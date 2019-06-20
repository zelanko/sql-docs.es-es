---
title: Configuración del servidor - cuentas de servicio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- service account configuration, SQL Server
ms.assetid: c283702d-ab20-4bfa-9272-f0c53c31cb9f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8435b0c677f80bf4f26acd4411d90ab63c7473d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092272"
---
# <a name="server-configuration---service-accounts"></a>Configuración del servidor - Cuentas de servicio
  Use la página Configuración del servidor del Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el fin de asignar cuentas de inicio de sesión a los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los servicios reales configurados en esta página dependen de las características que haya seleccionado para instalarse.  
  
 Las cuentas de inicio utilizadas para iniciar y ejecutar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden ser cuentas de usuario de dominio HYPERLINK "ms-help://SQL11_I1033/s11sq_GetStart_I/html/309b9dac-0b3a-4617-85ef-c4519ce9d014.htm" \l "Domain_User", cuentas de usuario locales, cuentas de servicio administradas las cuentas virtuales o cuentas del sistema integradas.  
  
## <a name="options"></a>Opciones  
 Puede asignar la misma cuenta de inicio de sesión a todos los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o configurar cada cuenta de servicio individualmente. También puede especificar si los servicios se inician de forma automática o manual, o si están deshabilitados. Se recomienda la cuenta predeterminada para la mayoría de las instalaciones.  
  
 En Windows 7 y [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2, de forma predeterminada casi todas las cuentas son virtuales.  
  
 Si configura servicios para que usen cuentas de dominio, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que configure las cuentas de servicio de forma individual para proporcionar a cada servicio los privilegios mínimos; así, los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] obtendrán los permisos mínimos que necesitan para completar sus tareas. Para obtener más información incluidas las descripciones de los tipos de cuentas, vea [Configure Windows Service Accounts and Permissions](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
 **Configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] individualmente cuentas de servicio (recomendado)**  
 Utilice la cuadrícula para proporcionar a cada servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un nombre de usuario y una contraseña de inicio de sesión, y para establecer el tipo de inicio para el servicio. Puede utilizar cuentas del sistema integradas, una cuenta local, un grupo local, un grupo de dominios o cuentas de usuario de dominio para los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Seleccione cualquiera de los siguientes servicios para personalizar su configuración.  
  
|Seleccione este servicio|Para configurar los valores de autenticación de|  
|-------------------------|----------------------------------------------|  
|e[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |El servicio que ejecuta trabajos, supervisa, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y permite la automatización de tareas administrativas.<br /><br /> No hay ninguna cuenta de inicio de sesión predeterminada para este servicio.<br /><br /> El tipo de inicio predeterminado es Manual.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|El tipo de inicio predeterminado es Automático.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|El tipo de inicio predeterminado es Automático.<br /><br /> Para el modo integrado de SharePoint, debe especificar una cuenta de usuario de dominio de Windows. La cuenta especificada se utiliza para el servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . La cuenta que especifique para la instancia actual se debe usar también para las instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] adicionales que se agregan a continuación a la misma granja de servidores.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Las cuentas de servicio se usan para configurar una conexión de base de datos del servidor de informes. Elija el servicio de red integrado si desea utilizar los valores de autenticación predeterminados. Si especifica una cuenta de usuario de dominio, asegúrese de registrar un nombre principal de servicio (SPN) para ella si está usando la autenticación de Windows en el servidor de informes. Para más información, consulte [Configure Windows Authentication on the Report Server](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md).<br /><br /> El tipo de inicio predeterminado es Automático.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es un conjunto de herramientas gráficas y objetos programables para mover, copiar y transformar datos.<br /><br /> El tipo de inicio predeterminado es Automático.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client|La cuenta de servicio que se usa para el servicio Distributed Replay Client.<br /><br /> Proporcione una cuenta en la que se ejecutará el servicio Distributed Replay Client. Esta cuenta debe ser diferente de la usada para el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> El tipo de inicio predeterminado es Manual.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller|La cuenta de servicio que se usa para el servicio Distributed Replay Controller.<br /><br /> Proporcione una cuenta en la que se ejecutará el servicio Distributed Replay Controller. Esta cuenta debe ser diferente de la usada para el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> El tipo de inicio predeterminado es Manual.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Full-text Filter Daemon Launcher|El servicio que crea los procesos fdhost.exe. Este servicio es necesario para hospedar los separadores de palabras y los filtros que procesan datos de texto en la indización de texto completo.<br /><br /> Si proporciona una cuenta de dominio en la que se va a ejecutar el servicio FDHOST Launcher, es muy recomendable que utilice una cuenta con pocos privilegios. Esta cuenta debe ser diferente de la usada para el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser es el servicio de resolución de nombres que proporciona información de conexión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a los equipos cliente. Este servicio lo comparten varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . La cuenta de inicio de sesión predeterminada es el servicio NT Authority\Local y no se puede cambiar durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Puede cambiar la cuenta una vez completado el proceso de instalación. Si no se especifica el tipo de inicio durante el proceso de instalación, se determina de la siguiente forma:<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser se establece en Automatic y se ejecuta en los escenarios de instalación que se describen a continuación:<br />-<br />                            [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instancia de clúster de conmutación por error<br />-<br />                            Instancia con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde está habilitado TCP o NP<br />-<br />                            Instancia con nombre de Analysis Server que no está en clúster<br /><br /> Si no se aplica ninguno de los escenarios anteriores y el Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ya está instalado, se mantendrá el estado actual del Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> El tipo de inicio se establece en Disabled y se detiene si no existe ninguna instancia de una versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior a la instalación.|  
  
## <a name="see-also"></a>Vea también  
 [Consideraciones de seguridad para una instalación de SQL Server](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
