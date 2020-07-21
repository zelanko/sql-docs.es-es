---
title: Configuración de PowerPivot mediante Windows PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4d83e53e-04f1-417d-9039-d9e81ae0483d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 83b42da3e676a291bb021c02ee52e9a810207397
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84535107"
---
# <a name="powerpivot-configuration-using-windows-powershell"></a>Configuración de PowerPivot mediante Windows PowerShell
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] incluye cmdlets de Windows PowerShell que puede usar para configurar una instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. Para configurar totalmente una instalación con PowerShell es necesario usar cmdlets de SharePoint y de PowerPivot para SharePoint. Gran parte de la configuración se puede completar mediante una de las herramientas de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para obtener más información sobre las herramientas, vea [PowerPivot Configuration Tools](power-pivot-configuration-tools.md).  
  
> [!IMPORTANT]  
>  En el caso de una granja de servidores de SharePoint 2010, debe instalarse SharePoint 2010 SP1 antes de configurar PowerPivot para SharePoint o una granja de SharePoint que use un servidor de bases de datos de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] . Si no ha instalado todavía el Service Pack, instálelo antes de empezar a configurar el servidor.  
  
## <a name="benefits-of-configuring-powerpivot-for-sharepoint-using-powershell"></a>Ventajas de configurar PowerPivot para SharePoint utilizando PowerShell  
 Puede crear archivos de script de Windows PowerShell (.ps1) para automatizar las tareas de configuración. Se recomienda este enfoque si se requieren pasos de instalación y configuración con script que se puedan ejecutar en cualquier servidor. Puede que se necesite un script como parte de un plan de recuperación ante desastres para volver a generar un servidor en caso de un error de hardware.  
  
## <a name="view-a-list-of-the-powerpivot-cmdlets-on-a-server"></a>Ver una lista de los cmdlets de PowerPivot de un servidor  
 Para ver el contenido y ejemplos de los [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cmdlets, consulte [referencia de PowerShell para PowerPivot para SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint).  
  
 Para usar PowerShell con el fin de ver una lista de los cmdlets de PowerPivot:  
  
1.  Abra el Shell de administración de SharePoint usando la opción **Ejecutar como administrador** .  
  
2.  Escriba el comando siguiente:  
  
    ```powershell
    Get-Help *powerpivot*  
    ```  
  
     Debe ver una lista de cmdlets que incluyen PowerPivot en el nombre del cmdlet. Por ejemplo, `Get-PowerPivotServiceApplication`. El número de cmdlets disponibles depende de la versión de Analysis Services que está usando.  
  
    -   10 cmdlets con el servidor de SQL Server 2012 SP1 Analysis Services configurado en modo de SharePoint, y SharePoint 2013. La versión de 2012 SP1 emplea una nueva arquitectura que permite que Analysis Server se ejecute fuera de la granja de servidores de SharePoint y necesita menos cmdlets de Windows PowerShell de administración.  
  
    -   17 cmdlets con el servidor de SQL Server 2012 Analysis Services configurado en modo de SharePoint, y SharePoint 2010.  
  
     Si no se devuelve ningún comando en la lista o aparece un mensaje de error similar a " `get-help could not find *powerpivot* in a help file in this session.` ", vea la sección siguiente de este tema para obtener instrucciones sobre cómo habilitar los cmdlets de PowerPivot en el servidor.  
  
     Todos los cmdlets tienen ayuda en pantalla. En el ejemplo siguiente se muestra cómo ver la ayuda en pantalla del cmdlet `New-PowerPivotServiceApplication`:  
  
    ```powershell
    Get-Help new-powerpivotserviceapplication -Full  
    ```  
  
     También puede ver solo los ejemplos utilizando la siguiente sintaxis:  
  
    ```powershell
    Get-Help new-powerpivotserviceapplication -Example  
    ```  
  
## <a name="enable-powerpivot-cmdlets-on-a-server"></a>Habilitar los cmdlets de PowerPivot en un servidor  
 Los cmdlets de PowerPivot están disponibles después de instalar PowerPivot para SharePoint e implementar la solución de granja. Las soluciones se implementan al ejecutar la herramienta de configuración de PowerPivot. Siga estos pasos para habilitar el uso de cmdlets:  
  
1.  Abra el Shell de administración de SharePoint usando la opción **Ejecutar como administrador** .  
  
2.  Ejecute el primer cmdlet:  
  
    ```powershell
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     El cmdlet devuelve el nombre de la solución, su identificador de solución y Deployed=False. En el paso siguiente, implemente la solución.  
  
3.  Ejecute el segundo cmdlet para implementar la solución:  
  
    ```powershell
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
4.  Cierre la ventana. Vuelva a abrirla utilizando de nuevo la opción **Ejecutar como administrador** .  
  
## <a name="related-content"></a>Contenido relacionado  
 [Administración y configuración del servidor PowerPivot en Administración central](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [Herramientas de configuración de PowerPivot](power-pivot-configuration-tools.md)  
  
 [Referencia de PowerShell para PowerPivot para SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
