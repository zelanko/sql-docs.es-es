---
title: Implementar soluciones de Power Pivot para SharePoint | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 94f887aa48a63fbc84e941e6259839bff1327bd3
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984767"
---
# <a name="deploy-power-pivot-solutions-to-sharepoint"></a>Implementar las soluciones de Power Pivot en SharePoint
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Use las instrucciones siguientes para implementar manualmente dos paquetes de soluciones que agregan características de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a un entorno de SharePoint Server 2010. La implementación de soluciones es un paso necesario para configurar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint en un servidor de SharePoint 2010. Para consultar la lista completa de pasos necesarios, vea [Administración y configuración del servidor de Power Pivot en Administración central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
 También puede usar la Herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para implementar las soluciones. Usar la herramienta de configuración es más fácil y más eficiente para una única instalación de servidor, pero podría ser conveniente usar Administración central y PowerShell si prefiere usar una herramienta conocida o si va a configurar varias características al mismo tiempo. Para más información sobre el uso de la herramienta de configuración, vea [Herramientas de configuración de Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
 Antes de implementar las soluciones, primero debe instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint usando los medios de instalación de SQL Server 2012. El programa de instalación de SQL Server instala los paquetes de soluciones que está a punto de implementar.  
  
 Este tema contiene las siguientes secciones:  
  
 [Requisitos previos: compruebe que la aplicación web usa el Modo clásico de autenticación](#bkmk_classic)  
  
 [Paso 1: implementar la solución de granja](#bkmk_farm)  
  
 [Paso 2: implementar la solución de aplicación web de Power Pivot para Administración central](#deployCA)  
  
 [Paso 3: implementar la solución de aplicación web de Power Pivot en otras aplicaciones web](#deployUI)  
  
 [Volver a implementar o retirar la solución](#retract)  
  
 [Acerca de las soluciones de Power Pivot](#intro)  
  
##  <a name="bkmk_classic"></a> Requisitos previos: compruebe que la aplicación web usa el Modo clásico de autenticación  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint solo se admite en las aplicaciones web que usan el modo clásico de autenticación de Windows. Para comprobar si la aplicación usa el modo clásico, ejecute el siguiente cmdlet de PowerShell desde la **SharePoint 2010 Management Shell**, reemplazando **http://\<nombre de sitio de nivel superior >** con el nombre del sitio de SharePoint:  
  
```  
Get-spwebapplication http://<top-level site name> | format-list UseClaimsAuthentication  
```  
  
 Se debería devolver el valor **false**. Si es **true**, no podrá obtener acceso a los datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] con esta aplicación web.  
  
##  <a name="bkmk_farm"></a> Paso 1: implementar la solución de granja  
 En esta sección se muestra cómo implementar soluciones con PowerShell, pero también puede utilizar la Herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para completar esta tarea. Para más información, vea [Configurar o reparar PowerPivot para SharePoint 2010 (Herramienta de configuración de PowerPivot)](http://msdn.microsoft.com/d61f49c5-efaa-4455-98f2-8c293fa50046).  
  
 Esta tarea solo tiene que realizarse una vez, después de instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.  
  
1.  En un servidor que tenga una instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, abra una Consola de administración de SharePoint 2010 con la opción **Ejecutar como administrador** .  
  
2.  Ejecute el siguiente cmdlet para agregar la solución de granja.  
  
    ```  
    Add-SPSolution –LiteralPath “C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp”  
    ```  
  
     El cmdlet devuelve el nombre de la solución, su identificador de solución y Deployed=False. En el paso siguiente, implementará la solución.  
  
3.  Ejecute el siguiente cmdlet para implementar la solución de granja:  
  
    ```  
    Install-SPSolution –Identity PowerPivotFarm.wsp –GACDeployment -Force  
    ```  
  
##  <a name="deployCA"></a> Paso 2: implementar la solución de aplicación web de Power Pivot para Administración central  
 Después de implementar la solución de granja, debe implementar la solución de aplicación web para Administración central. Este paso agrega el Panel de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a Administración central.  
  
1.  Abra un shell de administración de SharePoint 2010 utilizando la opción **Ejecutar como administrador** .  
  
2.  Ejecute el siguiente cmdlet para crear una referencia a Administración central:  
  
    ```  
    $centralAdmin = $(Get-SPWebApplication -IncludeCentralAdministration | Where { $_.IsAdministrationWebApplication -eq $TRUE})  
    ```  
  
3.  Ejecute el siguiente cmdlet para agregar la solución de granja.  
  
    ```  
    Add-SPSolution –LiteralPath “C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotWebApp.wsp”  
    ```  
  
     El cmdlet devuelve el nombre de la solución, su identificador de solución y Deployed=False. En el paso siguiente, implementará la solución.  
  
4.  Ejecute el siguiente cmdlet para instalar la solución de aplicación web en Administración central.  
  
    ```  
    Install-SPSolution -Identity PowerPivotWebApp.wsp -GACDeployment -Force -WebApplication $centralAdmin  
    ```  
  
 Ahora que la solución de aplicación web se implementa en Administración central, puede usar Administración central para completar el resto de pasos de configuración.  
  
##  <a name="deployUI"></a> Paso 3: implementar la solución de aplicación web de Power Pivot en otras aplicaciones web  
 En la tarea anterior, implementó Powerpivotwebapp.wsp en Administración central. En esta sección, implementa powerpivotwebapp.wsp en cada una de las aplicaciones web existentes que admiten el acceso a datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Si agrega más aplicaciones web más adelante, asegúrese de repetir este paso para esas aplicaciones web adicionales.  
  
1.  En Administración central, en Configuración del sistema, haga clic en **Administrar soluciones del conjunto de servidores**.  
  
2.  Haga clic en **powerpivotwebapp.wsp**.  
  
3.  Haga clic en **Implementar solución**.  
  
4.  En **¿Dónde implementarla?**, seleccione la aplicación web de SharePoint para la que desea agregar compatibilidad con las características de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
5.  Haga clic en **Aceptar**.  
  
6.  Repita el mismo proceso con las demás aplicaciones web de SharePoint que también admitirán el acceso a datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
##  <a name="retract"></a> Volver a implementar o retirar la solución  
 Aunque Administración central de SharePoint proporciona la retirada de la solución, no necesita retirar el archivo powerpivotwebapp.wsp a menos que esté solucionando problemas de una instalación o de la implementación de una revisión.  
  
1.  En Administración central de SharePoint 2010, en Configuración del sistema, haga clic en **Administrar las soluciones de la granja**.  
  
2.  Haga clic en **Powerpivotwebapp.wsp**.  
  
3.  Haga clic en **Retirar solución**.  
  
 Si encuentra problemas en la implementación del servidor que le remiten a la solución de granja de servidores, puede volver a implementarla ejecutando la opción **Reparar** en la Herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Las operaciones de reparación mediante la herramienta se prefieren porque requieren menos pasos por su parte. Para más información, vea [Configurar o reparar PowerPivot para SharePoint 2010 (Herramienta de configuración de PowerPivot)](http://msdn.microsoft.com/d61f49c5-efaa-4455-98f2-8c293fa50046).  
  
 Si aun así desea implementar de nuevo todas las soluciones, asegúrese de hacerlo en este orden:  
  
1.  Retirar la solución de aplicación web de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de todas las aplicaciones web de SharePoint que la utilizan.  
  
2.  Retirar la solución de granja de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
3.  Volver a implementar la solución de granja de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
4.  Volver a implementar la solución de aplicación web de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en todas las aplicaciones web de SharePoint.  
  
##  <a name="intro"></a> Acerca de las soluciones de Power Pivot  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint usa dos paquetes de soluciones para implementar sus páginas de aplicaciones y archivos de programas en la granja y en aplicaciones web individuales.  
  
-   La solución de granja es global. Se implementa una vez y después se convierte en disponible automáticamente para todos los servidores nuevos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint que se agreguen posteriormente a la granja.  
  
-   La solución de aplicación Web es específica de la aplicación y se debe implementar en cada aplicación Web de la granja, incluida la aplicación Web Administración central.  
  
 Cada solución se implementa de forma diferente.  La solución de granja se implementa una vez, tras instalar la primera instancia de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Para implementar la solución de granja, use los cmdlets de PowerShell o la Herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 La solución de aplicación web se implementa inicialmente en Administración central, seguida de las siguientes implementaciones de la solución en cualquier aplicación web adicional que vaya a admitir solicitudes de los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para implementar la solución de aplicación web de Administración central, debe usar el cmdlet de PowerShell o de la Herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para todas las demás aplicaciones Web, puede implementar la solución de aplicación Web mediante Administración central o PowerShell.  
  
|Solución|Descripción|  
|--------------|-----------------|  
|Powerpivotfarm.wsp|Agrega los archivos Microsoft.AnalysisServices.SharePoint.Integration.dll al ensamblado global.<br /><br /> Agrega Microsoft.AnalysisServices.ChannelTransport.dll al ensamblado global.<br /><br /> Instala las características y los archivos de recursos, y registra los tipos de contenido.<br /><br /> Agrega plantillas de biblioteca para las bibliotecas Fuentes de datos y Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Agrega las páginas de aplicación para la configuración de aplicación de servicio, el panel de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , actualización de datos y la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|powerpivotwebapp.wsp|Agrega los archivos de recursos Microsoft.AnalysisServices.SharePoint.Integration.dll a la carpeta de extensiones de servidor web del servidor front-end web.<br /><br /> Agrega el servicio web [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] al servidor front-end web.<br /><br /> Agrega la generación de imágenes en miniatura para la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
  
## <a name="see-also"></a>Vea también  
 [Actualización de PowerPivot para SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Administración y configuración del servidor de Power Pivot en Administración central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Configuración de Power Pivot mediante Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
  
