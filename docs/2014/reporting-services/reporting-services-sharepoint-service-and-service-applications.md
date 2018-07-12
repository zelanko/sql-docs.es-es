---
title: Reporting Services SharePoint Service and Service Applications | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 501aa9ee-8c13-458c-bf6f-24e00c82681b
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f612ac92f6741f83a92f29987cea03f662815e9d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37181502"
---
# <a name="reporting-services-sharepoint-service-and-service-applications"></a>Aplicaciones de servicio y servicio de SharePoint de Reporting Services
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Modo de SharePoint se ha diseñado como en la arquitectura de servicio de SharePoint y utiliza un servicio de SharePoint y una o varias aplicaciones de servicio. Al crear una aplicación de servicio, el servicio estará disponible y se generará la base de datos de aplicación del servicio. Puede crear varias aplicaciones de servicio de Reporting Services pero una aplicación de servicio es suficiente para la mayor parte de los escenarios de implementación.  
  
 Este tema contiene la información siguiente:  
  
-   [Crear una aplicación de servicio de Reporting Services](#bkmk_createapp)  
  
-   [Modificar las asociaciones de la aplicación de servicio con un grupo de servidores proxy](#bkmk_associations)  
  
-   [Modificar las propiedades de la aplicación de servicio](#bkmk_editserviceapplication)  
  
-   [Para crear una aplicación de servicio de Reporting Services mediante PowerShell](#bkmk_powershell_create_ssrs_serviceapp)  
  
-   [Tareas relacionadas](#bkmk_related)  
  
##  <a name="bkmk_createapp"></a> Crear una aplicación de servicio de Reporting Services  
 Puede usar los scripts de PowerShell o la Administración central de SharePoint para crear las aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Para más información sobre cómo usar la Administración central de SharePoint, vea la sección "Crear una aplicación de servicio de Reporting Services" en [Instalar el modo de SharePoint de Reporting Services para SharePoint 2010](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md). Consulte la sección de PowerShell más adelante en este tema para ver un ejemplo de un script de PowerShell para crear aplicaciones de servicio.  
  
##  <a name="bkmk_associations"></a> Modificar las asociaciones de la aplicación de servicio con un grupo de servidores proxy  
 La nueva página para crear aplicaciones de servicio contiene la sección **Asociación de aplicaciones web**. La sección le permite asociar la aplicación de servicio cuando la cree. Siga los pasos siguientes para cambiar la asociación y asignar una configuración de cliente a la aplicación de servicio. El mismo proceso general se puede usar también para agregar el proxy al grupo predeterminado en lugar de cambiar la asociación de la aplicación de servicio a un grupo personalizado.  
  
1.  En Administración central de SharePoint, en Administración de aplicaciones, haga clic en **Configurar las asociaciones de aplicación de servicio**.  
  
2.  En la página Asociaciones de aplicaciones de servicio, cambie la vista a **Aplicaciones de servicio**.  
  
3.  Busque y haga clic en el nombre de la nueva [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] aplicación de servicio. Puede hacer clic en el **valor predeterminado** del nombre del grupo de proxy de aplicación para agregar el proxy al grupo predeterminado en lugar de completar los pasos siguientes.  
  
4.  Seleccione **Personalizado** en el cuadro de selección **Editar el siguiente grupo de conexiones**.  
  
5.  Active la casilla correspondiente al proxy y haga clic en **Aceptar**.  
  
##  <a name="bkmk_editserviceapplication"></a> Modificar las propiedades de la aplicación de servicio  
 Puede volver a abrir la página de propiedades de la aplicación de servicio para modificar las propiedades.  
  
1.  En Administración central de SharePoint, en el grupo Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Seleccione la aplicación de servicio haciendo clic en la columna de tipo para seleccionar toda la fila. Si hace clic en el nombre de la aplicación, se abre la página de opciones de administración del servicio en lugar de las propiedades de la aplicación de servicio.  
  
3.  En la cinta de opciones de Aplicaciones de servicio, haga clic en **Propiedades**.  
  
##  <a name="bkmk_powershell_create_ssrs_serviceapp"></a> Para crear una aplicación de servicio de Reporting Services mediante PowerShell  
 Puede utilizar PowerShell para crear el proxy y la aplicación de servicio. En el ejemplo siguiente se supone que ya sabe qué grupo de aplicaciones desea configurar para usar la aplicación de servicio.  
  
1.  Agregue el objeto de grupo de aplicaciones del nombre del grupo de aplicaciones a una variable que se pasa en la acción Nueva.  
  
    ```  
    $appPoolName = get-spserviceapplicationpool “<application pool name>”  
    ```  
  
2.  Crear la aplicación de servicio con un nombre y un nombre de grupo de aplicaciones que proporcione.  
  
    ```  
    New-SPRSServiceApplication –Name ‘MyServiceApplication’ –ApplicationPool $appPoolName –DatabaseName ‘MyServiceApplicationDatabase’ –DatabaseServer ‘<Server Name>’  
    ```  
  
3.  Obtenga el nuevo objeto de aplicación de servicio y canalice el objeto en cmdlet para canalizar el nuevo proxy.  
  
    ```  
    Get-SPRSServiceApplication –name MyServiceApplication | New-SPRSServiceApplicationProxy “MyServiceApplicationProxy”  
    ```  
  
##  <a name="bkmk_related"></a> Tareas relacionadas  
  
|Tarea|Vínculo|  
|----------|----------|  
|Administre la configuración de la aplicación de servicio.|[Administración de una aplicación de servicio de SharePoint para Reporting Services](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)|  
|Realizar una copia de seguridad y restauración de la aplicación de servicio y de los componentes relacionados como las claves de cifrado y el proxy.|[Copias de seguridad y restauración de aplicaciones de servicio de SharePoint para Reporting Services](../../2014/reporting-services/backup-and-restore-reporting-services-sharepoint-service-applications.md)|  
  
  
