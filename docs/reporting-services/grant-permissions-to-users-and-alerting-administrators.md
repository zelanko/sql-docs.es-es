---
title: Conceder permisos a los usuarios y alertar a los administradores | Microsoft Docs
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 166808e1-ada7-48d2-bda8-8f7c017fb3aa
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e3c871fc80ebc172213fe843ea7cdf18002054ce
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52505598"
---
# <a name="grant-permissions-to-users-and-alerting-administrators"></a>Conceder permisos a los usuarios y alertar a los administradores

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

Para que los usuarios y administradores de alertas puedan crear, modificar, eliminar y ver las alertas de datos, se les deben conceder permisos de SharePoint. No hay que usar permisos especiales con la característica de alertas de datos de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (se usan los permisos integrados de SharePoint).

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.

**Trabajadores de la información**: se les deben conceder los permisos de SharePoint Crear alertas y Ver elementos. Los niveles de permisos integrados de SharePoint denominados Diseño, Colaborar, Leer y Solo ver incluyen los permisos de SharePoint Crear alertas y Ver elementos. También se puede crear un nivel de permiso personalizado con los permisos necesarios para permitir que los usuarios creen, modifiquen, ejecuten y vean las alertas de datos.

**Administradores de alertas**: se debe incluir el permiso de SharePoint Administrar alerta. De forma predeterminada, solo en nivel de permiso Control total incluye este permiso para los sitios creados con la plantilla de sitio Sitio de equipo. Si utiliza otras plantillas de sitio, verá lista diferentes de grupos de SharePoint predeterminados. Puede agregar el permiso Administrar alertas a uno de los niveles de permisos integrados o crear un nivel de permiso personalizado con el permiso requerido para permitir que los administradores de alertas vean y eliminen las alertas de datos.

Para más información sobre los permisos de SharePoint, vea [Permisos de usuario y niveles de permisos (SharePoint Server 2010)](https://technet.microsoft.com/library/cc721640.aspx).

## <a name="grant-permissions"></a>Conceder permisos
  
1.  Vaya al sitio de SharePoint para el que desea conceder permisos.  
  
2.  En la barra de herramientas, haga clic **Acciones del sitio** y en **Permisos de sitio**.  
  
     Si no aparece esta opción, no tiene permisos suficientes para conceder permisos a otros.  
  
3.  Haga clic en **Conceder permisos**.  
  
4.  En **Usuarios/Grupos**, escriba los nombres de usuario, los nombres de grupo o las direcciones de correo electrónico a los que quiere conceder permiso.  
  
5.  Seleccione la opción **Agregar usuarios a un grupo de SharePoint** o **Conceder permisos a los usuarios directamente** . Dependiendo de si seleccionó **Agregar usuarios a un grupo de SharePoint** o **Conceder permisos a los usuarios directamente** , siga uno de estos procedimientos:  
  
    -   Si ha seleccionado **Agregar usuarios a un grupo de SharePoint**, seleccione un nivel de permisos en la lista desplegable.  
  
    -   Si ha seleccionado **Conceder permisos a los usuarios directamente**, seleccione un nivel de permiso.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  

## <a name="see-also"></a>Ver también

[Establecer permisos para elementos del servidor de informes en un sitio de SharePoint &#40;Reporting Services en el modo integrado de SharePoint&#41;](../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
[Alertas de datos de Reporting Services](../reporting-services/reporting-services-data-alerts.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
