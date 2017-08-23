---
title: Crear clases de Proxy de servicio Web de Master Data Manager | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 8bdab026-a0c0-41f3-9d36-f3919c23247f
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a45cd15ced90aef95feb03f8fbaafd5aa70cb746
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>Crear clases de proxy del servicio web Master Data Manager
  El servicio web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] le permite usar las características de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] mediante programación desde cualquier equipo que pueda acceder a su sitio web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. Antes de empezar a escribir código para acceder al servicio web, debe generar clases de proxy. La clase de proxy principal que utiliza para realizar operaciones del servicio web es la clase <xref:Microsoft.MasterDataServices.ServiceClient>, que implementa la interfaz <xref:Microsoft.MasterDataServices.IService>.  
  
## <a name="enable-web-service-metadata-publishing"></a>Habilitar la publicación de metadatos del servicio web  
 Para poder generar clases de proxy, debe habilitar la publicación de metadatos del servicio web. Siga estos pasos para hacer esto:  
  
1.  Abra el [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] archivo Web.config en un editor de texto. Este archivo se encuentra en la carpeta WebApplication de la ruta de instalación de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
2.  Buscar el **mdsWsHttpBehavior** sección bajo  **\<serviceBehaviors >**. Para el  **\<serviceMetadata >** elemento, establezca **httpGetEnabled** a **true**.  
  
    > [!NOTE]  
    >  Si desea habilitar los servicios Web mediante capa de Sockets seguros (SSL), establezca **httpsGetEnabled** a **true** en el **mdsWsHttpBehavior** sección del archivo web.config. También debe cambiar **mdsWsHTTPBinding** para que se configure para SSL, también, y marque como comentario la sección sin SSL.  
  
3.  Guarde los cambios realizados en el archivo.  
  
4.  Publicación de metadatos de prueba a través de la dirección URL del servicio, por ejemplo: `http://yourserver/MDS/service/service.svc`. Si la publicación de metadatos está habilitada, se muestra una página que empieza con   
    “Ha creado un servicio”.  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>Crear clases de proxy usando Visual Studio  
 Si tiene instalado Visual Studio 2010, la manera más sencilla de generar clases de proxy es agregar un **referencia de servicio** al proyecto. La dirección de la referencia de servicio es la URL de la aplicación de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], seguida de /service/service.svc. Por ejemplo: `http://yourserver/MDS/service/service.svc`. Para obtener más información, consulte [Cómo: agregar, actualizar o quitar una referencia de servicio](http://go.microsoft.com/fwlink/?LinkId=221167).  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>Crear clases de proxy usando Svcutil.exe  
 Debe haber [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o [!INCLUDE[msCoName](../../includes/msconame-md.md)] instalado el SDK de Windows para tener Svcutil.exe en el equipo. Si utiliza [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], debe utilizar el símbolo del sistema de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para ejecutar el comando. Para obtener más información, consulte [la herramienta de utilidad de metadatos de ServiceModel (Svcutil.exe)](http://go.microsoft.com/fwlink/?LinkId=165027) y [generar un cliente de WCF de metadatos de servicio](http://go.microsoft.com/fwlink/?LinkId=164821).  
  
 Para crear un conjunto de clases de proxy en C# usando Svcutil.exe, utilice un comando como el siguiente:  
  
```  
svcutil.exe http://<server_name:port>/<virtual_path>/Service/Service.svc   
/out:<proxy_name>.cs /messageContract /tcv:Version35   
/noconfig /ct:System.Collections.ObjectModel.Collection`1   
/namespace:*,Microsoft.MasterDataServices  
```  
  
 Donde:  
  
-   *ServerName*:*puerto* son el nombre de equipo y número de puerto del equipo que hospeda [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].  
  
-   *virtual_path* es la ruta de acceso virtual [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] en Internet Information Services (IIS).  
  
-   *proxy_name* es el nombre del archivo de proxy generado.  
  
## <a name="see-also"></a>Vea también  
 [Las operaciones de servicio Web clasificadas &#40; Master Data Services &#41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
  
  
