---
title: "Configuración dinámica mediante Windows PowerShell de energía | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4d83e53e-04f1-417d-9039-d9e81ae0483d
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e25460598e99163c4866b14741bf020208de902b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="power-pivot-configuration-using-windows-powershell"></a>Configuración de Power Pivot mediante Windows PowerShell
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] incluye cmdlets de Windows PowerShell que puede usar para configurar una instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. Para configurar totalmente una instalación con PowerShell es necesario usar cmdlets de SharePoint y de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Gran parte de la configuración se puede completar mediante una de las herramientas de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para obtener más información sobre las herramientas, vea [Power Pivot Configuration Tools](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
> [!IMPORTANT]  
>  En el caso de una granja de servidores de SharePoint 2010, debe instalarse SharePoint 2010 SP1 antes de configurar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint o una granja de SharePoint que use un servidor de bases de datos de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] . Si no ha instalado todavía el Service Pack, instálelo antes de empezar a configurar el servidor.  
  
## <a name="benefits-of-configuring-power-pivot-for-sharepoint-using-powershell"></a>Ventajas de configurar Power Pivot para SharePoint utilizando PowerShell  
 Puede crear archivos de script de Windows PowerShell (.ps1) para automatizar las tareas de configuración. Se recomienda este enfoque si se requieren pasos de instalación y configuración con script que se puedan ejecutar en cualquier servidor. Puede que se necesite un script como parte de un plan de recuperación ante desastres para volver a generar un servidor en caso de un error de hardware.  
  
## <a name="view-a-list-of-the-power-pivot-cmdlets-on-a-server"></a>Ver una lista de los cmdlets de Power Pivot de un servidor  
 Para ver contenido y ejemplos de los cmdlets de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , vea [Referencia de PowerShell para Power Pivot para SharePoint](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md).  
  
 Para usar PowerShell con el fin de ver una lista de los cmdlets de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] :  
  
1.  Abra el Shell de administración de SharePoint usando la opción **Ejecutar como administrador** .  
  
2.  Escriba el comando siguiente:  
  
    ```  
    Get-help *powerpivot*  
    ```  
  
     Debe ver una lista de cmdlets que incluyen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en el nombre del cmdlet. Por ejemplo, `Get-PowerPivotServiceApplication`. El número de cmdlets disponibles depende de la versión de Analysis Services que está usando.  
  
    -   10 cmdlets con el servidor de SQL Server 2012 SP1 Analysis Services configurado en modo de SharePoint, y SharePoint 2013. La versión de 2012 SP1 emplea una nueva arquitectura que permite que Analysis Server se ejecute fuera de la granja de servidores de SharePoint y necesita menos cmdlets de Windows PowerShell de administración.  
  
    -   17 cmdlets con el servidor de SQL Server 2012 Analysis Services configurado en modo de SharePoint, y SharePoint 2010.  
  
     Si no se devuelve ningún comando en la lista o aparece un mensaje de error similar a “`get-help could not find *powerpivot* in a help file in this session.`“, vea la próxima sección de este tema para obtener instrucciones sobre cómo habilitar los cmdlets de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en el servidor.  
  
     Todos los cmdlets tienen ayuda en pantalla. En el ejemplo siguiente se muestra cómo ver la ayuda en línea del cmdlet **New-PowerPivotServiceApplication** :  
  
    ```  
    Get-help new-powerpivotserviceapplication -full  
    ```  
  
     También puede ver solo los ejemplos utilizando la siguiente sintaxis:  
  
    ```  
    Get-help new-powerpivotserviceapplication -example  
    ```  
  
## <a name="enable-power-pivot-cmdlets-on-a-server"></a>Habilitar los cmdlets de Power Pivot en un servidor  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] están disponibles después de instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint e implementar la solución de granja. Las soluciones se implementan al ejecutar la herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Siga estos pasos para habilitar el uso de cmdlets:  
  
1.  Abra el Shell de administración de SharePoint usando la opción **Ejecutar como administrador** .  
  
2.  Ejecute el primer cmdlet:  
  
    ```  
    Add-SPSolution –LiteralPath “C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp”  
    ```  
  
     El cmdlet devuelve el nombre de la solución, su identificador de solución y Deployed=False. En el paso siguiente, implemente la solución.  
  
3.  Ejecute el segundo cmdlet para implementar la solución:  
  
    ```  
    Install-SPSolution –Identity PowerPivotFarm.wsp –GACDeployment -Force  
    ```  
  
4.  Cierre la ventana. Vuelva a abrirla utilizando de nuevo la opción **Ejecutar como administrador** .  
  
## <a name="related-content"></a>Contenido relacionado  
 [Administración y configuración del servidor de Power Pivot en Administración central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [Power Pivot Configuration Tools](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
 [Referencia de PowerShell para Power Pivot para SharePoint](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md)  
  
  

