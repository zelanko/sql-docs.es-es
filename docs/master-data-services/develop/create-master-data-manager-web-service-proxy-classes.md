---
title: Crear clases de proxy del servicio web Master Data Manager | Microsoft Docs
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
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: ba3b315cc62ce64da9212ef3d00b60ec1a303e33
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>Crear clases de proxy del servicio web Master Data Manager
  El servicio web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] le permite usar las características de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] mediante programación desde cualquier equipo que pueda acceder a su sitio web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. Antes de empezar a escribir código para acceder al servicio web, debe generar clases de proxy. La clase de proxy principal que utiliza para realizar operaciones del servicio web es la clase <xref:Microsoft.MasterDataServices.ServiceClient>, que implementa la interfaz <xref:Microsoft.MasterDataServices.IService>.  
  
## <a name="enable-web-service-metadata-publishing"></a>Habilitar la publicación de metadatos del servicio web  
 Para poder generar clases de proxy, debe habilitar la publicación de metadatos del servicio web. Para ello, siga estos pasos:  
  
1.  Abra el archivo Web.config de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] en un editor de texto. Este archivo se encuentra en la carpeta WebApplication de la ruta de instalación de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
2.  Busque la sección **mdsWsHttpBehavior** en **\<serviceBehaviors>**. Para el elemento **\<serviceMetadata>**, establezca **httpGetEnabled** en **true**.  
  
    > [!NOTE]  
    >  Si quiere habilitar los servicios web mediante la capa de sockets seguros (SSL), establezca **httpsGetEnabled** en **true** en la sección **mdsWsHttpBehavior** del archivo web.config. También debe modificar **mdsWsHTTPBinding** para que esté configurado para SSL y convertir en comentario la sección que no es de SSL.  
  
3.  Guarde los cambios realizados en el archivo.  
  
4.  Pruebe la publicación de metadatos yendo a la dirección URL del servicio (por ejemplo, `http://yourserver/MDS/service/service.svc`). Si la publicación de metadatos está habilitada, se muestra una página que empieza con   
    “Ha creado un servicio”.  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>Crear clases de proxy usando Visual Studio  
 Si tiene instalado Visual Studio 2010, la manera más sencilla de generar clases de proxy consiste en agregar una **referencia de servicio** al proyecto. La dirección de la referencia de servicio es la URL de la aplicación de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], seguida de /service/service.svc. Por ejemplo: `http://yourserver/MDS/service/service.svc`. Para más información, vea [Cómo: Agregar, actualizar o quitar una referencia de servicio](http://go.microsoft.com/fwlink/?LinkId=221167).  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>Crear clases de proxy usando Svcutil.exe  
 Debe haber instalado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o el SDK de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para tener Svcutil.exe en su equipo. Si utiliza [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], debe utilizar el símbolo del sistema de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para ejecutar el comando. Para más información, vea [Herramienta de utilidad de metadatos de ServiceModel (Svcutil.exe)](http://go.microsoft.com/fwlink/?LinkId=165027) y [Generación de un cliente WCF a partir de los metadatos de servicio](http://go.microsoft.com/fwlink/?LinkId=164821).  
  
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
  
## <a name="see-also"></a>Vea también  
 [Operaciones de servicio web clasificadas &#40;Master Data Services&#41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
  
  
