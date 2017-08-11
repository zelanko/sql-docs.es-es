---
title: "Seguridad y protección de Reporting Services | Documentos de Microsoft"
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [Reporting Services]
- Reporting Services, security
ms.assetid: 270075c5-bf12-4467-a775-abbda3d954a5
caps.latest.revision: 21
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 217bd93631e96dae0b75532d73c14ade4355be6d
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="reporting-services-security-and-protection"></a>Seguridad y protección de Reporting Services
  Puede utilizar información de esta sección para obtener información acerca de las características de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. También se explican en ella los modelos de autorización y los proveedores de autenticación que se admiten en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="extended-protection-for-authentication"></a>Protección ampliada para la autenticación  
 A partir de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], se admite la protección ampliada para autenticación. La característica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el uso del enlace de canal y del enlace de servicio para mejorar la protección de la autenticación. Las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen que usarse con un sistema operativo que admita la protección ampliada. Para más información, consulte [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md).  
  
## <a name="authentication-and-authorization"></a>Autenticación y autorización  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]proporciona diferentes tipos de autenticación para los usuarios y aplicaciones de cliente para autenticar con el servidor de informes. La utilización del tipo de autenticación adecuado para el servidor de informes permite a su organización lograr el nivel de seguridad necesario. Para más información, consulte [Authentication with the Report Server](../../reporting-services/security/authentication-with-the-report-server.md).  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]también emplea roles y permisos para controlar el acceso de los usuarios a contenido en el catálogo del servidor de informes (en otras palabras, que puede tener acceso a qué y cómo éste puede tener acceso a él). Para más información, vea [Roles y permisos &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md).  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
|Descripciones de las tareas|Vínculos|  
|-----------------------|-----------|  
|Configurar SSL (Capa de sockets seguros) para proteger las conexiones de cliente al servidor de informes.|[Configurar conexiones SSL en un servidor de informes de modo nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)|  
  
  

