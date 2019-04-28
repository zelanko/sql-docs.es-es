---
title: Ejemplo de configuración de PowerPivot para SharePoint 2013 con privilegios mínimos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: c1e09e6c-52d3-48ab-8c70-818d5d775087
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b79b9c6662b40b860cfacd85d77b09dbfb04117d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62703246"
---
# <a name="example-of-a-minimum-privilege-configuration-for-powerpivot-for-sharepoint-2013"></a>Ejemplo de configuración con privilegios mínimos de PowerPivot para SharePoint 2013
  En este tema se describe una configuración de ejemplo de PowerPivot para SharePoint 2013 con privilegios mínimos. La configuración emplea una cuenta diferente para cada uno de los tres componentes y cada cuenta tiene el nivel mínimo de privilegios.  
  
## <a name="summary-of-accounts"></a>Resumen de cuentas  
 PowerPivot para SharePoint 2013 admite el uso de la cuenta de servicio de red para la cuenta de servicio de Analysis Services. La cuenta de servicio de red no es un escenario admitido con SharePoint 2010. Para obtener más información sobre las cuentas de servicio, consulte [Configure Windows Service Accounts and Permissions](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) (https://msdn.microsoft.com/library/ms143504.aspx).  
  
 En la tabla siguiente se resumen las tres cuentas usadas en este ejemplo de configuración con privilegios mínimos.  
  
|Ámbito|Name|  
|-----------|----------|  
|Cuenta de administrador de SharePoint|**SPAdmin**|  
|Cuenta de granja de SharePoint|**SPFarm**|  
|Cuenta de servicio de Analysis Services|**SPsvc**|  
  
### <a name="the-sharepoint-administrator-account-spadmin"></a>La cuenta de administrador de SharePoint (SpAdmin)  
 **SPAdmin** es una cuenta de dominio que se emplea para instalar y configurar la granja de servidores. Es la cuenta utilizada para ejecutar el Asistente para configuración de SharePoint y la herramienta de configuración de PowerPivot para SharePoint 2013 **SPAdmin** cuenta es la única cuenta que requiere derechos de administrador local. Antes de ejecutar la herramienta de configuración de PowerPivot, conceda el **SPAdmin** privilegios para la instancia de base de datos de SQL Server donde SharePoint crea bases de datos de contenido y la configuración de la cuenta. Para configurar la cuenta SPAdmin en un escenario de privilegios mínimos, debe ser miembro de los roles **securityadmin** y **dbcreator**.  
  
### <a name="the-farm-account-spfarm"></a>La cuenta de granja (SPFarm)  
 **SPFarm** es una cuenta de dominio que el servicio Temporizador de extensiones de SharePoint y la aplicación web de Administración central usan para acceder a la base de datos de contenido de SharePoint. No es necesario que esta cuenta sea administrador local. El Asistente para la configuración de SharePoint concede el privilegio mínimo adecuado en la base de datos back-end de SQL Server. La configuración de privilegios mínimos de SQL Server es la pertenencia a los roles **securityadmin** y **dbcreator**.  
  
### <a name="the-service-account-for-powerpivot-service-spsvc"></a>La cuenta de servicio para el servicio PowerPivot (SPsvc)  
 Si no se configura una nueva granja de SharePoint antes de ejecutar la herramienta de configuración de PowerPivot, esta herramienta creará lo siguiente de forma predeterminada:  
  
-   Aplicación de servicio PowerPivot.  
  
-   Aplicación de servicio de Excel.  
  
-   Aplicación de almacenamiento seguro.  
  
 La herramienta de configuración de PowerPivot configura las tres aplicaciones de servicio en el grupo de aplicaciones predeterminado. Ese grupo de aplicaciones se suele configurar para que se ejecute como la cuenta SPFarm, que tiene acceso a muchos recursos que una cuenta de servicio no necesita. Para hacer que el entorno sea un entorno con privilegios mínimos, configure una nueva cuenta de dominio para que la usen el grupo de aplicaciones y la aplicación web adecuados.  
  
 **Para crear una nueva cuenta de dominio SPsvc que se usará como cuenta de servicio de SharePoint:**  
  
1.  En Administración Central de SharePoint, haga clic en **seguridad**.  
  
2.  Haga clic en **configurar cuentas de servicio**  
  
3.  Haga clic en **registrar una nueva cuenta administrada**.  
  
 La cuenta **SPSvc** no tiene privilegios de administrador local y SPsvc no tendrá ningún privilegio en la base de datos de SharePoint. Los únicos privilegios que SPsvc necesita son derechos administrativos en la instancia de PowerPivot de Analysis Services.  
  
 **Para configurar el grupo de aplicaciones adecuado de manera que use la cuenta SPsvc:**  
  
1.  En Administración Central de SharePoint, haga clic en **seguridad**.  
  
2.  Haga clic en **configurar cuentas de servicio**.  
  
3.  Seleccione el grupo de aplicaciones de servicio usado por la aplicación de servicio PowerPivot. Seleccione después la cuenta SPSvc.  
  
 **Para conceder acceso a la aplicación web con PowerShell:**  
  
1.  Ejecute el shell de administración de SharePoint 2013 con privilegios de administrador.  
  
2.  Ejecute el siguiente código de PowerShell:  
  
    ```  
    $webApp = Get-SPWebApplication "http://<servername>"  
    $webApp.GrantAccessToProcessIdentity("DOMAIN\<ServiceAccountName>")  
  
    ```  
  
  
