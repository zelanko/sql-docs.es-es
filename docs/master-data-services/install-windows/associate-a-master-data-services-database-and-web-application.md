---
title: Asociar una base de datos y una aplicación Web
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ccb25672-f71d-4135-b548-f50eb45d8fa5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 257928505c1aa95a61151f47c234469158761e89
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728146"
---
# <a name="associate-a-master-data-services-database-and-web-application"></a>Asociar una base de datos y una aplicación web de Master Data Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Asocie una aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] a una base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para especificar la base de datos que se utilizará en las operaciones web.  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] en el equipo local. Para obtener más información, vea [Instalar Master Data Services](../../master-data-services/install-windows/install-master-data-services.md).  
  
-   Debe existir una aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] local. Para obtener más información, vea [Crear una aplicación web de Master Data Manager &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md).  
  
-   Debe existir una base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] local o remota. Para obtener más información, vea [Crea una base de datos de Master Data Services](../../master-data-services/install-windows/create-a-master-data-services-database.md).  
  
### <a name="to-associate-a-master-data-services-database-and-web-application"></a>Para asociar una base de datos y una aplicación web de Master Data Services  
  
1.  Abra [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
2.  En el panel izquierdo, haga clic en **Configuración web**.  
  
3.  En la página **Configuración web** , debajo de **Aplicación web**, en la lista **Sitio web** , seleccione el sitio web que contiene su aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
4.  En el cuadro **Aplicación web** , seleccione la aplicación web que hospeda [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].  
  
5.  Debajo de **Asociar una aplicación con una base de datos**, haga clic en **Seleccionar**. Se abre el cuadro de diálogo **Conectar con base de datos** .  
  
6.  Especifique la información de conexión para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la base de datos [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] y haga clic en **Conectar**.  
  
7.  En la lista **Base de datos de Master Data Services** , seleccione la base de datos que desee asociar a la aplicación web y, a continuación, haga clic en **Aceptar**.  
  
8.  En **Asociar una aplicación con una base de datos**, compruebe que la información de las bases de datos y las instancias son correctas y, a continuación, haga clic en **Aplicar**.  
  
## <a name="next-steps"></a>Next Steps  
  
-   El acceso mediante programación a los servicio web de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] se habilita automáticamente cuando se crea la aplicación web. Para que los desarrolladores tengan acceso a los metadatos del servicio para generar fácilmente clases de proxy para el acceso mediante programación, se debe habilitar la publicación de metadatos. Para más información, consulte [Create Master Data Manager Web Service Proxy Classes](../../master-data-services/develop/create-master-data-manager-web-service-proxy-classes.md).  
  
-   Agregue usuarios y grupos a [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. Si no se ha concedido el acceso a [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]a ningún usuario ni grupo, debe abrir [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] utilizando las credenciales de administrador del sistema de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] . Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../../master-data-services/administrators-master-data-services.md) y [Usuarios y grupos &#40;Master Data Services&#41;](../../master-data-services/users-and-groups-master-data-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Instalar Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)   
 [Página Configuración web &#40;Administrador de configuración de Master Data Services&#41;](../../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
  
