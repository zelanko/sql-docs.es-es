---
title: Seguridad y protección de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- security [Reporting Services]
- Reporting Services, security
ms.assetid: 270075c5-bf12-4467-a775-abbda3d954a5
caps.latest.revision: 20
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 9a993f574cbf272e4fdf47066360bd09299cd7d1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200471"
---
# <a name="reporting-services-security-and-protection"></a>Seguridad y protección de Reporting Services
  Puede usar la información de esta sección para obtener información acerca de las características de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. También se explican en ella los modelos de autorización y los proveedores de autenticación que se admiten en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="extended-protection-for-authentication"></a>Protección ampliada para la autenticación  
 A partir de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], se admite la protección ampliada para autenticación. La característica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el uso del enlace de canal y del enlace de servicio para mejorar la protección de la autenticación. Las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen que usarse con un sistema operativo que admita la protección ampliada. Para obtener más información, consulte [protección ampliada para la autenticación con Reporting Services](extended-protection-for-authentication-with-reporting-services.md).  
  
## <a name="authentication-and-authorization"></a>Autenticación y autorización  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona diferentes tipos de autenticación para que los usuarios y las aplicaciones cliente se autentiquen en el servidor de informes. La utilización del tipo de autenticación adecuado para el servidor de informes permite a su organización lograr el nivel de seguridad necesario. Para más información, consulte [Authentication with the Report Server](authentication-with-the-report-server.md).  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] también emplea roles y permisos para controlar el acceso de usuario al contenido del catálogo del servidor de informes (es decir, quién tiene acceso a qué y cómo puede obtener acceso). Para obtener más información, vea [Roles y permisos &#40;Reporting Services&#41;](roles-and-permissions-reporting-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripciones de las tareas|Vínculos|  
|-----------------------|-----------|  
|Configurar SSL (Capa de sockets seguros) para proteger las conexiones de cliente al servidor de informes.|[Configuración de conexiones SSL en un servidor de informes en modo nativo](configure-ssl-connections-on-a-native-mode-report-server.md)|  
  
  