---
title: Crear clases de proxy del servicio web Master Data Manager | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 8bdab026-a0c0-41f3-9d36-f3919c23247f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 82a6909ff518dc49b4b3037c0a323b4ef1f60f7b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84961995"
---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>Crear clases de proxy del servicio web Master Data Manager
  El servicio web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] le permite usar las características de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] mediante programación desde cualquier equipo que pueda acceder a su sitio web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . Antes de empezar a escribir código para acceder al servicio web, debe generar clases de proxy. La clase de proxy principal que utiliza para realizar operaciones del servicio web es la clase <xref:Microsoft.MasterDataServices.ServiceClient>, que implementa la interfaz <xref:Microsoft.MasterDataServices.IService>.  
  
## <a name="enable-web-service-metadata-publishing"></a>Habilitar la publicación de metadatos del servicio web  
 Para poder generar clases de proxy, debe habilitar la publicación de metadatos del servicio web. Para ello, siga estos pasos:  
  
1.  Abra el archivo Web.config de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] en un editor de texto. Este archivo se encuentra en la carpeta WebApplication de la ruta de instalación de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
2.  Busque la `mdsWsHttpBehavior` sección en **\<serviceBehaviors>** . En el caso del **\<serviceMetadata>** elemento, establezca `httpGetEnabled` en `true` .  
  
    > [!NOTE]  
    >  Si desea habilitar los servicios web sobre la capa de (SSL) sockets seguros, establezca `httpsGetEnabled` a `true` en la sección de `mdsWsHttpBehavior` de archivo web.config. También debe cambiar `mdsWsHTTPBinding` para configurarlo para SSL y comentar la sección que no es de SSL.  
  
3.  Guarde los cambios realizados en el archivo.  
  
4.  Pruebe la publicación de metadatos yendo a la dirección URL del servicio (por ejemplo, http://yourserver/MDS/service/service.svc). Si la publicación de metadatos está habilitada, se muestra una página que empieza con   
    "Ha creado un servicio".  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>Crear clases de proxy usando Visual Studio  
 Si tiene instalado Visual Studio 2010, la manera más sencilla de generar clases de proxy consiste en agregar una **referencia de servicio** al proyecto. La dirección de la referencia de servicio es la URL de la aplicación de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], seguida de /service/service.svc. Por ejemplo: http://yourserver/MDS/service/service.svc. Para más información, vea [Cómo: Agregar, actualizar o quitar una referencia de servicio](https://go.microsoft.com/fwlink/?LinkId=221167).  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>Crear clases de proxy usando Svcutil.exe  
 Debe tener [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] instalado o el [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows SDK para poder tener Svcutil.exe en el equipo. Si utiliza [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], debe utilizar el símbolo del sistema de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para ejecutar el comando. Para más información, vea [Herramienta de utilidad de metadatos de ServiceModel (Svcutil.exe)](https://go.microsoft.com/fwlink/?LinkId=165027) y [Generación de un cliente WCF a partir de los metadatos de servicio](https://go.microsoft.com/fwlink/?LinkId=164821).  
  
 Para crear un conjunto de clases de proxy en C# usando Svcutil.exe, utilice un comando como el siguiente:  
  
```  
svcutil.exe http://<server_name:port>/<virtual_path>/Service/Service.svc   
/out:<proxy_name>.cs /messageContract /tcv:Version35   
/noconfig /ct:System.Collections.ObjectModel.Collection`1   
/namespace:*,Microsoft.MasterDataServices  
```  
  
 Donde:  
  
-   *servername*:*port* son el nombre de equipo y el número de puerto del equipo que hospeda [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].  
  
-   *virtual_path* es la ruta de acceso virtual de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] en Internet Information Services (IIS).  
  
-   *proxy_name* es el nombre del archivo de proxy generado.  
  
## <a name="see-also"></a>Consulte también  
 [Operaciones de servicio web clasificadas &#40;Master Data Services&#41;](categorized-web-service-operations-master-data-services.md)  
  
  
