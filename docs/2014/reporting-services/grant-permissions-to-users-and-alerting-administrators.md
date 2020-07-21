---
title: Conceder permisos a los usuarios y alertar a los administradores | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 166808e1-ada7-48d2-bda8-8f7c017fb3aa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 48311ccaa22878fb5b17be75c3f12c64cb4a67e6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109059"
---
# <a name="grant-permissions-to-users-and-alerting-administrators"></a>Conceder permisos a los usuarios y alertar a los administradores
  Para que los usuarios y administradores de alertas puedan crear, modificar, eliminar y ver las alertas de datos, se les deben conceder permisos de SharePoint. No hay que usar permisos especiales con la característica de alertas de datos de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (se usan los permisos integrados de SharePoint).  
  
 **Trabajadores de la información**: se les deben conceder los permisos de SharePoint Crear alertas y Ver elementos. Los niveles de permisos integrados de SharePoint denominados Diseño, Colaborar, Leer y Solo ver incluyen los permisos de SharePoint Crear alertas y Ver elementos. También se puede crear un nivel de permiso personalizado con los permisos necesarios para permitir que los usuarios creen, modifiquen, ejecuten y vean las alertas de datos.  
  
 **Administradores de alertas**: los permisos deben incluir el permiso administrar alertas de SharePoint. De forma predeterminada, solo en nivel de permiso Control total incluye este permiso para los sitios creados con la plantilla de sitio Sitio de equipo. Si utiliza otras plantillas de sitio, verá lista diferentes de grupos de SharePoint predeterminados. Puede agregar el permiso Administrar alertas a uno de los niveles de permisos integrados o crear un nivel de permiso personalizado con el permiso requerido para permitir que los administradores de alertas vean y eliminen las alertas de datos.  
  
 Para más información sobre los permisos de SharePoint, vea [Permisos de usuario y niveles de permisos (SharePoint Server 2010)](https://technet.microsoft.com/library/cc721640.aspx).  
  
### <a name="to-grant-permissions"></a>Para conceder permisos  
  
1.  Vaya al sitio de SharePoint para el que desea conceder permisos.  
  
2.  En la barra de herramientas, haga clic **Acciones del sitio** y en **Permisos de sitio**.  
  
     Si no aparece esta opción, no tiene permisos suficientes para conceder permisos a otros.  
  
3.  Haga clic en **Concesión de permisos**.  
  
4.  En **Usuarios/Grupos**, escriba los nombres de usuario, los nombres de grupo o las direcciones de correo electrónico a los que quiere conceder permiso.  
  
5.  Seleccione la opción **Agregar usuarios a un grupo de SharePoint** o **Conceder permisos a los usuarios directamente** . Dependiendo de si seleccionó **Agregar usuarios a un grupo de SharePoint** o **Conceder permisos a los usuarios directamente** , siga uno de estos procedimientos:  
  
    -   Si ha seleccionado **Agregar usuarios a un grupo de SharePoint**, seleccione un nivel de permisos en la lista desplegable.  
  
    -   Si ha seleccionado **Conceder permisos a los usuarios directamente**, seleccione un nivel de permiso.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Establecer permisos para elementos del servidor de informes en un sitio de SharePoint &#40;Reporting Services en el modo integrado de SharePoint&#41;](security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Alertas de datos de Reporting Services](../ssms/agent/alerts.md)  
  
  
