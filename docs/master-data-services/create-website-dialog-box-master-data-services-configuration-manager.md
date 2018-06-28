---
title: Cuadro de diálogo Crear sitio web (Administrador de configuración de Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.createsite.f1
ms.assetid: 179c9c1e-3b06-421b-b71b-1cb64d104f5e
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 6a18d54250582490506bfe5222f8b4fab17563c5
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35410037"
---
# <a name="create-website-dialog-box-master-data-services-configuration-manager"></a>Cuadro de diálogo Crear sitio web (Administrador de configuración de Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Utilice el cuadro de diálogo **Crear sitio web** para crear un sitio web nuevo en el equipo local. Cuando crea un sitio web en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], el sitio se agrega a Internet Information Services (IIS) en el equipo local con una aplicación raíz que se configura como la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . También se crea un nuevo grupo de aplicaciones y la aplicación web se coloca en ese grupo de aplicaciones.  
  
## <a name="web-site"></a>Sitio web  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|**Nombre del sitio Web**|Especifique un nombre para el sitio web o utilice el nombre predeterminado. Este nombre es descriptivo y se utiliza solamente para identificar al sitio en IIS. No se utiliza para tener acceso al sitio desde un explorador web.<br /><br /> El nombre debe ser único con respecto a todos los sitios en IIS del equipo local.|  
|**Protocolo**|Muestra **http**. Seleccione el protocolo de transferencia de hipertexto (HTTP) cuando no sea precisa la comunicación a través de un canal cifrado entre cliente y servidor.<br /><br /> **Nota**: No puede crear un sitio HTTPS en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. HTTPS es el protocolo HTTP mediante capa de sockets seguros (SSL), el cual resulta útil cuando se intercambia información confidencial o personal o cuando quiera que los usuarios confirmen la identidad del servidor antes de transmitir datos personales. Si necesita transferir información entre el servidor y un cliente a través de un canal cifrado, debe utilizar una herramienta de IIS, como Administrador de IIS, para configurar el sitio con un enlace HTTPS y asociar el enlace de sitio web a un certificado de servidor. Debe hacerlo para poder abrir correctamente el sitio web en un explorador web. Para obtener más información sobre los certificados de servidor, vea [Configurar certificados de servidor en IIS 7](http://go.microsoft.com/fwlink/?LinkId=163220) en [!INCLUDE[msCoName](../includes/msconame-md.md)] TechNet.|  
|**Dirección IP**|Seleccione una dirección IP que puedan utilizar los usuarios para tener acceso al sitio. De forma predeterminada, se selecciona **Todas sin asignar** . A menos que tenga razones para utilizar una dirección IPv4 o IPv6, utilice el valor predeterminado.<br /><br /> Con **Todas sin asignar**, este sitio responde a las solicitudes para todas las direcciones IP en el puerto y nombre de host opcional que especifique. Si hay otro sitio en el servidor que tenga un enlace en el mismo puerto pero con una dirección IP concreta, ese sitio recibe las solicitudes HTTP a ese puerto y dirección IP específicos y el sitio con la dirección IP en **Todas sin asignar** recibe el resto de solicitudes HTTP en ese puerto y en las otras direcciones IP.|  
|**Puerto**|Escriba el puerto para las solicitudes realizadas para este sitio web. Si selecciona el protocolo HTTP, el puerto predeterminado es 80. Si especifica un puerto distinto a los puertos predeterminados, los clientes deberán especificar el número de puerto para conectarse al sitio web.<br /><br /> **Nota**: El **sitio web predeterminado** en IIS está configurado para usar el protocolo HTTP en el puerto 80 con todas las direcciones IP sin asignar. Si intenta crear el sitio web en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] con la información de enlace predeterminado, recibirá un error que indica que existe un enlace duplicado. Debe cambiar la información de enlace para el sitio en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]o cambiar la información de enlace para el sitio web predeterminado con una herramienta IIS, como el Administrador IIS. Como alternativa, puede especificar un encabezado de host para que IIS pueda identificar el sitio web de forma inequívoca. Asegúrese de que configura su firewall para que acepte el tráfico a través del puerto que especifica.|  
|**Encabezado del host**|Valor opcional. Escriba un nombre de encabezado del host. Utilice esto cuando quiera asignar un nombre de host, también denominado nombre de dominio, a un equipo que utiliza una dirección IP o puerto únicos. Cuando especifique un nombre de host, los clientes deben utilizar ese nombre en lugar de la dirección IP para obtener acceso al sitio web. Al configurar un nombre de host, no puede abrir el sitio en un explorador web hasta que su servidor DNS tenga una entrada para ese nombre de host.<br /><br /> Por ejemplo, si quiere que los usuarios tengan acceso a su sitio en `http://www.contoso.com/`, debe especificar www.contoso.com como nombre de host y el servidor DNS debe tener una entrada para él.<br /><br /> Si su sitio web está disponible en una intranet, no tiene que especificar un nombre de host si los usuarios especifican el nombre del servidor en un explorador; por ejemplo, `http://server_name`. Sin embargo, si el servidor DNS en su entorno se configura para almacenar otros nombres para este servidor web, puede crear un enlace independiente para cada nombre de host, de forma que los usuarios puedan utilizar los otros nombres que haya almacenado el servidor DNS. Si debe configurar más de un nombre de host para el sitio, utilice una herramienta IIS, como el Administrador de IIS al objeto de agregar enlaces adicionales al sitio.|  
  
## <a name="application-pool"></a>Grupo de aplicaciones  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|**Nombre**|Especifique un único nombre descriptivo para el nuevo grupo de aplicaciones o utilice el nombre predeterminado que se proporciona. La aplicación web raíz para este sitio web se ejecuta en este grupo de aplicaciones.<br /><br /> Los grupos de aplicaciones proporcionan límites que evitan que las aplicaciones en un grupo de aplicaciones afecten a las aplicaciones en otro grupo de aplicaciones.|  
|**User name**|Especifique un dominio y nombre de usuario en Active Directory. Esta cuenta es la identidad del grupo de aplicaciones donde se ejecuta la aplicación web.<br /><br /> Esta cuenta se agrega al rol de base de datos mds_exec de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para el acceso a la base de datos. Para obtener más información, vea [Inicios de sesión, usuarios y roles en bases de datos &#40;Master Data Services&#41;](../master-data-services/database-logins-users-and-roles-master-data-services.md). También se agrega a un grupo de Windows de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], **MDS_ServiceAccounts**, al que se le concede permiso al directorio de compilación temporal, **MDSTempDir**, en el sistema de archivos. Para obtener más información, vea [Permisos de carpetas y archivos&#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).|  
|**Contraseña**|Escriba la contraseña de la cuenta de usuario especificada.|  
|**Confirmar contraseña**|Vuelva a escribir la contraseña de la cuenta de usuario especificada. Los campos **Contraseña** y **Confirmar contraseña** deben contener la misma contraseña.|  
  
## <a name="see-also"></a>Ver también  
 [Página Configuración web &#40;Administrador de configuración de Master Data Services&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
[Instalación y configuración de Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md) [Requisitos de la aplicación web &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [Crear una aplicación web de Master Data Manager &#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
