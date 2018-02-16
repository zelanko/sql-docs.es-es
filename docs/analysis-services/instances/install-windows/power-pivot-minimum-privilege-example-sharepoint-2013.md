---
title: "Power Pivot con privilegios mínimos ejemplo: SharePoint 2013 | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c1e09e6c-52d3-48ab-8c70-818d5d775087
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: aa7ce279e968322d9e1ffd80d9a277d27b18c9f7
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="power-pivot-minimum-privilege-example---sharepoint-2013"></a>Power Pivot con privilegios mínimos ejemplo: SharePoint 2013
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
En este tema se describe una configuración de ejemplo de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013 con privilegios mínimos. La configuración emplea una cuenta diferente para cada uno de los tres componentes y cada cuenta tiene el nivel mínimo de privilegios.  
  
## <a name="summary-of-accounts"></a>Resumen de cuentas  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013 admite el uso de la cuenta de servicio de red para la cuenta de servicio de Analysis Services. La cuenta de servicio de red no es un escenario admitido con SharePoint 2010. Para obtener más información sobre las cuentas de servicio, vea [Configurar los permisos y las cuentas de servicio de Windows](http://msdn.microsoft.com/library/ms143504.aspx) (http://msdn.microsoft.com/library/ms143504.aspx).  
  
 En la tabla siguiente se resumen las tres cuentas usadas en este ejemplo de configuración con privilegios mínimos.  
  
|Ámbito|Nombre|  
|-----------|----------|  
|Cuenta de administrador de SharePoint|**SPAdmin**|  
|Cuenta de granja de SharePoint|**SPFarm**|  
|Cuenta de servicio de Analysis Services|**SPsvc**|  
  
### <a name="the-sharepoint-administrator-account-spadmin"></a>La cuenta de administrador de SharePoint (SpAdmin)  
 **SPAdmin** es una cuenta de dominio que se emplea para instalar y configurar la granja de servidores. Es la cuenta empleada para ejecutar el Asistente para la configuración de SharePoint y la herramienta de configuración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013. La cuenta **SPAdmin** es la única que necesita derechos de administrador local. Antes de ejecutar la herramienta de configuración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , conceda a la cuenta **SPAdmin** privilegios para la instancia de base de datos de SQL Server donde SharePoint crea bases de datos de contenido y de configuración. Para configurar la cuenta SPAdmin en un escenario de privilegios mínimos, debe ser miembro de los roles **securityadmin** y **dbcreator**.  
  
### <a name="the-farm-account-spfarm"></a>La cuenta de granja (SPFarm)  
 **SPFarm** es una cuenta de dominio que el servicio Temporizador de extensiones de SharePoint y la aplicación web de Administración central usan para acceder a la base de datos de contenido de SharePoint. No es necesario que esta cuenta sea administrador local. El Asistente para la configuración de SharePoint concede el privilegio mínimo adecuado en la base de datos back-end de SQL Server. La configuración de privilegios mínimos de SQL Server es la pertenencia a los roles **securityadmin** y **dbcreator**.  
  
### <a name="the-service-account-for-power-pivot-service-spsvc"></a>La cuenta de servicio para el servicio Power Pivot (SPsvc)  
 Si no se configura una nueva granja de SharePoint antes de ejecutar el [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] herramienta de configuración, a continuación, de forma predeterminada el [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] herramienta de configuración creará lo siguiente:  
  
-   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Aplicación de servicio.  
  
-   Aplicación de servicio de Excel.  
  
-   Aplicación de almacenamiento seguro.  
  
 La herramienta de configuración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] configura las tres aplicaciones de servicio en el grupo de aplicaciones predeterminado. Ese grupo de aplicaciones se suele configurar para que se ejecute como la cuenta SPFarm, que tiene acceso a muchos recursos que una cuenta de servicio no necesita. Para hacer que el entorno sea un entorno con privilegios mínimos, configure una nueva cuenta de dominio para que la usen el grupo de aplicaciones y la aplicación web adecuados.  
  
 **Para crear una nueva cuenta de dominio SPsvc que se usará como cuenta de servicio de SharePoint:**  
  
1.  En Administración central de SharePoint, seleccione **Seguridad**.  
  
2.  Seleccione **Configurar cuentas de servicio**  
  
3.  Seleccione **Registrar una nueva cuenta administrada**.  
  
 La cuenta **SPSvc** no tiene privilegios de administrador local y SPsvc no tendrá ningún privilegio en la base de datos de SharePoint. Los únicos privilegios que SPsvc necesita son derechos administrativos en la instancia de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] de Analysis Services.  
  
 **Para configurar el grupo de aplicaciones adecuado de manera que use la cuenta SPsvc:**  
  
1.  En Administración central de SharePoint, seleccione **Seguridad**.  
  
2.  Seleccione **Configurar cuentas de servicio**.  
  
3.  Seleccione el grupo de aplicaciones de servicio usado por la aplicación de servicio de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Seleccione después la cuenta SPSvc.  
  
 **Para conceder acceso a la aplicación web con PowerShell:**  
  
1.  Ejecute el shell de administración de SharePoint 2013 con privilegios de administrador.  
  
2.  Ejecute el siguiente código de PowerShell:  
  
    ```  
    $webApp = Get-SPWebApplication "http://<servername>"  
    $webApp.GrantAccessToProcessIdentity("DOMAIN\<ServiceAccountName>")  
  
    ```  
  
  
