---
title: Requisitos de aplicaciones web (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9455d3cf-c1b7-4d48-8aff-7dc636ed5dc3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 15b394c836cb24229944f4e0775dfccad847a32b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65482882"
---
# <a name="web-application-requirements-master-data-services"></a>Requisitos de la aplicación web (Master Data Services)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] es una aplicación web hospedada por Internet Information Services (IIS). [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] funciona únicamente en Internet Explorer (IE) 7 o posterior. No se admiten IE 7 ni versiones anteriores, así como tampoco Microsoft Edge ni Chrome.  
  
 Use [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para crear y configurar la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] configura IIS en el equipo local, de modo que es lo mejor para las tareas iniciales de configuración web. Por ejemplo, configure un entorno de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] con una aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] única, o bien configure la primera aplicación web en una implementación escalada de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Utilice las herramientas de IIS para realizar tareas más complejas, como configurar varios servidores web en una implementación escalada.  
  
> [!NOTE]  
>  Cualquier equipo en el que instale los componentes de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] debe tener las licencias pertinentes. Para obtener más información, consulte el Contrato de licencia para el usuario final (CLUF).  
  
## <a name="requirements"></a>Requisitos  
  
### <a name="operating-system"></a>Sistema operativo  
 Los siguientes sistemas operativos Windows incluyen la funcionalidad de Internet Information Services (IIS) necesaria para la aplicación web y el servicio web [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .  
  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Developer (64 bits) x64|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (64 bits) x64|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Business Intelligence (64 bits) x64|  
|-------------------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------|  
|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows 7 Professional, Enterprise y Ultimate<br /><br /> Windows 8.0 Professional, Enterprise y Ultimate|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows Server 2012|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows Server 2012|  
  
 Para obtener una lista completa de los sistemas operativos Windows compatibles con su edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea requisitos de [hardware y software para la instalación de SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
### <a name="microsoft-silverlight"></a>Microsoft Silverlight  
 Para trabajar en la aplicación web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , Silverlight 5 debe estar instalado en el equipo cliente. Si no tiene la versión necesaria de Silverlight, se le pedirá que la instale cuando navegue a un área de la aplicación web que la necesite. Puede instalar Silverlight 5 [aquí](https://go.microsoft.com/fwlink/?LinkId=243096).  
  
### <a name="role-and-role-services-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a>Rol y servicios del rol (sistemas operativos Windows Server 2008 o Windows Server 2008 R2, Windows 7)  
 En Windows Server 2008 R2, puede usar el **Administrador del servidor**, que está disponible en Microsoft Management Console (MMC), para instalar el rol **Servidor web (IIS)** y los siguientes servicios de rol necesarios.  
  
> [!NOTE]  
>  En [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] y en los sistemas operativos Windows 7, use **Programas y características** en el Panel de control para habilitar estas opciones en el cuadro de diálogo **Características de Windows** .  
  
||  
|-|  
|Servidor Web<br /><br /> Características HTTP comunes<br /><br /> Contenido estático<br /><br /> Documento predeterminado<br /><br /> Examen de directorios<br /><br /> Errores HTTP<br /><br /> Desarrollo de aplicaciones<br /><br /> ASP.NET<br /><br /> Extensibilidad de .NET<br /><br /> Extensiones ISAPI<br /><br /> Filtros de ISAPI<br /><br /> Estado y diagnóstico<br /><br /> Registrar HTTP<br /><br /> Monitor de solicitudes<br /><br /> Seguridad<br /><br /> Autenticación de Windows<br /><br /> Filtro de solicitudes<br /><br /> Rendimiento<br /><br /> Compresión de contenido estático<br /><br /> Herramientas de administración<br /><br /> Consola de administración de IIS|  
  
### <a name="role-and-role-services-windows-server-2012-or-windows-8-operating-systems"></a>Rol y servicios de rol (sistemas operativos Windows Server 2012 o Windows 8)  
 En Windows Server 2012, puede usar el **Administrador del servidor**, que está disponible en Microsoft Management Console (MMC), para instalar el rol **Servidor web (IIS)** y los siguientes servicios de rol necesarios.  
  
> [!NOTE]  
>  En el sistema operativo Windows 8, use **Programas y características** en el Panel de control para habilitar estas opciones en el cuadro de diálogo **Características de Windows** .  
  
||  
|-|  
|Internet Information Services<br /><br /> Herramientas de administración web<br /><br /> Consola de administración de IIS<br /><br /> Servicios de World Wide Web<br /><br /> Desarrollo de aplicaciones<br /><br /> Extensibilidad de .NET<br /><br /> Extensibilidad de .NET 4.5<br /><br /> ASP.NET 3.5<br /><br /> ASP.NET 4.5<br /><br /> Extensiones ISAPI<br /><br /> Filtros de ISAPI<br /><br /> Características HTTP comunes<br /><br /> Documento predeterminado<br /><br /> Examen de directorios<br /><br /> Errores HTTP<br /><br /> Contenido estático<br /><br /> [Nota: no instale Publicación en WebDAV]<br /><br /> Estado y diagnóstico<br /><br /> Registrar HTTP<br /><br /> Monitor de solicitudes<br /><br /> Rendimiento<br /><br /> Compresión de contenido estático<br /><br /> Seguridad<br /><br /> Filtro de solicitudes<br /><br /> Autenticación de Windows|  
  
### <a name="features-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a>Características (sistemas operativos Windows Server 2008 o Windows Server 2008 R2, Windows 7)  
 En [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] o en Windows Server 2008 R2, puede usar **Administrador del servidor** para instalar las siguientes características necesarias.  
  
> [!NOTE]  
>  En [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] y en los sistemas operativos Windows 7, use **Programas y características** en el Panel de control para habilitar estas opciones en el cuadro de diálogo **Características de Windows** .  
  
||  
|-|  
|Características de .NET Framework 3.0<br /><br /> Activación WCF<br /><br /> Activación HTTP<br /><br /> Activación no HTTP<br /><br /> Servicio de activación de procesos de Windows<br /><br /> Modelo de proceso<br /><br /> Entorno .NET<br /><br /> API de configuración|  
  
### <a name="features-windows-server-2012-or-windows-8-operating-systems"></a>Características (sistemas operativos Windows Server 2012 o Windows 8)  
 En Windows Server 2012, puede usar **Administrador del servidor** para instalar las siguientes características necesarias.  
  
> [!NOTE]  
>  En el sistema operativo Windows 8, use **Programas y características** en el Panel de control para habilitar estas opciones en el cuadro de diálogo **Características de Windows** .  
  
||  
|-|  
|.NET Framework 3.5 (incluye .NET 2.0 y 3.0)<br /><br /> Servicios avanzados de .NET Framework 4.5<br /><br /> ASP.NET 4.5<br /><br /> WCF Services<br /><br /> Activación HTTP [Nota: esto es necesario]<br /><br /> Uso compartido de puertos TCP<br /><br /> Servicio de activación de procesos de Windows<br /><br /> Modelo de proceso<br /><br /> Entorno .NET<br /><br /> API de configuración|  
  
### <a name="accounts-and-permissions"></a>Cuentas y permisos  
  
|Tipo|Descripción|  
|----------|-----------------|  
|Cuenta de Windows|Debe iniciar sesión en el equipo servidor web con una cuenta de Windows que tenga permiso para configurar roles de Windows, servicios de rol y características, y para crear y administrar grupos de aplicaciones, sitios web y aplicaciones web en IIS, en el equipo local.|  
|Cuenta de servicio|Cuando cree la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] en [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)], debe especificar una identidad para el grupo de aplicaciones en el que se ejecute la aplicación. Esta cuenta puede ser diferente de la cuenta de servicio que se especificó cuando se creó la base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .<br /><br /> Esta identidad debe ser una cuenta de usuario de dominio y se agrega al rol de la base de datos mds_exec en la base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para tener acceso a las bases de datos. Para obtener más información, vea [Inicios de sesión, usuarios y roles en bases de datos &#40;Master Data Services&#41;](../database-logins-users-and-roles-master-data-services.md). Esta cuenta también se agrega a un grupo de Windows [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , **MDS_ServiceAccounts**, que es el permiso concedido al directorio de compilación temporal, **MDSTempDir**, en el sistema de archivos. Para obtener más información, vea [Permisos de carpetas y archivos&#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md).<br /><br /> La cuenta de grupo de aplicaciones necesita el permiso VIEW SERVER STATE para evitar errores de servidor. Por ejemplo, el comando Validar versión MDS produce un error de servidor. Para obtener más información, consulte [Comando Validar versión MDS produce un error de servidor en SQL Server 2012 y SQL Server 2014](https://go.microsoft.com/fwlink/p/?LinkId=526304)|  
  
## <a name="see-also"></a>Consulte también  
 [Instalar Master Data Services](install-master-data-services.md)   
 [Cree una aplicación Web de Master Data Manager &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md)   
 [Página Configuración web &#40;Administrador de configuración de Master Data Services&#41;](../web-configuration-page-master-data-services-configuration-manager.md)  
  
  
